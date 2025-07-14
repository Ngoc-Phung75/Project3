SOCIAL ANXIETY affects millions of people worldwide.


This project aims to :
    - Build regression models to predict social anxiety levels
    - Identify key risk factors contributing to anxiety
    - Visualize correlations and psychological behavior trends

I will use machine learning in order to reach my objectives.

Dataset source : Kaggle : https://www.kaggle.com/datasets/natezhang123/social-anxiety-dataset

Dataset description :
    - 10,000+ samples representing individuals with varying levels of social anxiety, ranging from mild to severe
    - Features : Demographics, Lifestyle, Health & Mental Indicators, Mental Health History, Life Events
    - Target : Anxiety levels (1-10)

Here the link to my presentation :
https://www.canva.com/design/DAGnuL4J5JQ/inopvqOiQga4f4dAv3d0Rw/edit?utm_content=DAGnuL4J5JQ&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton


Outcomes :
Linear Regression - MSE: 0.21, R²: 0.52
Gradient Boosting - MSE: 0.18, R2: 0.59
Random Forest - MSE: 0.18, R2: 0.60
XGBoost - MSE: 0.20, R2: 0.55
LightGBM - MSE: 0.17, R2: 0.61


Scores are poor. I want to train with 2 datasets : 
- the first one where I will drop features with the lowest correlation with my target
- the second one where I will group indicators into 4 main categories : demographics, health, life events and lifestyle.


Dropping columns ['Occupation', 'Gender_Female', 'Gender_Male', 'Gender_Other', 'Family_History_of_Anxiety', 'Dizziness', 'Medication', 'Smoking', 'Recent_Major_Life_Event']) doesn't improve the predictions. Worst, two models -Random Forest and Linear Regression- are less performant.

Linear Regression - MSE: 0.21, R2: 0.51
Gradient Boosting - MSE: 0.18, R2: 0.59
Random Forest - MSE: 0.18, R2: 0.58
XGBoost - MSE: 0.20, R2: 0.55
LightGBM - MSE: 0.17, R2: 0.61


Then, I tried another method by checking if groupping indicators into categories would improve accuracy:
Demographics : Gender_Female, Gender_Male, Gender_Other, Age
Health : Sweating_Level, Sleep, Breathing_Rate, Heart_Rate, Stress_Level, Therapy_Session, Dizziness
Life events : Family_History_of_Anxiety, Recent_Major_Life_Event
Lifestyle : Caffeine_Intake, Alcohol_Consumption, Diet_Quality, Quality, Smoking, Medication


    'Sleep': 'Health',
    'Breathing_Rate': 'Health',
    'Heart_Rate': 'Health',
    'Stress_Level': 'Health',
    'Therapy_Session': 'Health',
    'Sweating_Level': 'Health',
    'Dizziness': 'Health',

    'Physical_Activity': 'Lifestyle',
    'Caffeine_Intake': 'Lifestyle',
    'Alcohol_Consumption': 'Lifestyle',
    'Diet_Quality': 'Lifestyle',
    'Smoking': 'Lifestyle',
    'Medication': 'Lifestyle',

    'Family_History_of_Anxiety': 'Lifestyle_events',
    'Recent_Major_Life_Event': 'Lifestyle_events'

    
I plotted the features groups and also searched for the top features contributing to their category.

Top features in group 'Demographics':
Age              0.068472
Gender_Female    0.002641
Gender_Male      0.002600

Top features in group 'Health':
Stress_Level       0.553861
Therapy_Session    0.401288
Sleep              0.290244

Top features in group 'Lifestyle':
Caffeine_Intake      0.294186
Physical_Activity    0.229608
Diet_Quality         0.177101

Top features in group 'Lifestyle_events':
Family_History_of_Anxiety    0.176907
Recent_Major_Life_Event      0.070107

Comments :
- In "Health" category, the top 3 features beat all the top 3 features of the other categories.
- Since 'Demographics' has a weak bond with my target, I decided to drop this category and pursue with the 3 other categories.


After training the 3 categories, I evaluated their performance :
KNN : MSE: 0.1997409090909091, R² score: 0.5351682104226608
Random Forest - MSE: 0.18, R2: 0.58
Gradient Boosting - MSE: 0.18, R2: 0.58
Linear Regression - MSE: 0.22, R2: 0.49
XGBoost - MSE: 0.20, R2: 0.54
LightGBM - MSE: 0.17, R2: 0.59

=> R2 scores are not better. 


** Key findings :
To improve accuracy, the models need all the features, even those which have a weak correlation with the target.













