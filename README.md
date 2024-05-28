# Chicago Traffic Crashes Project
### Determining the primary causes of traffic accidents

Joel Mott
Flatiron School
joel.mott8@gmail.com
May 2024

![jake-blucker-ZGnC2gOvzKw-unsplash](https://github.com/joeldmott/chicago_auto_accidents_project/assets/51928528/6c3f0bd2-94ff-4354-aa33-20d2e51ad2ee)
Photo by <a href="https://unsplash.com/@jakeblucker?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Jake Blucker</a> on <a href="https://unsplash.com/photos/time-lapse-photography-of-road-ZGnC2gOvzKw?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>

### business inquiry

The goal of this project is to determine the primary causes of traffic accidents in the City of Chicago. While [similar efforts](https://www.chicago.gov/city/en/sites/complete-streets-chicago/home/traffic-safety/vehicle-size-and-speed.html) have shed light on crashes resulting in injuries and/or fatalities, this project takes **a broader perspective by including non-injury accidents in order to identify wide-ranging trends in traffic safety issues.** The stakeholder in this scenario would be the [Chicago Department of Transportation (CDOT)](https://www.chicago.gov/city/en/depts/cdot.html).

Recent CDOT studies on Chicago traffic safety have found that [most accidents involve reckless driving and/or a disregarding traffic laws & signals](https://www.chicago.gov/city/en/sites/complete-streets-chicago/home/traffic-safety/reckless-driving.html). Subsequently, this project focuses on those features of the data which correlate with **accidents that are more avoidable (and therefore more actionable) than those that are less so.**

### dataset

This project's raw dataset originates from the [City of Chicago's website](https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if/about_data), where it is updated daily. I downloaded the data on May 1st, 2024 and [uploaded that snapshot to Kaggle](https://www.kaggle.com/datasets/joelmott/chicago-traffic-crashes-may-2024) for this project.

This dataset consists of three seperate csv files: one for general crash information, one for the people involved in each crash, and one for each vehicle. When merged, the resulting dataset contains over 146 columns and 3.8 million records tied to over 837,000 different traffic crashes.

### data preparation & modeling

While some data preprocessing and feature elimination took place in my [data engineering notebook](https://github.com/joeldmott/chicago_auto_accidents_project/blob/main/data_engineering_notebook.ipynb) through EDA and domain knowledge, further feature trimming through modeling is done in the [project notebook](https://github.com/joeldmott/chicago_auto_accidents_project/blob/main/project_notebook.ipynb), which is available to run for reproducibility on [Google Colab](https://colab.research.google.com/drive/1uUvI_7ytHNdIKEZjJs73YlK-Y0rZjljM#scrollTo=HOPrEI3idQmK), where it links to the aforementioned data snapshot. 

Since this project focuses more on the data's *features*, the overall emphasis is on **model interpretability** as opposed to prediction accuracy. Specifically, while I use some black-box modeling techniques (a Scikit-Learn Random Forest as well as Principal Component Analysis) to help trim the features down, the ultimate predicting models are white-box methods that are easier for a non-technical stakeholder to interpret.

I first attempted a StatsModels Logistic Regression model, but it struggled to find a linear relationship to this more complex data. However, it did help with further feature reduction. Ultimately, a Scikit-Learn Decision Tree model was able to make better predictions while still showing which columns tend to contibute to reckless & negligent driving in a more interpretable fashion.

### evaluation

As seen below, the final model's perfomance results are more so in the 'acceptable' range than 'great'. While they would likely be higher through use of a more complex model, this white-box approach allows for a more interpretable look at the data features which should be targeted to help improve traffic safety with a broader approach.

These finding were validated through an 80/20 train-test-split before preprocessing.

![final model results](https://github.com/joeldmott/chicago_auto_accidents_project/assets/51928528/4f5a1d8b-0797-42e7-a82c-2f4df9ac3fc5)

By the end of the modeling process, three features stand out as being the most important when it comes to predicting whether an accident was avoidable:

- location (on busier streets)
- age (drivers between 23-40 are most likely to have an avoidable crash)
- time of day (heavier commute times are riskier)

While these finding aren't exactly groundbreaking, they do help isolate issues for general traffic safety, resulting in the following three recommendations:

1. Ads focused on heavy traffic safety for drivers between 23-40
2. Road sign/traffic signal studies in Chicago’s middle/downtown 
3. Safety PSAs over the radio during commute times
