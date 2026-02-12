# Docker & Qdrant Setup for WSL2

**Environment:** Ubuntu 26.04 (Resolute Raccoon) on WSL2
**Docker Engine:** 29.1.3 (latest: 29.2.1 as of Feb 2026)
**Docker Compose:** v5.0.2
**Status:** Working

---

## 1. Enable systemd in WSL2 (Required First)

WSL2 does not enable systemd by default. Without it, `service` and `systemctl` commands fail silently or error out. This was the root cause of the initial Docker startup failures.

### Step 1: Create or edit `/etc/wsl.conf`

```bash
sudo nano /etc/wsl.conf
```

Add this content:

```ini
[boot]
systemd=true
```

### Step 2: Restart WSL entirely (from Windows PowerShell, NOT from inside WSL)

```powershell
wsl --shutdown
```

Then reopen your WSL terminal.

### Step 3: Verify systemd is running

```bash
ps -p 1 -o comm=
# Expected output: systemd
```

If the output is `init` instead of `systemd`, the WSL restart did not apply. Try `wsl --shutdown` again from PowerShell.

---

## 2. Install Docker Engine

The `docker.io` package from Ubuntu's repository works well and is the simplest option for WSL2.

```bash
# Update package index
sudo apt-get update

# Install Docker and Compose plugin
sudo apt-get install -y docker.io docker-compose-plugin
```

### What gets installed

| Package | Description |
|---------|-------------|
| `docker.io` | Docker Engine (Ubuntu-maintained package) |
| `docker-compose-plugin` | Docker Compose v2 (runs as `docker compose`) |

### Alternative: Docker CE (Official Docker repository)

If you want the latest Docker CE (29.2.x) instead of Ubuntu's `docker.io` package:

```bash
# Add Docker's official GPG key
sudo apt-get update
sudo apt-get install -y ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt-get update

# Install Docker CE
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

---

## 3. Start and Enable Docker Service

Now that systemd is running, Docker service commands work:

```bash
# Start Docker and enable auto-start on boot
sudo systemctl enable --now docker

# Verify the service is active
systemctl is-active docker
# Expected output: active
```

### Add your user to the docker group (avoids needing sudo for every docker command)

```bash
sudo usermod -aG docker $USER
newgrp docker
```

### Verify Docker is working

```bash
docker run hello-world
```

---

## 4. Start Ollama + Qdrant via Docker Compose

Both Ollama (LLM inference) and Qdrant (vector database) run as Docker containers managed by a single `docker-compose.yml` file. Ollama runs in **CPU-only mode** (no GPU passthrough required).

### Step 1: Start the containers

```bash
cd ~/GRA_AI_Scientist/rag_prototype

# Start both services in background
docker compose up -d
```

This creates:

| Container | Image | Host Port | Purpose |
|-----------|-------|-----------|---------|
| `ollama` | `ollama/ollama:0.15.6` | `11435` | LLM inference (CPU-only) |
| `qdrant` | `qdrant/qdrant:v1.16.3` | `6333`, `6334` | Vector database |

### Step 2: Wait for health checks to pass

```bash
# Both containers have health checks - wait ~15 seconds then verify
docker ps
# STATUS should show "(healthy)" for both

# Manual verification
curl http://localhost:11435/api/version    # Ollama
curl http://localhost:6333/healthz         # Qdrant
```

### Step 3: Pull required models (first time only)

Models are stored in the `ollama_data` Docker volume and persist across container restarts.

```bash
# Pull embedding model (~274MB)
docker exec ollama ollama pull nomic-embed-text

# Pull LLM model (~9GB - takes several minutes)
docker exec ollama ollama pull qwen2.5:14b-instruct

# Verify models are available
docker exec ollama ollama list
```

### Step 4: Verify the complete setup

```bash
# Check Qdrant Web UI in browser
# http://localhost:6333/dashboard

# Test Ollama embedding
curl http://localhost:11435/api/embed -d '{"model": "nomic-embed-text", "input": "test"}'

# Run the RAG pipeline
conda activate gra-venv
python app.py "What affects stroke rehabilitation?" --papers 3
```

---

## 5. Docker Compose Reference

### Compose file location

`rag_prototype/docker-compose.yml`

### Common commands

```bash
cd ~/GRA_AI_Scientist/rag_prototype

# Start all services
docker compose up -d

# Stop all services (containers stop, data persists in volumes)
docker compose down

# View logs
docker compose logs ollama
docker compose logs qdrant

# Restart a single service
docker compose restart ollama

# Check status
docker compose ps

# Pull model into Ollama
docker exec ollama ollama pull <model-name>

# List models in Ollama
docker exec ollama ollama list

# Check Docker version
docker --version

# Check Compose version
docker compose version
```

### Architecture

```
Host (WSL2 Ubuntu 26.04)
  |
  |-- Docker Engine (systemd)
  |     |
  |     |-- ollama container (CPU-only)
  |     |     Port: 11435 -> 11434 (internal)
  |     |     Volume: ollama_data -> /root/.ollama
  |     |     Models: nomic-embed-text, qwen2.5:14b-instruct
  |     |
  |     |-- qdrant container
  |     |     Port: 6333 -> 6333 (REST + Dashboard)
  |     |     Port: 6334 -> 6334 (gRPC)
  |     |     Volume: qdrant_data -> /qdrant/storage
  |     |
  |     |-- rag-net bridge network
  |           (containers communicate via service names)
  |
  |-- conda env: gra-venv
        python app.py -> connects to localhost:11435 (Ollama)
                      -> connects to localhost:6333 (Qdrant)
```

### Port mapping explained

| Service | Container Port | Host Port | Why Different |
|---------|---------------|-----------|---------------|
| Ollama | 11434 (default) | 11435 | Codebase was built with port 11435; compose maps it to avoid confusion |
| Qdrant REST | 6333 | 6333 | Standard port, no remapping |
| Qdrant gRPC | 6334 | 6334 | Standard port, no remapping |

---

## Troubleshooting

### "Cannot connect to the Docker daemon"

1. Check if systemd is PID 1: `ps -p 1 -o comm=`
2. If it shows `init`, you need to restart WSL: run `wsl --shutdown` from Windows PowerShell
3. After reopening WSL, run: `sudo systemctl start docker`

### "sudo service docker start" does nothing

This is the sysvinit command. It may silently fail in WSL2. Always use `systemctl` instead:

```bash
sudo systemctl start docker
```

### Quick workaround (no systemd, temporary)

If you cannot enable systemd, start the Docker daemon directly for the current session:

```bash
sudo dockerd &
```

This is **not persistent** across WSL restarts.

---

### Ollama "Connection refused" from pipeline

1. Check container is running: `docker ps | grep ollama`
2. Check health: `curl http://localhost:11435/api/version`
3. If not running: `cd rag_prototype && docker compose up -d ollama`
4. Check models are pulled: `docker exec ollama ollama list`

### Ollama model pull hangs or fails

```bash
# Check Ollama container logs
docker compose logs ollama

# Restart Ollama and try again
docker compose restart ollama
docker exec ollama ollama pull nomic-embed-text
```

### Container ports already in use

```bash
# Find what's using the port
sudo lsof -i :11435
sudo lsof -i :6333

# Kill conflicting process or change port in docker-compose.yml
```

---

## Version History

| Date | Docker Engine | Docker Compose | Ollama | Qdrant | Notes |
|------|---------------|----------------|--------|--------|-------|
| Feb 2026 | 29.1.3 (docker.io) | v5.0.2 | 0.15.6 | v1.16.3 | Docker Compose setup, CPU-only |

---

## Sources

- [Docker Engine Install on Ubuntu (Official)](https://docs.docker.com/engine/install/ubuntu/)
- [Docker Engine v29 Release Notes](https://docs.docker.com/engine/release-notes/29/)
- [Run Docker in WSL2 via systemd](https://dev.to/klo2k/run-docker-in-wsl2-in-5-minutes-via-systemd-without-docker-desktop-28gi)
- [Install Docker in WSL2 without Docker Desktop](https://nickjanetakis.com/blog/install-docker-in-wsl-2-without-docker-desktop)
- [Ollama Docker Setup (Official)](https://docs.ollama.com/docker)
- [Ollama Docker Image](https://hub.docker.com/r/ollama/ollama)
- [Qdrant Docker Image](https://hub.docker.com/r/qdrant/qdrant)
