# Project 3: Mental Health Awareness and NLP

## Problem Statement

Many people who are diagnosed with one neurological condition or mental illness discover at some point that they also have one or more other conditions, or that they got the wrong diagnosis in the first place. This confusion has implications for prognosis, treatment, medication, and accomodations at school or work.

The following models aim to classify posts from subreddits for several overlapping mental health conditions (ADHD, anxiety, depression, and autism), with the goal of helping people understand their brains (or their loved ones’ brains) better. These models could point patients in the right direction when seeking professional help, or could even be used by clinicians to supplement evaluation.

---

## Data Dictionary

| Field       | Data Type | Description                                                                                         |
|-------------|-----------|-----------------------------------------------------------------------------------------------------|
| compound    | float     | overall score from VADER sentiment analysis                                                         |
| created_UTC | int       | time stamp of when the post was initially created on subreddit <br>used in data collection only |
| length      | int       | character count of the post after cleaning                                       |
| neg         | float     | score for negative-oriented sentiment                                                               |
| neu         | float     | score for neutral sentiment                                                                         |
| pos         | float     | score for positive-oriented sentiment                                                               |
| selftext    | str       | content of the post                                                                                 |
| subreddit   | int       | Anxiety = 0<br>ADHD = 1<br>Depression = 2<br>Autism = 3                                             |
| title       | str       | title of the post                                                                                   |
| word count  | int       | number of words in the post, after cleaning                                       |

---

## Methodology
- Reddit API, PushShift, was used to collect around 15,000 text-based posts from each of four sub-reddits:
  - ADHD
  - Anxiety
  - Depression
  - Aspergers (Autism)
- Sentiment analysis incorporated into two of the models
- CountVectorizer optimized via a grid search
- Three models:
  - Multinomial Naive Bayes
  - Random Forest Classifier
  - Gradient Boost Classifier

---

## Analysis & Conclusions

Overall, all three models had very similar performance, but I would recommend the GBoost model based on its superior accuracy on test data. 

| Model                     | Train Accuracy | Test Accuracy | Best Parameters                                                                                            |
|---------------------------|---------------|----------------|------------------------------------------------------------------------------------------------------------|
| Multinomial Naive Bayes   | 85%           | 75%            | max_df: 0.9<br>max_features: 5000<br>min_df: 3<br>ngram_range: (1, 2)                                      |
| Random Forest Classifier  | 83%           | 76%            | max_depth: 19<br>max_features: 'auto'<br>min_samples_leaf: 2<br>min_samples_split: 4<br>n_estimators: 1000 |
| Gradient Boost Classifier | 84%           | 77%            | learning rate: 1<br>max_depth: 2<br>n_estimators: 50                                                       |

I could imagine this tool being available on self-improvement or mental wellness websites, just as you can find screening questionaires for various conditions all over the internet. People who are curious or struggling could submit a sample journal entry and immediately get a few suggestions of illnesses or conditions to learn more about. The mental healthcare system in the US is generally overburdened, so patient self-advocacy is crucial. This tool could allow a patient to bring up their concerns with their doctor and get the right referrals. 

Clinicians and mental health professionals could also use this tool in conjunction with other long-standing tools in a variety of situations. It could be part of their initial evaluation of a new patient. For a patient who has been in treatment for a while and is still struggling, it could help suggest new areas to explore -- maybe they have only been getting treatment for some of their problems.  
