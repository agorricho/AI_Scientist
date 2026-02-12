nature mental health
Analysis
https://doi.org/10.1038/s44220-024-00359-2
Applying analytics to sociodemographic 
disparities in mental health
Received: 25 November 2023
Accepted: 16 October 2024
Published online: xx xx xxxx
 Check for updates
Aaron Baird   & Yusen Xia 
Mental health services and treatment are unfortunately subject to 
sociodemographic disparities. To address this issue, recent studies have 
begun to apply analytics methods—that is, artificial intelligence in general, 
machine learning and deep learning in particular—toward the identification 
of such disparities and, where possible, mitigation of bias within models 
used in mental health research. However, it is difficult to understand the 
scope and status of such research as it is spread across many journals and 
contexts of study. Here we conducted an analysis of articles in this area. We 
identified 40 articles from 2017 to July 2023 related to the use of analytics 
in the context of sociodemographic disparities in mental health. We find 
that prediction, clustering/grouping and fairness models were most 
often applied in the articles analyzed. A number of mental health-related 
sociodemographic disparities were identified in these articles, for example, 
associated with race/ethnicity, gender, age and socioeconomic status, 
but such findings were typically context dependent. Thus, we also provide 
suggestions in this Analysis on how to both enhance generalizability and 
embrace context-dependent findings, especially via the identification of 
heterogeneous treatment effects, model bias mitigation, use of generative 
artificial intelligence, incorporation of data from devices, and translation of 
f
indings into practice.
A goal of recent policy, practice and research efforts is to identify and 
reduce mental health disparities1. Disparities in health are “potentially 
avoidable differences in health (or in health risks that policy can influ
ence) between groups of people who are more and less advantaged 
socially”2. Mental health disparities are differences in rates of preva
lence and incidence of mental health disease or diagnosis as well as dif
ferences in outcomes related to access and treatment1. In this Analysis, 
we consider both of these types of mental health disparity, as well as 
disparities related to predictions from machine learning (ML) models 
(that is, model bias). We specifically focus on sociodemographic dis
parities associated with mental health3,4. Sociodemographic disparities 
in health care are differences in access to care, treatment or health 
outcomes with respect to one’s socioeconomic status (for example, 
income level), demographic factors (for example, race/ethnicity and 
gender) or location (for example, rural and incarcerated)5–7. Previous 
studies have shown that, unfortunately, sociodemographic disparities 
are present in access to mental health care as well as in treatment, diag
nosis and outcomes1,8.
Identifying and seeking to mitigate such disparities in mental 
health, however, is not trivial as there are many forms of disparities. 
Further, “Mental health disparities are complex, challenging problems 
that involve multiple determinants at the individual, community, 
program, system, and policy levels.”1. While many attempts have been 
made to reduce such disparities, such as through the use of technol
ogy9, structural interventions10 and encouraging more research in this 
important area11, these disparities persist12.
One opportunity to better identify sources of such disparities, 
as well as sources of outcome variations due to such disparities, and 
even mitigate bias where possible, is the application of analytics to 
mental health data. Artificial intelligence (AI), a subset of AI referred 
to as ML and a further subset of ML referred to as deep learning (DL) 
(all referred to collectively here as ‘analytics’) apply “computational 
Institute for Insight, Robinson College of Business, Georgia State University, Atlanta, GA, USA.  e-mail: abaird@gsu.edu
Nature Mental Health
Analysis
Identification
https://doi.org/10.1038/s44220-024-00359-2
Screening
Eligibility
Included
Publications identified through 
search (n = 2,124):
• Web of Science = 1,079
• PubMed = 850
• PsychInfo = 167
• Google Scholar = 22
• IEEE Xplore = 6
Removed duplicates and nonarticles:
• Removed 390 for matching DOIs
• Removed 258 for matching PMIDs
• Removed 33 for matching article titles
• Removed 10 for being book chapters or proceedings
Manual abstract screening of 
n = 1,428 articles
Full text review of n = 59 articles for 
eligibility
• Removed 5 for being protocols or proposals
Removed for not meeting inclusion criteria:
• Removed 1,369 for not including all three required 
concepts (that is, ML/AI + mental health + 
sociodemographic disparity)
Removed for not meeting inclusion criteria:
n = 40 as final corpus of articles 
included for analysis
• Removed 19 for not having at least one 
sociodemographic disparity as a primary 
consideration
Fig. 1 | PRISMA-ScR flow diagram. The flow diagram represents how many articles were selected, included and excluded in each stop of the process of identifying the 
most relevant articles for this study. DOI, digital object identifier; PMID, PubMed identifier (reference number).
methods using experience to improve performance or make accurate 
predictions.”13. These computational methods range from supervised 
to unsupervised as well as newer methods focused on generation of 
content (that is, generative AI) and the processing of unstructured data 
(that is, subtyping or topic modeling applied to clinical notes or other 
unstructured data such as images). There is considerable promise in 
applying such methods to mental health data as they have the potential 
to more granularly identify causes of mental health disparities, dispari
ties in outcomes by subgroup, and biases in underlying data, as well as 
mitigate bias in models where underlying data are biased (that is, one 
subgroup has received more care than another in the past).
However, this field is emerging and, as such, has yet to consolidate 
around a consistent set of findings and/or recommendations. Further, 
while scoping and general reviews have been published on the pres
ence of disparities in mental health8 and the use of DL and AI in mental 
health14,15, there is not yet a study that considers the application of 
analytics toward better understanding of sociodemographic dispari
ties associated with mental health. Thus, we analyze articles here that 
apply analytics toward sociodemographic disparity identification, 
outcome variation and mitigation in mental health. Later, we provide 
insights into opportunities that may further the frontier of knowledge 
in this important field.
Table 1 | Topics, topic labels and associated keywords
Topic 1: distress 
and depression
distress
psychological
depression
emotional
symptoms
subtypes
violence
pandemic
group
Topic 2: violence 
and self-harm
suicide
visits
specialty
risk
hospitalization
claims
black
Topic 3: 
substance use
alcohol
subgroup
opioid
subgroups
substance
screening
black
Topic 4: model 
bias and fairness
biases
fairness
gender
algorithmic
metrics
assessment
SDOH
native
records
severe
visit
drinking
racial
quantity
care
research
systems
to identify areas of similarity, which is measured using keyword coher
ence scores. Similarities are then grouped into clusters called ‘topics’. 
Clusters include similar articles, and each cluster represents a suffi
ciently distinct set of coherent keywords, thus allowing the separation 
Results
Our article search process, described in detail in Fig. 1, first identi
fied 2,124 articles. After removing duplicates, screening abstracts and 
conducting full-text reviews, the final corpus contained 40 articles.
After finalizing our corpus of relevant articles, we identified overall 
topics within the corpus (that is, areas of similarity within clusters of 
articles) and also subtopics within each topic (that is, areas of similarity 
between articles within each topic). To identify primary overall topics, 
we ran several ML topic models with the input being the abstracts, 
discussions and conclusions from the articles in the final corpus. Topic 
modeling evaluates the words and phrases within a corpus and seeks 
of clusters of articles (that is, similarity within the cluster, but differ
ences between the clusters). As described next, to analyze our corpus 
of articles, we applied common topic models including nonnegative 
matrix factorization (NMF), the word embedding-based BERTopic and 
latent Dirichlet allocation (LDA).
We found that, for our corpus, outputs from NMF and BERTopic 
perform similarly, and both performed better than LDA in terms of 
coherence scores and keyword consistency. For the NMF model, high
frequency words (for example, mental, health and disparity) were 
removed that had been used to identify the articles in the first place. 
Stop words were also removed. A term frequency inverse document 
frequency vectorizer was used to vectorize each document (that is, 
Nature Mental Health
Analysis
https://doi.org/10.1038/s44220-024-00359-2
Corpus
Included articles that use analytics to identify or address socioeconomic disparities in 
mental health (n = 40)
Topics
Distress and 
depression (n = 12)
Violence and self- 
harm (n = 7)
Substance use 
(n = 6)
• Vulnerability (n = 5)
• Trauma (n = 3)
Subtopics
• Subtypes/ 
heterogeneity (n = 4)
• Suicide (n = 5)
• Violent 
environments (n = 2)
Model bias and 
fairness (n = 15)
• Alcohol use (n = 2)
• Impact of bias (n = 4)
• Opioid use (n = 2)
• Substance agnostic 
(n = 2)
• Mitigation of bias in 
ML models (n = 4)
• General 
perspectives (n = 7)
Fig. 2 | Topics and subtopics identified within the corpus. This figure represents the topics and subtopics identified through analysis of the final corpus of articles 
included for analysis.
article), which considers the frequency of words appearing in a particu
lar article and all articles in this setting (for example, ref. 16). Then, we 
tested topic models ranging from two topics to ten topics. Topics were 
evaluated by the authors looking at the keywords per topic and assessing 
whether they were orthogonal with respect to meaning across topics. 
If more than one topic had words with similar meanings, the number of 
topics was adjusted until the words per topic uniquely represented the 
topic and did not correlate highly between topics. A four-topic model 
seemed to yield the best results, but we verified this with a second topic 
model, as the selection of a four-topic model was a subjective process. 
Following other topic model-based work17, we subsequently ran three-, 
four- and five-topic topic models using NMF and BERTopic. We deter
mined that the four-topic NMF model yielded the best results (Table 1),  
as the words in each topic were sufficiently similar within each topic 
and different between topics. We report the NMF results here. Once the 
number of topics was finalized, we labeled each topic according to what 
was observed in the keywords, as the algorithm does not automatically 
name each topic. We next assigned each article to one topic, first by 
using the probability of topic assignment from the topic model run, 
and then manually adjusted the assignments, as some articles could 
be assigned to multiple topics. We made the final determination of 
topic by reading all the articles and assigning them on the basis of how 
sociodemographic disparities were assessed (or mitigated).
The next step was to further subdivide the articles assigned to each 
of the above topics into subtopics (that is, subgroups or clusters of 
articles within each topic). Following a similar procedure as used in 
another paper to assign content to topics derived from topic models17, 
the authors of this study evaluated the articles within each topic and 
further grouped them by subtopic using a qualitative coding approach, 
similar to grounded theory coding18. For instance, for the 12 articles 
assigned to topic 1 (distress and depression), we grouped these 12 articles 
into 3 subtopics: (1) vulnerability, (2) trauma and (3) identification of het
erogeneity and/or subtypes, as shown in Fig. 2. This thematic grouping 
process was done similarly to qualitative research where each article was 
manually coded with a thematic code by each author. Then, we compared 
our individual coding results. When the coding between the two authors 
was the same or similar, the article was assigned to the coded subtopic. 
When the coding was different between the authors (that is, an article was 
coded or labeled differently by each author), we jointly discussed what 
code (that is, which thematic label) would best represent the article and 
arrived at a consensus. The results are shown in Fig. 2. Detailed discussion 
of the articles within each topic and subtopic follows.
Distress and depression (topic 1)
We labeled this topic ‘distress and depression’ as the articles assigned 
to this topic focused on the application of analytic methods to data 
associated with stress disorders and depression. Of the 40 total articles 
in our full corpus, 12 were assigned to this topic (details in Table 2). 
The primary methods applied with these articles included prediction 
of having a stress disorder or depression19, natural language process
ing20,21 and, in one case, computer vision using a convolutional neural 
network22. A fascinating variety of datasets were analyzed including 
images from Google Street View22, both structured data23 and unstruc
tured data from electronic health records (EHRs)21 and from Twitter/X20,  
surveys primarily from public sources24–26, and mobile app global 
positioning system data27. In a number of cases, the most vulnerable 
populations were found to be younger, female, belonging to a racial/
ethnic minority and/or of lower socioeconomic status20,26,28. However, 
some contrasting findings were also observed: sociodemographics was 
not a factor in one case19, and racial/ethnic minorities did not report 
as many posttraumatic stress disorder symptoms in other cases22,25, 
perhaps due to more resilience or not wanting to report vulnerabilities.
Within the 12 articles assigned to the ‘distress and depression’ 
topic, we identified 3 subtopics: (1) vulnerability (5 articles), (2) trauma 
(3 articles) and (3) identification of heterogeneity and/or subtypes  
(4 articles). We assigned each article to one subtopic, based on the 
primary focus of the conditions, data or sociodemographic disparities 
considered in the article.
We start by discussing the vulnerability subtopic. We identified 
five articles that included methods and/or findings related to vulner
ability. Within these five articles, three focused on vulnerability within 
the coronavirus disease 2019 (COVID-19) time period to anxiety, depres
sion, stress and suicidal ideation20,26,29. In two of these three articles 
related to COVID-19, the data were from surveys generated by public 
health agencies and the methods were prediction models focused 
on predicting different types of stress (that is, emotional, social and 
work related)26,29. In the third article, the focus was also on emotional 
distress, but rather than prediction, the study applied natural language 
processing, specifically latent semantic scaling, to develop emotional 
distress scores from data retrieved from Twitter/X20. The primary find
ings from these three articles are that younger individuals (18 to 29 or 
39 depending on the study), females and lower-income households 
were more vulnerable to stress during the pandemic. Further, the use 
of ML (for example, XGBoost, least absolute shrinkage and selection 
operator (LASSO) and random forest) and natural language processing 
methods (for example, latent semantic scaling) allowed exploratory 
analysis of large datasets (sample sizes ranging from about 6,000 
to over 2 million) and for previous unestablished trends in the data, 
as COVID-19 has not been experienced prior and, thus, did not have 
historical trends to draw upon when analyzing the data.
The other two articles focused on vulnerability to mental distress 
as a result of the built environment22 and vulnerability to postpartum 
Nature Mental Health
Nature Mental Health
Analysis https://doi.org/10.1038/s44220-024-00359-2
Table 2 | Papers in the distress and depression topic (topic 1)
Citation Aim(s) Data Disparity Methods (related to 
disparities)
Findings (related to disparities)
Subtopic: vulnerability
22 Measure the 
association of 
built-environment 
features with 
health-related 
behaviors
Google Street View data 
(n = 31 million images)
Disparity type: outcome 
variation associated with 
sociodemographic subgroups 
(and environmental factors)
Disparity variables: age (under 
18 and over 65), race/ethnicity 
(white, African American 
and Hispanic), gender and 
socioeconomic disadvantage 
(for example, percent 
unemployment and so on)
Visual geometry group 
(VGG-16) convolutional 
neural network for image 
feature extraction from 
Google Street View 
images. Regression for 
analysis of effects on 
health outcomes.
For all image factors considered 
(street greenness, crosswalks, 
not a single-family home, single 
lane road and visible wires), 
sociodemographic conditions 
in each location associated with 
lower mental distress include 
female, 65+ years of age (and 
higher median age), races/
ethnicities other than white, and 
higher median income.
19 To predict 
women at risk 
for depressive 
symptoms 
at 6 weeks 
postpartum
Utilized a questionnaire for 
2009–2018 (for clinical and 
psychometric self-report, 
and medical journal) (from 
BASIC study; n = 4,313)
Disparity type: outcome 
variation associated with 
sociodemographic subgroups
Disparity variables: education, 
employment and country of 
origin
To predict women at risk 
for postpartum depression, 
extremely randomized 
trees was selected as the 
final model after testing 
ridge regression, LASSO 
regression, gradient 
boosting machines, 
distributed random forests, 
naive Bayes and stacked 
ensembles.
Low positive predictive value 
across all models, but models may 
be best suited to predict the high
risk group. Depression and anxiety 
during pregnancy were most 
important. Sociodemographic 
variables were not highly 
important, but marital status and 
employment were significant in 
univariate analyses; however, they 
were also overrepresented in the 
data.
26 Use ML to identify 
factors related 
to mental health 
and their change 
over the COVID-19 
pandemic
Web-based surveys for 
Canadian adults (n = 6,021)
Disparity type: outcome 
variation associated with 
sociodemographic subgroups
Disparity variables: Canadian 
region, age, gender, has 
children, education, marital 
status, race/ethnicity, income 
and locality
XGBoost and LASSO were 
used to predict emotional 
distress.
Age group 18–39 and female 
gender were associated with 
higher levels of emotional distress.
29 Identification of 
risk factors for 
mental health 
vulnerability 
during the 
pandemic
COVID-19 impact survey 
from the National Opinion 
Research Center (n = 17,764 
adults)
Disparity type: outcome 
variation associated with 
sociodemographic subgroups
Disparity variables: age, gender, 
economic security and social 
dynamics
Prediction of mental health 
indicators, such as anxiety 
and loneliness, was done 
with Bayesian network, 
random forest and support 
vector machine.
Females and those in the 
18–29 age range were the most 
vulnerable to anxiety and stress. 
Income assistance and physical 
social connections help alleviate 
mental health issues.
20 Real-time 
surveillance of 
mental health 
using ML
Tweets from 2019 to 2022 
(n = 2,493,682) and online 
survey response (n = 2,432)
Disparity type: outcome 
variation associated with 
sociodemographic subgroups
Disparity variables: gender, age, 
low income and employment 
stability
Latent semantic scaling 
for distress scores (from 
Twitter data). Fixed-effects 
regression for impacts 
of covariates on distress 
score.
Youngest age considered in 
the study (18–29), unemployed 
and lower-income participants 
had higher distress during the 
pandemic. Females had a high 
level of distress early in the 
pandemic.
Subtopic: trauma
30 Depression 
severity 
classification of 
patients post
breast cancer 
diagnosis
Medical, 
sociodemographic, 
lifestyle and psychosocial 
data of women with breast 
cancer in Europe (n = 609)
Disparity type: ML model 
performance as a result of 
sociodemographic variable 
inclusion
Disparity variables: financial 
difficulties, age, education, 
employment and income
Random forest used to 
predict post-diagnosis 
depression symptom 
severity.
Random forest model 
performance was better than 
a baseline logistic regression. 
However, sociodemographic 
features did not end up as that 
important. More important 
features were related to quality of 
life, resilience trait, cancer stage 
and menopausal status.
25 Examine 
heterogeneity in 
posttraumatic 
stress symptoms 
across adolescents
Annual assessments 
(n = 498; 14–19 years old, 
female adolescents)
Disparity type: outcome 
variation associated with 
sociodemographic subgroups
Disparity variables: age 
(adolescents), race/ethnicity 
(white non-Hispanic versus 
other) and income
Elastic net regression used 
to develop a prediction 
model of posttraumatic 
stress symptoms.
Racial and ethnic minority patients 
were found to be less likely to 
report posttraumatic stress 
disorder symptoms, perhaps due 
to competency with dealing with 
adversity.
23 Develop clinically 
relevant indicators 
of adverse 
childhood 
experiences
EHR data collected from 
2002 to 2018
Disparity type: ML model 
performance as a result of 
sociodemographic variable 
inclusion
Disparity variables: 63 (or 
56 after excluding 7 from 
the reference standard) final 
sociodemographic indicators 
including those associated 
with maternal mental health 
problems and adverse family 
environments
Methods including Cox 
models to reduce 408 
indicators down to 56. 
Prediction models include 
random forest, Cox and 
logistic regression with 
LASSO (a method used to 
select the most impactful 
features by penalizing low 
impact features). Final 
validation was done with a 
balanced random forest.
Linked EHR data between children 
and mothers can be effectively 
used, along with the updated set 
of indicators found in this study, to 
predict childhood maltreatment or 
intimate partner violence.
Nature Mental Health
Analysis https://doi.org/10.1038/s44220-024-00359-2
depression19. In regard to the built environment, this paper used an inno
vative computer vision approach to extract features from street view 
images, such as crosswalks and greenness, to determine if structural 
features had an impact on health and mental health22. They found that 
such features had varied impacts for different sociodemographic groups, 
including lower mental distress associated with being female, higher 
median age, higher income and a higher proportion of African American 
residents. In regard to the paper on postpartum depression, they found 
postpartum depression to be difficult to predict, but depression and 
anxiety during pregnancy to be important predictors19. In this study, they 
did not find sociodemographic variables to be important predictors.
Next, we discuss the trauma subtopic. Three papers were found to 
focus on trauma. Two of these papers focused on minors23,25, and one 
focused on mental health outcomes after a breast cancer diagnosis30. 
Of the two papers focused on minors, one used a novel EHR dataset 
to link children’s records to mother’s records and then developed a 
prediction model using 56 predictors that could predict childhood mal
treatment or intimate partner violence23. Sociodemographic variables 
were included in the model, but their importance or impact was not 
explained in detail. The other paper applied a prediction model (elastic 
net regression), then examined heterogeneity in posttraumatic stress 
such as from abuse or neglect, and found that racial/ethnic minority 
patients were less likely to report posttraumatic stress systems25. They 
surmised this was perhaps due to having developed competencies in 
dealing with adversity or unwillingness to report symptoms. However, 
they used only one model (elastic net) and did not report testing of 
other models, which would have been helpful to verify that the accuracy 
of the elastic net model, and associated findings, was robust. Finally, 
the paper on mental health outcomes after a breast cancer diagnosis 
applied a random forest model to depression severity and found that 
sociodemographic features were not as important as other features, 
such as quality of life and resilience, in their models30.
Finally, we discuss the ‘identification of heterogeneity and/or sub
types’ subtopic. In these papers, the primary goal was to find subgroups 
that exhibited different effects from other subgroups. In other words, 
heterogeneity by subgroup was the objective. We identified four papers 
matching the criteria for this subtopic. Two of the papers used predic
tion models and, through feature importance analysis, found those 
more vulnerable to distress or depression include minorities24 and/
or those in lower socioeconomic groups24,28. One of the papers found 
that trying to predict depression from mobility data gathered from 
smartphones does not scale well to heterogeneous samples, suggesting 
the mobility data are relevant only for specific samples27. Finally, one 
paper grouped patients by depression systems, with a novel application 
of an LDA model, and found that female patients were overrepresented 
in the mild-typical group, white patients were underrepresented in the 
psychotic group, and Black and Asian patients were overrepresented in 
the psychotic group21. We note that they did not report verification of 
these findings through use of other topic models, such as through the 
use of bidirectional encoder representations from transformers (BERT)
based models or other models such as NMF. One recommendation for 
future work like this would be to run multiple topic models and report 
the reasoning behind selecting the results from a specific algorithm.
Violence and self-harm (topic 2)
We labeled this topic as ‘violence and self-harm’ as the models employed 
by articles in this topic focused on predicting suicide, suicidal ideation 
and factors associated with being in violent environments. A total of 
Citation Aim(s) Data Disparity Methods (related to 
disparities)
Findings (related to disparities)
Subtopic: subtypes/heterogeneity
21 To create 
clinically relevant 
depressive 
subtypes
Unstructured data from 
EHR (n = 7,741 patients)
Disparity type: identification of 
underlying bias in the data
Disparity variables: gender, 
race (white, Black, Asian, 
mixed, other), age group and 
neighborhood deprivation
LDA topic modeling for 
subtype identification 
using patient symptoms 
as input. Chi-squared was 
then used for between
group comparisons.
Sociodemographic representation 
was not proportionally distributed 
among the subgroups compared 
with the full sample. For 
instance, female patients were 
overrepresented in the mild
typical group, white patients were 
underrepresented in the psychotic 
group, and Black and Asian 
patients were overrepresented in 
the psychotic group.
27 To determine 
how accurately 
mobility (global 
positioning system 
data) predicts 
depression
MindDoc app users. 
Homogeneous student 
sample (n = 57), 
heterogeneous student 
sample (n = 5,262)
Disparity type: ML model 
performance as a result of 
sociodemographic variable 
inclusion
Disparity variables: age, 
education, ethnicity, gender, 
sexual orientation and rural 
versus urban
Penalized logistic 
regression for prediction 
of depressive symptoms; 
subgroup analysis 
for examination of 
heterogeneity.
Prediction of depression from 
mobility behaviors does not 
scale well to heterogeneous 
samples. When considering 
sociodemographic conditions, 
prediction performance was 
low for ‘rural’ but was otherwise 
consistent, suggesting that 
bias was not present for 
sociodemographic conditions.
28 Estimate the 
effect of traumatic 
experiences on the 
mental health of 
survivors
The Iwanuwa study in 
Japan (n = 4,957 residents)
Disparity type: outcome 
variation associated with 
sociodemographic subgroups
Disparity variables: gender, 
age, marital status, living 
alone, education attainment, 
employment status and 
equalized household income
Generalized random 
forest for prediction of 
posttraumatic stress 
symptoms.
Those in lower socioeconomic 
groups with preexisting 
depression symptoms were the 
most vulnerable to disaster and 
disaster impacts.
24 To examine 
predictors that 
affect self
reported severe 
psychological 
distress
HINTS survey (n = 9,303) Disparity type: outcome 
variation associated with 
sociodemographic subgroups
Disparity variables: gender, 
race, age, income range, census 
region and marital status
Logistic regression; other 
models used for feature 
importance were GLM, 
random forest, DL and 
GBM.
More severe psychological distress 
was significantly associated with 
LatinX or ‘other’ race, female, 
bisexual or other orientation, lower 
education, lower income and 
residing in central, mountain or 
Pacific areas.
HINTS, Health Information National Trends Survey; GLM, generalized linear model; GBM, gradient boosting machine.
Table 2 (continued) | Papers in the distress and depression topic (topic 1)
Nature Mental Health
Analysis https://doi.org/10.1038/s44220-024-00359-2
seven articles were included in this topic (details in Table 3). These 
seven articles were further subdivided into two subtopics: (1) suicide 
(five articles) and (2) violent environments (two articles).
Within the suicide subtopic, the primary goal of these studies was 
to predict suicide with both known and novel risk factors31–34 and, in one 
case, to develop a typology of those who died from homicide–suicide35. 
In all cases, the methods applied were for prediction and included logistic 
regression with LASSO31,32,35, random forest31,33 and XGBoost with the syn
thetic minority over sampling technique (SMOTE) to address imbalanced 
data34. In one case, latent class analysis was also applied to subdivide the 
sample into subtypes35. The overall findings related to sociodemographic 
conditions were that prediction accuracy was higher when including 
Table 3 | Papers in the violence and self-harm topic (topic 2)
Citation Aim(s) Data Disparity Methods (related to 
disparities)
Findings (related to disparities)
Subtopic: suicide
31 To evaluate racial 
differences in the 
performance of 
statistical model in 
suicide prediction
Data from 7 health 
systems, EHR and 
insurance claims data 
(n = 1,398,070 visits by 
1,433,543 patients)
Disparity type: ML model 
subgroup performance 
variation associated with 
sociodemographic subgroups
Disparity variables: race/
ethnicity (all)
To predict suicide within 
90 days of a mental 
health visit where 
logistic regression with 
LASSO and random 
forest were applied.
Models for specific race/ethnic 
subgroups performed poorly 
compared with population models. 
Thus, predictive performance is not as 
good for those in the Black, American 
Indian/Alaskan Native or no race/
ethnicity recorded subgroups.
32 Examine how specific 
data types affect 
accuracy of suicide 
prediction models
Health record and 
insurance information 
on patients, 13 years 
of age and older, 
from 2009 to 2015 
(n = 2,960,929)
Disparity type: ML model 
performance associated 
within inclusion of 
sociodemographic variables
Disparity variables: race/
ethnicity and neighborhood 
characteristics
Logistic regression with 
LASSO for prediction of 
suicide attempts.
Additional data, including 
sociodemographic data, improved 
prediction accuracy.
35 Characterize 
homicide–suicide 
decedents in the 
United States
CDC NVDRS Restricted 
Access Database. From 
2003 to 2015 (n = 2,447)
Disparity type: ML model 
subgroup performance 
variation
Disparity variables: gender, 
race, age group, marital status 
and military service
Latent class analysis for 
subtype identification. 
LASSO logistic 
regression with one 
versus rest to determine 
characteristics 
associated with 
subtypes.
Eight homicide–suicide subtypes were 
found. Demographic characteristics 
were associated with each type.
33 To find evidence 
of the impact of 
hospitalization on 
suicide prevention
Data from California 
Office of Statewide 
Health Planning 
and Development, 
deliberate self-harm 
visits from January 
2009 to December 
2011 (n = 57,312)
Disparity type: outcome 
variation associated with 
sociodemographic subgroups
Disparity variables: gender, 
age
Generalized random 
forest for prediction 
of suicide risk within 
30 days and 1 year of a 
hospitalization.
More suicide risk was found for 
patients who were male, aged 10–29 
and 50 years of age or greater.
34 Identify factors of 
suicidal ideation 
among teenagers in 
Korea and examine 
the link between 
these factors and 
socioeconomic status
Data from Korea 
Youth Risk Behavior 
Web-based Survey 
(n = 54,948 youth from 
800 schools in 17 
cities)
Disparity type: outcome 
variation associated with 
sociodemographic subgroups
Disparity variables: 
sample focused on 
adolescents; gender, 
academic performance and 
socioeconomic status
XGBoost with SMOTE 
used for prediction of 
suicidal ideation.
Suicidal risk factors for Korean 
adolescents in the high 
socioeconomic group were academic 
achievement as opposed to emotional 
stress and anxiety for those in the low 
SES group. Higher levels of risk were 
shown to be associated with those in 
the lower SES group.
Subtopic: violent environments
36 Identify the most 
relevant factors 
associated with 
different confessed 
domains of violence
Data from large sample 
of ex-members of 
Colombian illegal 
armed groups 
(n = 26,349)
Disparity type: ML 
model performance as 
a result of inclusion of 
sociodemographic features
Disparity variables: age, 
gender and education
Deep neural network, 
random forest classifier 
for recursive feature 
elimination.
Classification of those committing past 
acts of violence was more accurate 
when including sociodemographic 
factors. Effects of individual 
sociodemographic features (that is, 
age, gender and education) were used 
for matching in the analysis; effects 
of those individual features were not 
reported.
37 Impact of living in 
politically violent 
environments on the 
mental and cognitive 
health of children
Primary data extracted 
from the national 
health behavior in 
school-age children 
study conducted 
in Palestinian 
territories (n = 6,374 
schoolchildren)
Disparity type: ML 
model performance as 
a result of inclusion of 
sociodemographic features
Disparity variables: age, 
parents’ education, family 
income, place of residence, 
school type and additional 
variables such as social 
support
Random forest, artificial 
neural network, support 
vector machine, 
gradient boost, decision 
tree and k-nearest 
neighbors used for 
classification of 
domains of violence.
Maltreatment and exposure to political 
violence were the top two most 
important features when considering 
impacts to lower cognitive ability. 
Academic performance of boys 
was inversely related to exposure to 
political violence. While age was not 
found to be a significant predictor, 
variables such as living in an urban 
area with more exposure to violence 
were found to be associated with more 
mental health issues.
CDC NVDRS, Centers for Disease Control National Violent Death Reporting System; SES, socioeconomic status.
Nature Mental Health
Analysis https://doi.org/10.1038/s44220-024-00359-2
sociodemographic data. Findings for specific sociodemographic sub
groups were limited, but one study found that predictive accuracy was 
low for minority subpopulations31 and one study found that suicide risk 
was higher for males in the 10–29 or over 50 age ranges33. All the datasets 
used were structured data from medical records, insurance claims or 
public health agencies that tracked suicides and deaths.
Within the violent environments subtopic, two papers examined 
how to best classify those who had previously committed violent acts 
as part of illegally armed groups in Colombia36 and how to best predict 
cognitive scores for children exposed to violence in the Palestinian 
territories37. In both cases, advanced methods were used to establish 
high accuracy, including deep neural network and random forest meth
ods. The primary findings related to sociodemographic disparities were 
that including sociodemographic factors (for example, age, gender 
and/or education level) improved accuracy and/or explainability and, 
in some cases, that outcomes varied by sociodemographic subgroup.
Substance use (topic 3)
We labeled this topic as ‘substance use’ as the articles assigned to this 
topic focused on predicting or explaining the use of substances either 
Table 4 | Papers in the substance use topic (topic 3)
Citation Aim(s) Data Disparity Methods (related to 
disparities)
Findings (related to disparities)
Subtopic: alcohol use
38 Use models to identify 
patterns of high-risk 
drinking
Web-based survey 
of Brazilian medical 
students (n = 4,254 
medical students)
Disparity type: outcome and ML 
performance variation associated 
with sociodemographic subgroups
Disparity variables: age, gender 
(and gender identification), sexual 
orientation, income, marital status, 
has children, living situation and 
social considerations such as quality 
of family and friend relationships
Random forest, 
GLMNET and ANN for 
prediction of high-risk 
drinking. LIME for 
feature importance 
and explanation.
Either lower or higher (that is, not 
middle) income, being single, 
being bisexual and tobacco and 
cannabis use were the most 
important predictors of high-risk 
drinking. Lower precision was 
seen in female-specific models 
for high-risk drinking, but higher 
precision for low-risk drinking 
models.
40 Identify predictors of 
screening for alcohol 
quantity
Data from National 
Alcohol Survey 
(n = 9,668 respondents)
Disparity type: outcome variation 
associated with sociodemographic 
subgroups
Disparity variables: gender, age, race/
ethnicity, education, marital status, 
primary care source and insurance
Logistic regression 
and CART to predict 
screening of alcohol 
usage quantity.
In logistic regression results, 
college graduates and those 
over 35 years of age were 
more likely to be screened for 
alcohol use. CART results find 
additional subgroups, including 
that nonwhite individuals with 
high school education (or less 
education than high school) were 
less likely to be screened for 
alcohol use quantity.
Subtopic: opioid use
39 To find evidence to 
support individualized 
approach to improve 
outcome of cessation 
attempts
1,192 African American 
and 2,557 European 
ancestry. Each ML 
model had a different 
combination of these 
two
Disparity type: outcome variation 
associated with sociodemographic 
subgroups
Disparity variables: race (African 
American versus European ancestry)
Support vector 
machine to classify for 
opioid use cessation 
versus noncessation.
Racial differences included 
a stronger association with 
substance initiation for antisocial 
behaviors in European ancestry 
children than African American 
children, and a stronger 
association with African American 
for gambling problems than with 
European ancestry.
41 Subgroup analysis 
to identify what 
characteristics 
beyond race make 
individuals vulnerable 
to receive opioid use 
disorder care
Substance use 
disorder dataset from 
Treatment Episode 
Data Set admissions 
(A) (n = 188,637 
from California and 
n = 184,276 from 
Maryland)
Disparity type: outcome variation 
associated with sociodemographic 
subgroups
Disparity variables: race/ethnicity, 
homelessness status, age, gender, 
marital status, education level, 
employment status, income and 
pregnancy status
Virtual twins (random 
forest in stage 1; 
decision tree in stage 
2) for prediction 
of wait times and 
explanation of 
heterogeneity.
Longer wait times were 
associated with being African 
American as opposed to white. 
Individuals who were African 
American and also homeless 
had the longest waiting times for 
treatment.
Subtopic: substance agnostic
17 To understand topics 
of discussion on 
Twitter in association 
with telehealth for 
mental health
Tweets from 2014 to 
2021 (n = 353,554)
Disparity type: subgroup 
representation in the data
Disparity variables: subpopulations 
identified in topic analysis: military, 
veterans, children and parents
BERTopic used to 
extract primary topics 
of discussion.
Primary topics were anxiety, 
depression, addiction and 
rehabilitation, but subpopulation 
discussions shifted from 
a prepandemic emphasis 
on military, veterans and 
posttraumatic stress disorder to 
child- and parent-focused issues 
during the pandemic.
42 To examine the 
disparities in the 
completion of 
substance use 
disorder treatment
Treatment Episode 
Data Set discharges (D) 
(n = 649,479)
Disparity type: outcome variation 
associated with sociodemographic 
subgroups
Disparity variables: race/ethnicity, 
income source, gender, age, health 
insurance and veteran
Virtual twins (random 
forest in stage 1; 
decision tree in stage 
2) used to predict 
treatment completion 
and explain 
heterogeneity.
Individuals more likely to 
complete treatment do not have 
co-occurring mental health 
condition, have income from a job 
and are white non-Hispanic.
GLMNET, generalized linear model net; ANN, artificial neural network; LIME, local interpretable model-agnostic explanations
Nature Mental Health
Analysis https://doi.org/10.1038/s44220-024-00359-2
deemed illegal or in excess. We found six articles that applied analyt
ics within the context of substance use (details in Table 4). We further 
subdivided these six articles into three subtopics: (1) alcohol use (two 
articles), (2) opioid use (two articles) and (3) substance agnostic (two 
articles). Within this overall topic, the use and application of analytic 
methods was quite diverse, even more diverse than in the other topics. 
Methods applied include prediction38,39, a mix of regression and deci
sion trees40, a causal ML method called ‘virtual twins’ that makes use 
Table 5 | Empirical papers in the model bias and fairness topic (topic 4)
Citation Aim(s) Data Disparity Method (final) Findings (especially related to 
disparities)
Subtopic: impact of bias
16 Impact of bias on 
predicting mortality 
and readmission
Unstructured clinical 
and psychiatric notes 
(MIMIC-III dataset) 
from 2011 to 2015 
(n = 3,202).
Disparity type: ML model bias 
related to sociodemographic 
features
Disparity variables: race, gender 
and insurance type
LDA (for topics) and 
logistic regression with 
L1 regularization (for 
prediction).
Heterogeneity was found in topics 
for gender and insurance type; race 
was not significant. Differences 
in error rates were observed for 
insurance type for psychiatric 30-day 
readmission, and both gender and 
insurance type for ICU mortality.
47 To understand 
average gender 
transition sentiment 
patterns
n = 41,066 posts from 
240 Tumblr transition 
blogs
Disparity type: using ML to 
reduce group membership bias
Disparity variables: transgender 
(and gender transition)
Sentiment with 
linguistic inquiry 
word count. Final 
classification of 
sentiment with 
AdaBoost.
Sentiment increases over time but 
was observed to dip in the transition 
stage (when assessing sentiment of 
Facebook disclosures).
48 Impact of behavioral 
health accessibility on 
incarceration rates
Incarceration trends, 
County Health 
Rankings and Uniform 
Crime Report
Disparity type: ML model bias 
related to sociodemographic 
features
Disparity variables: rural, income, 
race (African American % and 
Hispanic %), high graduation rate, 
health care access violent crime 
rate and police per capita
LASSO for feature 
selection; beta 
regression to predict 
jail population per 
capita.
Physically unhealthy days, lower rates 
of psychiatrists per capita, high health 
care costs and lower percent of drug 
treatment paid by Medicaid are more 
predictive of jail population than the 
violent crime rate.
46 Examine how 
combined exposure to 
heat and air pollution 
affects health and 
how it varies across 
inter- and intraurban 
areas
Data from Google 
Earth Engine (from 
Landsat 8 for 16 
days), SA1 (n = 57,523 
areas)
Disparity type: ML model bias 
related to sociodemographic 
features
Disparity variables: many 
sociodemographic factors 
including age, ethnic diversity, 
has children, mobile living, 
unemployed and education
Principal components 
analysis (for dimension 
reduction) and global 
random forest (for 
feature importance 
and accumulated local 
effects).
The top five most important variables 
associated with mental health in 
urban areas were low socioeconomic 
status, distances to public facilities, 
compact design, crowded living 
and health care access. The top 
five in rural areas were minority, low 
socioeconomic status, distance to 
public facilities, crowded living and 
proportion of Indigenous population.
Subtopic: mitigation of bias in ML models
51 Reducing bias in ML 
models
IBM MarketScan 
Medicaid Database 
(n = 573,634 females)
Disparity type: ML model bias 
related to sociodemographic 
features
Disparity variables: race (Black 
versus white) for pregnant 
females receiving Medicaid
Logistic regression 
with L2 regularization 
for predicting 
postpartum depression 
and mental health 
services use.
White females were two times as likely 
to be diagnosed with postpartum 
depression and were 37% more likely 
to utilize mental health services. 
Of the three mitigation techniques 
applied (prejudice remover, 
reweighting and fairness through 
unawareness), reweighting worked 
best.
50 Assessment of bias in 
existing classifier
EHR data (n = 1,000 
for original classifier; 
n = 53,974 for the 
external validation 
of bias)
Disparity type: ML model bias 
related to sociodemographic 
features
Disparity variables: race/
ethnicity—Black, Hispanic/LatinX, 
white and other
Fairness of 
existing classifier 
(convolutional 
neural network) 
for classification of 
patients by opioid 
misuse (or nonmisuse).
Bias found in FNR of Black subgroup 
compared with the white subgroup 
in the original classifier. Post-hoc 
mitigation reduced bias.
52 Examine the 
susceptibility of 
common ML models 
in mental health to 
bias
Labeled dataset from 
previous study (n = 55)
Disparity type: ML model bias 
related to sociodemographic 
features
Disparity variable: gender
Random forest to 
classify mental health 
status.
Disparity found with respect to 
gender. Bias mitigation was effective 
when balanced error rate applied in 
the preprocessing phase, albeit with 
some accuracy loss.
53 Gender disparities 
in algorithms for 
prediction of anorexia
Spanish dataset of 
177 ‘anorexia’ users 
(n = 471,262 tweets) 
and 326 ‘nonanorexia’ 
users (n = 910,967 
tweets)
Disparity type: ML model bias 
related to sociodemographic 
features
Disparity variable: gender
Logistic regression 
classifier for 
classification of 
anorexia nervosa.
The FNR was higher for females (FNR 
0.082) than for males (0.005). Age, 
emotion and personal concerns, 
attributed to body dissatisfaction 
in the discussion section, were 
primary predictors for females. Bias 
mitigation techniques provided some 
improvement, but not complete 
removal of bias.
MIMIC-III, Medical Information Mart for Intensive Care III
Analysis
https://doi.org/10.1038/s44220-024-00359-2
of both prediction and decision trees41,42, and topic modeling through 
use of BERTopic17.
Within the alcohol use subtopic, the primary focus was the identi
fication of patterns associated with high-risk or high-quantity alcohol 
use. One study found that a number of sociodemographic factors 
were predictive of high-risk drinking in Brazilian medical school stu
dents, including either being high or low (not middle) income, being 
single, being bisexual and use of other substances including tobacco 
and cannabis38. The other study in this subtopic used both logistic 
regression and classification and regression trees (CART) to find that 
alcohol consumption screening is most likely for college graduates 
over 35 years of age but is less likely for individuals of color with high 
school education or less40.
Within the opioid use subtopic, both studies focused on racial 
differences related to treatment. In the first study in this subtopic, 
race was shown to have differential impacts on factors associated with 
opioid cessation39. In the second study, the virtual twins model (also 
known as S meta-learner) was applied43,44. A virtual twins model is one 
that first seeks to predict an outcome and then predicts again with the 
counterfactual variable changed (that is, race changed from African 
American to white). This change in variable simulates how the predic
tion would be different if the single variable were different for that one 
person. Then, the difference in predictions is the target variable in the 
second stage that seeks to explain the variation with a decision tree. In 
this work, it was found that African Americans often have longer wait 
times for opioid treatment services and that other variables interact 
to exacerbate that effect, such as by also being homeless41.
In the next subtopic, focused on substance use more generally 
(that is, substance agnostic), the same virtual twins method was applied 
to explain what types of individual are most likely to complete treat
ment. In this work, it was found that not having a co-occurring mental 
health condition, being employed and being white non-Hispanic were 
all predictive of successfully completing substance use treatment42. 
Finally, another work in this subtopic examined unstructured data from 
Twitter (before changing to X) focused on consumer perceptions of 
telehealth for mental health, particularly directly before and during/
after the peak of the pandemic. This study found that prepandemic 
tweets in this context primarily focused on topics including the mili
tary, veterans and posttraumatic stress disorder but shifted to children 
and parents during and after the peak of the pandemic17.
Model bias and fairness (topic 4)
We labeled this topic ‘model bias and fairness’ as the articles within 
this topic focused on identification of bias within models as well as 
ways to mitigate model-based biases, which is referred to as fairness 
in analytics parlance45. In brief, bias in this sense means that a model 
might have higher prediction accuracy for one sociodemographic 
group over another, which creates disproportionate and potentially 
unfair predictions. Such bias often occurs due to training a model on 
data that are either biased themselves or do not contain sufficient 
representation for all subgroups seeking to be modeled. If such model 
bias is detected, it can potentially be mitigated or reduced with fairness 
approaches, such as by adjusting predictions to be more proportion
ally appropriate given known population parameters (for example, 
adjusting predictions to more appropriately balance between genders 
even though there is gender imbalance in the data). In this section, we 
discuss articles that have detected bias in ML models associated with 
sociodemographic variables in the context of mental health. Some of 
the articles have also sought to mitigate such bias to the extent possible 
using fairness algorithms (details in Table 5).
We also note that, when conducting our article search, we found 
seven articles that were either perspectives or reviews. We consider 
these to be nonempirical articles as they do not use data to derive their 
conclusions or contributions. These articles are valuable to consider 
as they provide insights and recommendations at a higher level, and 
Table 6 | Nonempirical (for example, perspective or review) 
papers in the bias and fairness topic (topic 4)
Citation
54
55
60
56
58
57
59
Area of focus (for 
disparities)
Social determinants
Sex/gender
Includes a table that 
reviews the literature 
on individual predictor 
variables such as gender 
and age.
Gender, age, race/
ethnicity and 
socioeconomic variables
Evaluation of bias in 
research studies that 
use natural language 
processing models trained 
via GloVe or Word2Vec
Overcoming challenges, 
such as algorithmic bias, 
with respect to applying 
AI toward precision 
behavioral health
Recommendations (with respect to 
mental health disparities)
Suggest ingesting and integrating 
data from multiple sources, 
including both clinical encounter 
and nontraditional sources such as 
social media and wearables, toward 
understanding which individuals 
might not be actively seeking care 
but could use assistance.
Recommend eradicating “existing 
undesirable sex and gender biases 
from datasets, algorithms and 
experimental design”.
Regarding individual predictors, 
the study states, “No single variable 
was found to consistently predict 
treatment response across multiple 
reviews”. They go on to state that 
heterogeneity and context are 
important considerations.
No indications related to gender, 
race or age/ethnicity were 
associated with antidepressant 
choice in practice. Socioeconomic 
status and race were suggested to 
be considered for attrition rates.
Many of the models within papers 
considered were trained with social 
media data. Only 2 of the 52 studies 
considered bias. Recommendations 
include consideration of bias with 
respect to gender, sexuality, race 
and ethnicity when training and 
implementing natural language 
processing models.
Several challenges are identified, 
including algorithmic bias. 
Regarding such bias, the 
recommendation is to leverage 
determinants to address algorithmic 
bias. Such determinants (for 
example, homelessness) can be 
used in models to tailor interventions 
but also must be assessed regarding 
fairness (that is, to prevent 
inequitable resource allocation).
Develop fairness-aware AI.
Mitigating bias in AI for 
mental health
we found all these nonempirical articles to primarily focus on biases, 
sources of bias or ways to address bias. Thus, we consider all seven of 
these nonempirical articles within this ‘model bias and fairness’ topic 
(more details in Table 6). Overall, out of the 40 total articles in our cor
pus, 15 were assigned to this topic. We then subdivided these 15 articles 
into three subtopics: impact of bias (4 articles), mitigation of bias in ML 
model (4 articles) and general recommendations and perspectives on 
bias from nonempirical articles (7 articles). We discuss each of these 
subtopics in more detail now.
In regard to the impact of bias, the articles within this subtopic 
demonstrate that the presence or absence of model bias is conditional 
on context and condition and can often be identified or addressed 
with the inclusion of novel data or post-hoc analyses. For instance, 
when examining unstructured psychiatric notes and seeking to use 
information extracted from these notes to predict psychiatric 30-day 
readmission and intensive care unit (ICU) mortality, biases (that is, 
prediction errors) were primarily found with respect to gender and 
insurance type, but not race16. Another article found both similarities 
and differences in variables needed to predict mental health in urban 
Nature Mental Health
Analysis
https://doi.org/10.1038/s44220-024-00359-2
versus rural areas in Australia using a dataset to extract features and 
effects of exposure to excessive heat and air pollution, where low 
socioeconomic status was consistently a predictor, but minority and 
proportion of Indigenous population were most predictive only in 
rural areas46. Additional articles focused on understanding the senti
ment throughout a gender transition lifecycle to more appropriately 
tailor treatment and advice47 as well as the impact of accessibility of 
behavior health services on incarceration rates48. An overall theme of 
these articles is that biases are often found in either the models, such 
as by measuring prediction errors (that is, false negative or false posi
tive rates) or disproportionality (that is, selection rate), or the data, 
but the type of bias and the impact are context dependent. Thus, as 
discussed next, mitigation strategies need to be tailored to the type 
of bias observed and the context and will often need to include novel 
sources of data to fully capture all environmental, social and acces
sibility determinants.
Mitigation of bias requires at least two things: (1) acknowledge
ment of potential bias in models or underlying data and (2) determina
tion of the best way to either remove the bias from the data or correct 
for the bias in the model itself49. Removal of bias is typically done with 
fairness algorithms or corrections45 that attempt to make corrections 
when biases are observed and then desired to be accounted for. One 
study within this subtopic found that the false negative rate (FNR) was 
biased against Black individuals as opposed to white individuals and 
corrected for this using post-hoc mitigation50. Another study found 
that white females were twice as likely to be diagnosed with postpar
tum depression and, thus, were more likely to utilize assistive ser
vices. To address such data-based bias, the study focused on assessing 
three different bias mitigation methods and found that a reweighting 
approach worked best51. Additional studies found disparities related 
to gender in mental health assessments52 and for predicting anorexia53. 
Bias was mitigated in one case by balancing the error rates52 and in 
another by reweighting53, but neither was able to completely remove 
the bias. Thus, one important lesson is that underlying biases cannot 
be removed by technical means alone and will probably require more 
comprehensive efforts. This will be discussed further later.
Given this overall lesson, it is probably unsurprising that several 
nonempirical papers (that is, perspectives, viewpoints and reviews) 
have been written about identifying and addressing biases at a deeper 
level than technical correction. We identified seven such nonempirical 
papers in our search. A general theme in these works is that biases are 
present in most data, at least in their view, and it is incumbent upon 
those either managing the processes that generate the data or those 
who are analyzing the data to identify and mitigate bias, such as by 
providing corrections for prediction errors. A more comprehensive 
approach suggested by some of the articles is to start by eliminating 
as much bias as possible from the data themselves, such as by inte
grating data from both clinical and social sources54 and by designing 
studies to address such biases from the start55. Further, a number of 
these articles also suggested that simply considering bias, rather 
than ignoring it or avoiding it, would go a long way toward making 
predictions and classifications more fair56–59. Finally, it was also found 
that biases are not always consistent and, thus, are subject to hetero
geneity, requiring that biases be evaluated in full for all models and 
research designs56,60.
Discussion
The principal finding of this analysis is that analytics—AI, ML, DL and 
related methods—are beginning to effectively identify and help reduce 
model bias associated with sociodemographic disparities in the context 
of mental health research. We find that the application of novel methods 
(for example, neural networks22,36,50, virtual twins41,42 and prediction 
models that include use of LASSO or SMOTE34,35) as well as the inclu
sion of novel data (for example, social determinants30, environmental 
features22 and socioeconomic status28) and bias mitigation with fairness 
techniques50–52 all go a long way toward improving prediction, grouping, 
understanding and mitigation of model bias associated with dispari
ties in mental health. We specifically observe three types of ML-based 
methods being used in the studies analyzed here: (1) prediction models, 
(2) clustering or grouping models and (3) fairness models (which are 
typically prediction plus bias correction). Further, the most specific 
findings tended to be associated with a specific measurable outcome 
(for example, suicide) in the data, while the most variation in findings 
was observed for mental health issues with more ambiguity in causes 
and outcomes (for example, causes of distress and depression).
While excellent work is emerging in this important area, we see 
considerable opportunities for future research, as discussed further 
below. In particular, new methods now allow for identification of het
erogeneity (for example, application of the causal forest method61), 
which could then be followed up by explicit application of fairness 
methods when bias is detected62. Generative AI can now be used to 
synthesize complex and large data streams, helping providers and 
patients to more quickly understand the latest research and even sum
marize sensor and interventional data when seeking to personalize 
treatment. Synthetic data can be used to develop models outside of 
access to restricted information, thus helping to move the field for
ward while respecting the need for data limits. In addition, novel data 
sources, such as from sensors and trackers, may be able to help with 
continuous monitoring and intervention. We suggest that, as research 
expands in this area, future systematic reviews may help to consolidate 
findings, especially when causes and outcomes have more variation, 
such as for depression and anxiety. Thus, we recommend publishing 
both incremental findings (for example, individual studies that identify 
disparities) and integrated findings (for example, systematic reviews 
that consolidate incremental findings).
We note some limitations of our study. First, we conducted as 
thorough of a search as reasonably possible, but it is possible that some 
articles were not indexed or were not picked up by our search terms, 
thus resulting in not including some relevant articles. Second, dispari
ties are complex and intersectional, and we acknowledge that some 
disparities may not be fully represented in our results, particularly 
when at the intersection of multiple factors or variables.
Future research
We observe from the articles included in this analysis that analytic 
methods, and larger, more detailed datasets, are helping to identify and 
in some cases reduce model bias associated with sociodemographic 
disparities in mental health. While such work is commendable, it is 
only the start of what could be accomplished. In particular, present 
research in this area has three primary limitations: (1) more in-depth 
analyses are needed to consider more possible intersections between 
variables as well as further validation from follow-on studies to verify 
that findings are in fact consistent, (2) a majority of the studies focus 
on identification of sources of disparities or disparity-related outcome 
variation but do not typically focus on solutions or mitigation strate
gies, and (3) most studies do not consider various types of dynamics, 
such as temporal and situational dynamics, which would also help 
enhance validation of situations under which effects can be expected 
to be observed. As discussed in the following subsections, there is 
considerable opportunity in this area to further analyze disparities 
and validate findings.
Identification of heterogeneous treatment effects. In regard to more 
in-depth analyses and further identifications of variable intersections, 
research focused on the identification of heterogeneous treatment 
effects (HTEs) is an excellent opportunity for future research in this 
area. While there is abundant research that identifies effects of treat
ment on mental health conditions (for example, ref. 63), often such 
methods rely on the estimation of average treatment effects. However, 
such averages may not be sufficiently applicable to all individuals64. 
Nature Mental Health
Analysis
https://doi.org/10.1038/s44220-024-00359-2
For instance, in the context of substance use disorder treatment, we 
know that, on average, attending self-help groups can help maintain 
substance use abstinance, but the degree of attendance and associ
ated outcomes can vary due to social determinants42,65. Thus, one 
excellent best practice moving forward would be to follow up any 
identification of one or more average treatment effects with an HTE 
analysis to see how much variation exists (for example, ref. 42). By 
using analytic methods to identify HTEs, more specific intersections 
of variables can then be identified that may indicate subgroups for 
which more mental health resources are needed, or groups for which 
certain treatment approaches are most effective. Further, as discussed 
more below, solutions can then be tailored to these subgroups, and 
additional analytic approaches, such as generative AI, can be used to 
generate advice or support tailored to specific subgroups (for example, 
females experiencing postpartum depression versus teenagers having 
thoughts of self-harm).
Further, while multiple methods, such as propensity score match
ing, virtual twins, causal trees/forests and double ML, are available for 
identifying HTEs, new techniques to handle various situations such 
as addressing confounding effects continue to be developed66,67. We 
thus argue it is critical for researchers to continue to apply methods 
with the most promise for accurately identifying heterogeneity and 
confounding effects. Many analytic methods, and, especially, causal 
ML methods61,68,69, deserve serious consideration when developing 
experiments and research designs in the context of mental health.
However, one important issue to consider is that not all HTE meth
ods return the exact same results, meaning there is heterogeneity and 
variation among these methods70,71. Just like the variation of results 
observed here in the articles analyzed, results in this area tend to be 
both situationally specific and also dependent on the type of method 
applied to extracting the heterogeneity. Replication may be difficult, as 
different results may be obtained when using different datasets, even if 
considering similar mental health conditions, and when applying dif
ferent methods (for example, causal forest versus double ML outputs 
may be somewhat different even for the same data and treatment). 
Thus, what is ultimately needed is a better understanding of when 
situationally specific heterogeneity is acceptable versus when more 
generalizable results would be more effective.
Synthetic data. An additional challenge is that not all subgroups are 
always fully represented in the data, at times leading to biased models4. 
For instance, in one of the studies considered here, white females were 
more likely to get treatment for postpartum depression and, thus, 
had higher representation in the data, which could result in bias when 
predicting whether a new mother should be referred to treatment51. 
While it is best to have fully representative data, if that is not possible 
or if underrepresented groups only have limited data available, use of 
synthetic data approaches can be one effective way to increase data 
quantity and quality while waiting for larger and more representative 
datasets. Use of synthetic data is a fascinating area of analytics that 
holds considerable promise for medical and mental health research 
(see ref. 72 for examples, including using synthetic data to model refer
ral rates for those over 65 years of age and longitudinal effects for those 
with type 2 diabetes). AI can now generate close to realistic (hyperre
alistic) data73. For instance, recent efforts in this space include a tool 
called Synthea that can generate realistic synthetic patient records 
and histories74,75. Thus, not only can such synthetic data provide more 
comprehensive input for developing models and understanding how 
to address heterogeneity, but they can also create more opportuni
ties for those who do not have access to constrained data to conduct 
needed research.
However, while synthetic data have a lot of potential, generation 
of such data is a first step. Much more needs to be done in regard to 
validation of the data, assessment for bias and determination of metrics 
to apply to assess the validity of synthetic data, other than just relying 
on distributions of existing data, which may be subject to bias. Thus, 
many opportunities abound for considering how to best incorporate 
synthetic data into analytics-based mental health disparities research.
Incorporation of generative AI. Another limitation discussed above 
is situational and temporal dynamics not yet fully considered in the 
literature. One way to address temporal and situational dynamics in 
disparities, as well as to tailor advice to specific subgroups, such as 
those identified through heterogeneous treatment effect analyses, 
would be to generate mental health advice dynamically, based on indi
vidual and situational characteristics76. One specific way to embrace 
such dynamism is through the use of generative AI, which is the use of 
tools such as ChatGPT and Google Gemini to generate text and images 
from prompts. Advantages include improving image clarity, looking 
for new opportunities for drug development and tailoring advice to 
patients77. Challenges, however, include potential issues with data pri
vacy, especially as more detailed data are fed into such models, as well 
as the digital divide, as some institutions and patients may have more 
access to advanced technologies than others77. Research is needed 
to determine where advantages can be maximized and challenges 
minimized, especially as generative AI in mental health is emerging 
as an underresearched use case78. For instance, generative AI could 
be used in combination with some of the other ideas mentioned here, 
such as for generating synthetic data79, characters for interaction73, 
and improving the scientific discovery process80. Further, generative 
AI could be used to tailor treatments or advice to patients on the basis 
of their individual or situational characteristics77. However, if genera
tive AI is trained on data that have inherent biases, generated content 
may also contain biases81. Therefore, research is needed to assess bias 
throughout the generative AI process, from input data to the process 
of generating data and assessment of the outputs relative to what is 
considered fair and unbiased.
Internet of Things, wearables and AI for mental health treatment. 
Situational and temporal dynamics associated with mental health, as 
discussed as a limitation above, could also be better understood if more 
data sources were considered. Thus, we also propose considerable 
opportunities in this space associated with using data from nontradi
tional sources, such as sensors, activity trackers, providing behavior 
change technique suggestions through AI-based interventions and 
analyzing such data and outcomes with analytics. Data collection via 
Internet of Things and wearables is becoming more prevalent. It is natu
ral to utilize AI to analyze such abundant data to identify characteristics 
such as heart rate, how often patients go out, frequency of exercise and 
whether activity is sufficient during bad weather. However, while such 
data would be helpful, they must be collected along with sociodemo
graphic and social determinant data, as suggested by other studies, 
to determine differences in impacts by individual characteristics and 
situations82,83. For instance, one study82 found that many studies evalu
ating digital health technologies did not consider sociodemographic 
variables such as race/ethnicity or Internet access, which would have 
helped enhance the precision of the studies themselves.
We note that the application of Internet of Things data in mental 
health is not new84. What is new, however, is the use of AI and analytics, 
and even generative AI plus sensor data analysis, for real-time data 
collection and proactive management of mental health issues, which 
may enhance access to help and treatment. Real-time monitoring and 
feedback provisioning can benefit both individual patients and even 
society as a whole if mental health can be improved with noncostly or 
less time-consuming interventions. While mental health profession
als have limited time to actively monitor different patients between 
visits, the development of generative AI has provided a pathway for 
the future synthesis of lengthy and complex data streams85. Further, 
the use of such sensor-based data could help remove bias in treatment, 
as it may help to identify issues that may have been ignored otherwise.
Nature Mental Health
Analysis
https://doi.org/10.1038/s44220-024-00359-2
Translation to practice. Finally, we see the most value occurring in this 
space when complex models, findings and methods can be translated 
to practice. As is beginning to be argued in the literature86,87, moving 
from models to the real world is essential for improving mental health 
outcomes. Specifically, more research is needed into which solutions 
are likely to work best once disparities have been identified, particularly 
where solutions would be more effective if tailored to individual sub
groups. Such research could take the form of experiments or perhaps 
quasi-natural experiments using observational data and comparing 
groups that experience less disparities to those that experience more 
(for example, ref. 88). There are many possibilities here, but the point 
is that research should begin to expand beyond what can be done 
with currently available data and start conducting research on how to 
address underlying disparities that are identified.
However, one issue we observed in the articles we analyzed is that, 
unless the context of the study is focused on a specific demographic 
(for example, postpartum depression for females), the findings are 
often somewhat general, such as finding higher model accuracy when 
including sociodemographic characteristics or being able to better 
identify model bias when including such variables. Thus, one other 
considerable opportunity is to use analytics to identify specific causes, 
and associated solutions, for disparities for specific sociodemographic 
characteristics or intersections.
Methods
To determine the current state of research in this area, and to provide 
a foundation for future research, we selected and analyzed a corpus 
of relevant articles. Such an approach is appropriate when the topic 
of focus is new, emerging and in need of mapping, clarification or 
understanding of both the breadth and depth of the literature89. In 
conducting this analysis, we followed the Preferred Reporting Items 
for Systematic Reviews and Meta-Analyses Scoping Review (PRISMA
ScR) guidelines (Fig. 1)90, which provide a rigorous set of guidelines 
for identifying, screening and selecting articles relevant to a specific 
research question or topic.
Following these guidelines, we developed a protocol, which is 
available at the repository linked to in the ‘Code availability’ section 
later in this Analysis. We selected the following well-regarded indexing 
services: Web of Science, PubMed, IEEE Xplore, PsycInfo and, for follow
up manual searches, Google Scholar. For each of these indexing ser
vices, our initial search conditions were articles within the past ~5 years 
(2017 to July 2023) that contained ‘machine learning’ or ‘artificial intel
ligence’; and ‘mental health’ or ‘behavioral health’ or ‘substance abuse’; 
and also ‘socioeconomic’, ‘sociodemographic’, ‘population-based’, 
‘population related’, ‘dispari*’ or ‘hetergene*’. Only published journal 
articles were included. We note that, while we searched from 2017 to 
July 2023, the first matching and included articles were from 2019, 
making the date range of the final corpus of articles 2019 to July 2023.
We also note that we did not limit our search to a specific type of 
disparity, such as only disparities in algorithmic accuracy. Rather, we 
included articles that applied analytics and also considered any form of 
mental health disparity within analyses including (1) disparities related 
to how outcomes are impacted by group membership (for example, 
impact of race on mental health treatment), (2) disparities related to 
subgroup variation in model performance (for example, impact of 
variables associated with those living in rural areas on model accuracy) 
and (3) disparities in model outcomes related to data or model bias (for 
example, identification of accuracy variations as a result of bias in the 
data the model is trained on). Then, in our results, we identify what 
type(s) of mental health disparities each article considered within the 
analytics applied.
Once the search and selection processes were complete, using 
Jupyter Notebook 6.5.2 and Python 3.8.16, we applied topic mode
ling methods to our corpus of articles, which are ML and DL methods 
that can provide structured results for unstructured data. This topic 
modeling effort resulted in four overall topics representative of the 
articles included, as discussed in Results. Then, within the articles 
assigned to each topic, we qualitatively determined subtopics through 
a combination of assessing the topic probability for each article and 
manual assignment on the basis of full-text review, following a method 
articulated in ref. 17. All articles were assigned to one topic and one 
subtopic.
Reporting summary
Further information on research design is available in the Nature 
Portfolio Reporting Summary linked to this article.
Data availability
The data are journal articles obtained from the searches described 
earlier of Web of Science (https://www.webofscience.com/wos/
woscc/basic-search), PubMed (https://pubmed.ncbi.nlm.nih.gov/), 
IEEE Xeplore (https://ieeexplore.ieee.org/Xplore/home.jsp), PsycInfo 
(https://psycinfo.apa.org) and Google Scholar (https://scholar.google.
com). All articles used in our analyses are referenced in this analysis.
Code availability
Code is available via GitHub at https://github.com/ProfAaronBaird/
JournalArticleRepo/tree/main/NatureMHAnalyticsDisparities.
References
1. 
2. 
3. 
Safran, M. A. et al. Mental health disparities. Am. J. Public Health 
99, 1962–1966 (2009).
Braveman, P. Health disparities and health equity: concepts and 
measurement. Annu. Rev. Public Health 27, 167–194 (2006).
Alang, S. M. Sociodemographic disparities associated with 
perceived causes of unmet need for mental health care. Psychiatr.
Rehab. J. 38, 293–299 (2015).
4. Barr, P. B., Bigdeli, T. B. & Meyers, J. L. Prevalence, comorbidity 
and sociodemographic correlates of psychiatric disorders 
reported in the All of Us Research program. JAMA Psychiatry 79, 
622–628 (2022).
5. 
6. 
7. 
8. 
9. 
Joynt Maddox, K. E. et al. Adjusting for social risk factors impacts 
performance and penalties in the hospital readmissions reduction 
program. Health Serv. Res. 54, 327–336 (2019).
Kleindorfer, D. Sociodemographic groups at risk: race/ethnicity. 
Stroke 40, S75–S78 (2009).
Edwards, A. M. et al. Health disparities among rural individuals 
with mental health conditions: a systematic literature review.  
J. Rural Ment. Health 47, 163 (2023).
Cook, B. L. et al. A review of mental health and mental health care 
disparities research: 2011–2014. Med. Care Res. Rev. 76, 683–710 
(2019).
Ralston, A. L., Andrews, A. R. III & Hope, D. A. Fulfilling the promise 
of mental health technology to reduce public health disparities: 
review and research agenda. Clin. Psychol. Sci. Pract. 26, e12277 
(2019).
10. Brown, A. F. et al. Structural interventions to reduce and eliminate 
health disparities. Am. J. Public Health 109, S72–S78 (2019).
11. 
Barksdale, C. L., Pérez-Stable, E. & Gordon, J. Innovative 
directions to advance mental health disparities research. Am. J. 
Psychiatry 179, 397–401 (2022).
12. Harris, E. CDC report documents disparities in mental health
related ED visits. JAMA 329, 968 (2023).
13. Mohri, M., Rostamizadeh, A. & Talwalkar, A. Foundations of 
Machine Learning 2nd edn (MIT Press, 2018).
14. Graham, S. et al. Artificial intelligence for mental health and 
mental illnesses: an overview. Curr. Psychiatry Rep. 21, 1–18 (2019).
15. Su, C., Xu, Z., Pathak, J. & Wang, F. Deep learning in mental health 
outcome research: a scoping review. Transl. Psychiatry 10, 116 
(2020).
Nature Mental Health
Analysis
https://doi.org/10.1038/s44220-024-00359-2
16. Chen, I. Y., Szolovits, P. & Ghassemi, M. Can AI help reduce 
disparities in general medical and mental health care? AMA J. 
Ethics 21, 167–179 (2019).
17. Baird, A., Xia, Y. & Cheng, Y. Consumer perceptions of telehealth 
for mental health or substance abuse: a Twitter-based topic 
modeling analysis. JAMIA Open 5, ooac028 (2022).
18. Wolfswinkel, J. F., Furtmueller, E. & Wilderom, C. P. Using 
grounded theory as a method for rigorously reviewing literature. 
Eur. J. Inf. Syst. 22, 45–55 (2013).
19. Andersson, S., Bathula, D. R., Iliadis, S. I., Walter, M. & Skalkidou, A. 
Predicting women with depressive symptoms postpartum with 
machine learning methods. Sci. Rep. 11, 7877 (2021).
20. Ueda, M., Watanabe, K. & Sueki, H. Emotional distress 
during COVID-19 by mental health conditions and economic 
vulnerability: retrospective analysis of survey-linked Twitter 
data with a semisupervised machine learning algorithm. J. Med. 
Internet Res. 25, e44965 (2023).
21. Kung, B., Chiang, M., Perera, G., Pritchard, M. & Stewart, R. 
Identifying subtypes of depression in clinician-annotated text: a 
retrospective cohort study. Sci. Rep. 11, 22426 (2021).
22. Keralis, J. M. et al. Health and the built environment in United 
States cities: measuring associations using Google Street view
derived indicators of the built environment. BMC Public Health 
20, 215 (2020).
23. Syed, S. et al. Identifying adverse childhood experiences with 
electronic health records of linked mothers and children in 
England: a multistage development and validation study. Lancet 
Digit. Health 4, e482–e496 (2022).
24. Zhang, X. et al. Identifying the predictors of severe psychological 
distress by auto-machine learning methods. Inform. Med. 
Unlocked 39, 101258 (2023).
25. Herd, T. et al. Individual and social risk and protective factors 
as predictors of trajectories of post-traumatic stress symptoms 
in adolescents. Res. Child Adolesc. Psychopathol. 12, 1739–1751 
(2022).
26. Hueniken, K. et al. Machine learning-based predictive modeling 
of anxiety and depressive symptoms during 8 months of the 
COVID-19 global pandemic: repeated cross-sectional survey 
study. JMIR Mental Health 8, e32876 (2021).
27. Müller, S. R., Chen, X., Peters, H., Chaintreau, A. & Matz, S. C.  
Depression predictions from GPS-based mobility do not 
generalize well to large demographically heterogeneous 
samples. Sci. Rep. 11, 14007 (2021).
28. Shiba, K. et al. Uncovering heterogeneous associations of 
disaster‐related traumatic experiences with subsequent mental 
health problems: a machine learning approach. Psychiatry Clin. 
Neurosci. 76, 97–105 (2022).
29. Jha, I. P., Awasthi, R., Kumar, A., Kumar, V. & Sethi, T. Learning 
the mental health impact of COVID-19 in the United States with 
explainable artificial intelligence: observational study. JMIR 
Mental Health 8, e25097 (2021).
30. Kourou, K. et al. A machine learning-based pipeline for modeling 
medical, socio-demographic, lifestyle and self-reported 
psychological traits as predictors of mental health outcomes 
after breast cancer diagnosis: an initial effort to define resilience 
effects. Comput. Biol. Med. 131, 104266 (2021).
31. Coley, R. Y., Johnson, E., Simon, G. E., Cruz, M. & Shortreed, S. M. 
Racial/ethnic disparities in the performance of prediction models 
for death by suicide after mental health visits. JAMA Psychiatry 78, 
726–734 (2021).
32. Simon, G. E. et al. What health records data are required for 
accurate prediction of suicidal behavior? J. Am. Med. Inform. 
Assoc. 26, 1458–1465 (2019).
33. Goldman-Mellor, S. J., Bhat, H. S., Allen, M. H. & Schoenbaum, M.  
Suicide risk among hospitalized versus discharged deliberate 
self-harm patients: generalized random forest analysis using a 
large claims data set. Am. J. Prevent. Med. 62, 558–566 (2022).
34. Park, H. & Lee, K. Using boosted machine learning to predict 
suicidal ideation by socioeconomic status among adolescents.  
J. Person. Med. 12, 1357 (2022).
35. Jordan, J. T. & McNiel, D. E. Homicide–suicide in the United States: 
moving toward an empirically derived typology. J. Clin. Psychiatry 
82, 28068 (2021).
36. Santamaría-García, H. et al. Uncovering social-contextual and 
individual mental health factors associated with violence via 
computational inference. Patterns 2, 100176 (2021).
37. Qasrawi, R. et al. Machine learning techniques for identifying 
mental health risk factor associated with schoolchildren cognitive 
ability living in politically violent environments. Front. Psychiatry 
14, 1071622 (2023).
38. Marcon, G. et al. Patterns of high-risk drinking among medical 
students: a web-based survey with machine learning. Comput. 
Biol. Med. 136, 104747 (2021).
39. Cox, J. W. et al. Identifying factors associated with opioid 
cessation in a biracial sample using machine learning. Explor. 
Med. 1, 27 (2020).
40. Subbaraman, M. S., Lui, C. K., Karriker-Jaffe, K. J., Greenfield, T. K. & 
Mulia, N. Predictors of alcohol screening quality in a US general 
population sample and subgroups of heavy drinkers. Prevent. 
Med. Rep. 29, 101932 (2022).
41. Kong, Y., Zhou, J., Zheng, Z., Amaro, H. & Guerrero, E. G. Using 
machine learning to advance disparities research: subgroup 
analyses of access to opioid treatment. Health Serv. Res. 57, 
411–421 (2022).
42. Baird, A., Cheng, Y. & Xia, Y. Use of machine learning to examine 
disparities in completion of substance use disorder treatment. 
PLoS ONE 17, e0275054 (2022).
43. Foster, J. C., Taylor, J. M. & Ruberg, S. J. Subgroup identification from 
randomized clinical trial data. Stat. Med. 30, 2867–2880 (2011).
44. Deng, C. et al. Practical guidance on modeling choices for the 
virtual twins method. J. Pharm. Stat. 33, 653–676 (2023).
45. Rajkomar, A., Hardt, M., Howell, M. D., Corrado, G. & Chin, M. H. 
Ensuring fairness in machine learning to advance health equity. 
Ann. Intern. Med. 169, 866–872 (2018).
46. Wang, S. et al. Unpacking the inter- and intra-urban differences 
of the association between health and exposure to heat and 
air quality in Australia using global and local machine learning 
models. Sci. Total Environ. 871, 162005 (2023).
47. Haimson, O. L. Mapping gender transition sentiment patterns via 
social media data: toward decreasing transgender mental health 
disparities. J. Am. Med. Inform. Assoc. 26, 749–758 (2019).
48. Ramezani, N. et al. The relationship between community 
public health, behavioral health service accessibility, and mass 
incarceration. BMC Health Serv. Res. 22, 966 (2022).
49. Castelnovo, A. et al. A clarification of the nuances in the fairness 
metrics landscape. Sci. Rep. 12, 4209 (2022).
50. Thompson, H. M. et al. Bias and fairness assessment of a natural 
language processing opioid misuse classifier: detection and 
mitigation of electronic health record data disadvantages across 
racial subgroups. J. Am. Med. Inform. Assoc. 28, 2393–2403 (2021).
51. Park, Y. et al. Comparison of methods to reduce bias from clinical 
prediction models of postpartum depression. JAMA Netw. Open 
4, e213909 (2021).
52. Park, J., Arunachalam, R., Silenzio, V. & Singh, V. K. Fairness in 
mobile phone-based mental health assessment algorithms: 
exploratory study. JMIR Form. Res. 6, e34366 (2022).
53. Solans Noguero, D., Ramírez-Cifuentes, D., Ríssola, E. A. & 
Freire, A. Gender bias when using artificial intelligence to assess 
anorexia nervosa on social media: data-driven study. J. Med. 
Internet Res. 25, e45184 (2023).
Nature Mental Health
Analysis
https://doi.org/10.1038/s44220-024-00359-2
54. Deferio, J. J., Breitinger, S., Khullar, D., Sheth, A. & Pathak, J. Social 
determinants of health in mental health care and research: a case 
for greater inclusion. J. Am. Med. Inform. Assoc. 26, 895–899 (2019).
55. Cirillo, D. et al. Sex and gender differences and biases in artificial 
intelligence for biomedicine and healthcare. NPJ Digit. Med. 3, 81 
(2020).
56. Perna, G., Alciati, A., Daccò, S., Grassi, M. & Caldirola, D.  
Personalized psychiatry and depression: the role of 
sociodemographic and clinical variables. Psychiatry Investig. 17, 
193 (2020).
57. Walsh, C. G. et al. Stigma, biomarkers, and algorithmic bias: 
recommendations for precision behavioral health with artificial 
intelligence. JAMIA Open 3, 9–15 (2020).
58. Straw, I. & Callison-Burch, C. Artificial intelligence in mental 
health and the biases of language based models. PLoS ONE 15, 
e0240376 (2020).
59. Timmons, A. C. et al. A call to action on assessing and mitigating 
bias in artificial intelligence applications for mental health. 
Perspect. Psychol. Sci. 18, 1062–1096 (2023).
60. Gillett, G., Tomlinson, A., Efthimiou, O. & Cipriani, A. Predicting 
treatment effects in unipolar depression: a meta-review. 
Pharmacol. Ther. 212, 107557 (2020).
61. Wager, S. & Athey, S. Estimation and inference of heterogeneous 
treatment effects using random forests. J. Am. Stat. Assoc. 113, 
1228–1242 (2018).
62. Mehrabi, N., Morstatter, F., Saxena, N., Lerman, K. & Galstyan, A. 
A survey on bias and fairness in machine learning. ACM Comput. 
Surv. 54, 1–35 (2021).
63. Domino, M. E. et al. Do timely mental health services reduce re
incarceration among prison releasees with severe mental illness? 
Health Serv. Res. 54, 592–602 (2019).
64. Kaiser, T. et al. Heterogeneity of treatment effects in trials on psycho
therapy of depression. Clin. Psychol. Sci. Pract. 3, 294–303 (2022).
65. Baird, A., Cheng, Y. & Xia, Y. Determinants of outpatient substance 
use disorder treatment length-of-stay and completion: the case of 
a treatment program in the southeast US. Sci. Rep. 13, 13961 (2023).
66. Bouvier, F. et al. Do machine learning methods lead to similar 
individualized treatment rules? A comparison study on real data. 
Stat. Med. 11, 2043–2061 (2024).
67. Brand, J. E., Xu, J., Koch, B. & Geraldo, P. Uncovering sociological 
effect heterogeneity using tree-based machine learning. Sociol. 
Methodol. 51, 189–223 (2021).
68. Athey, S. & Imbens, G. W. Machine learning methods for 
estimating heterogeneous causal effects. Stat 1050, 1–26 (2015).
69. Cheng, L. et al. Evaluation methods and measures for causal 
learning algorithms. IEEE Trans. Artif. Intell. 3, 924–943 (2022).
70. Cintron, D. W. et al. Heterogeneous treatment effects in social 
policy studies: an assessment of contemporary articles in the 
health and social sciences. Ann. Epidemiol. 70, 79–88 (2022).
71. Schuetze, B. A. & von Hippel, P. How not to fool ourselves about 
heterogeneity of treatment effects. Preprint at OSF https://osf.io/
preprints/psyarxiv/zg8hv (2023).
72. Gonzales, A., Guruswamy, G. & Smith, S. R. Synthetic data in health 
care: a narrative review. PLoS Digit. Health 2, e0000082 (2023).
73. Pataranutaporn, P. et al. AI-generated characters for supporting 
personalized learning and well-being. Nat. Mach. Intell. 3, 
1013–1022 (2021).
74. Walonoski, J. et al. Synthea: an approach, method and 
software mechanism for generating synthetic patients and the 
syntheticelectronic health care record. J. Am. Med. Inform. Assoc. 
25, 230–238 (2018).
75. Begoli, E., Brown, K., Srinivas, S., & Tamang, S. SynthNotes: a 
generator framework for high-volume, high fidelity synthetic 
mental health notes. In Proc. 2018 International Conference on 
Management of Data (IEEE, 2018).
76. Baird, A. & Xia, Y. Precision digital health: a proposed framework 
and future research opportunities. Bus. Inform. Syst. Eng. 66, 
261–271 (2024).
77. Sai, S. et al. Generative AI for transformative healthcare: a 
comprehensive study of emerging models, applications, case 
studies and limitations. IEEE Access 12, 31078–31106 (2024).
78. Abd-Alrazaq, A. A., Rababeh, A., Alajlani, M., Bewick, B. M. & 
Househ, M. Effectiveness and safety of using chatbots to improve 
mental health: systematic review and meta-analysis. J. Med. 
Internet Res. 22, e16021 (2020).
79. Baowaly, M. K., Lin, C.-C., Liu, C.-L. & Chen, K.-T. Synthesizing 
electronic health records using improved generative adversarial 
networks. J. Am. Med. Inform. Assoc. 26, 228–241 (2019).
80. Wang, H. et al. Scientific discovery in the age of artificial 
intelligence. Nature 620, 47–60 (2023).
81. Stokel-Walker, C. & van Noorden, R. The promise and peril of 
generative AI. Nature 614, 214–216 (2023).
82. Coss, N. A. et al. Does clinical research account for diversity in 
deploying digital health technologies? NPJ Digit. Med. 6, 187 (2023).
83. Koinis, L., Mobbs, R. J., Fonseka, R. D. & Natarajan, P. A 
commentary on the potential of smartphones and other wearable 
devices to be used in the identification and monitoring of mental 
illness. Ann. Transl. Med. 10, 1420 (2022).
84. Muhammad Ali, N., Muhammad Ali, M. & Brohi, P. in The Smart 
Cyber Ecosystem for Sustainable Development (eds Kumar, P. et al.) 
235–250 (Wiley, 2021).
85. Cheng, S. W. et al. The now and future of ChatGPT and GPT in 
psychiatry. Psychiatry Clin. Neurosci. 77, 592–596 (2023).
86. Koutsouleris, N., Hauser, T. U., Skvortsova, V. & De Choudhury, M. 
From promise to practice: towards the realisation of AI-informed 
mental health care. Lancet Digit. Health 4, e829–e840 (2022).
87. Hauser, T. U., Skvortsova, V., De Choudhury, M. & Koutsouleris, N.  
The promise of a model-based psychiatry: building 
computational models of mental ill health. Lancet Digit. Health 4, 
e816–e828 (2022).
88. Tordoff, D. M. et al. Mental health outcomes in transgender and 
nonbinary youths receiving gender-affirming care. JAMA Netw. 
Open 5, e220978 (2022).
89. Munn, Z. et al. Systematic review or scoping review? Guidance for 
authors when choosing between a systematic or scoping review 
approach. BMC Med. Res. Method 18, 143 (2018).
90. Tricco, A. C. et al. PRISMA extension for scoping reviews (PRISMA
ScR): checklist and explanation. Ann. Intern. Med. 169, 467–473 
(2018).
Acknowledgements
We appreciate the assistance of L. Davordzi in this project, a graduate 
research assistant completing her Master of Science in Analytics 
(MSA).
Author contributions
A.B. and Y.X. contributed to the design and implementation of the 
research, to the analysis of the data, to the development of final 
results and to the writing of the manuscript.
Competing interests
The authors declare no competing interests.
Additional information
Supplementary information The online version  
contains supplementary material available at  
https://doi.org/10.1038/s44220-024-00359-2.
Correspondence and requests for materials should be addressed to 
Aaron Baird.
Nature Mental Health
Analysis
https://doi.org/10.1038/s44220-024-00359-2
Peer review information Nature Mental Health thanks Debarshi Datta, 
Gayatri Kawlra and Emma Stanley for their contribution to the peer 
review of this work.
Reprints and permissions information is available at  
www.nature.com/reprints.
Publisher’s note Springer Nature remains neutral with regard to 
jurisdictional claims in published maps and institutional affiliations.
Springer Nature or its licensor (e.g. a society or other partner)  
holds exclusive rights to this article under a publishing agreement 
with the author(s) or other rightsholder(s); author self-archiving  
of the accepted manuscript version of this article is solely  
governed by the terms of such publishing agreement and  
applicable law.
© The Author(s), under exclusive licence to Springer Nature America, 
Inc. 2025
Nature Mental Health