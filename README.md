# Phase--3--Project-
## Overview
Our stakeholder is a Vehicle Saftey board from Chicago, they would like us to analyze the crashes that happened in the city from the year 2016-2020 and build models that will contribute to coming up with conclusions as to why this crashes took place and how them as an organization can prevent it in the future. We used an iterative modeling approach in our analysis and incorporated several classification models to see if we could find what crashes were preventable. Our recommendations include investing in driver education for certain age groups and fixing certain road conditions that could cause a crash.

## Business Understanding
Our stakeholder is the Vehicle Safety Board from Chicago that wants to know if they should spend more funding in drivers education or fixing roads. They want to determine whether a crash is preventable and how to allocate funds to limit the number of crashes in order to present it to the Vehicle Safety Board committee of Chicago.It is up to us to give a conlusive analysis in order to make their decision as accurate as possible.


## Data Understanding
Our task is to build an inferential model to find out which crashes were preventable and not. We labeled ‘Preventable’ as crashes that could have easily been avoided. Not following traffic laws and negligent driving would fall under this category. ‘Less Preventable’ are crashes that would require a substantial amount of money, time, and labor to fix. Bad road conditions, vision obscurity, and bad weather conditions would fall under this category as well.

## Data Cleaning

Within the Crashes dataset, we determined that there were a lot of columns that did not contribute any value to the stakeholder's business problem, which is identifying causes of a car crash. Information such as injuries may tell us the severity of the crash, but not a clue on to how the crash occured. Same applies to when the police were notified and time it took place. Columns such as 'INTERSECTION_RELATED_I', 'NOT_RIGHT_OF_WAY_I' may contain relevant information, however they hold too many null values for us to fill, so we decided to drop them. Columns such 'STREET_DIRECTION' and 'ALIGNMENT' tells us the road shape, but since it is not feasible to change any of these roads - meaning they will always have turns and a direction - so we also left these columns from our final dataset.

Before saving our final modeling data to a csv, we ran a heatmap to see if there are any concerning correlations.

![image](https://user-images.githubusercontent.com/91674285/182371251-d950ad4d-41e7-4e07-a699-1752e00740bc.png)

From our heatmap we observed that BAD_WEATHER and BAD_ROAD_CONDITIONS are highly correlated with each other. In order to not overfit our data, we dropped BAD_WEATHER from our dataset due to this reason.


## Data Preparation
We combined 3 different datasets that we found on the City of Chicago website. Those datasets were crashes, people, and vehicles.

Crashes details various contributory causes of the accidents such as traffic devices and road conditions. For this dataset, we dropped all unnecessary columns such as injury severity and street direction. After dropping missing values we could not reasonably populate ourselves, we were left with a dataset of ~950,000 entries. Then, we mapped all the object data types into an int or float 64 to pass into our model. Finally, we created a Target column to label the crashes as Preventable or Less Preventable.

Next, we worked on the people dataset. For the people dataset, we dropped 25 unnecessary columns that we think would not influence the primary contributory cause of an accident. We removed remaining null and unknown values. We then binned by age, and this is where we saw that most of the drivers involved in accidents were between the ages of 20-39. We then converted the remaining features into binary variables. We joined this with the crash dataset and mapped the features into our target.

## Data Modeling
Our target had a distribution of .75 to .25. The 2 categories in the target are 0 for preventable and 1 for not preventable. Because our class balance was 3:1, we did not SMOTE the minority class.
We modeled the data through iterative modeling. We used a logistic regression model as our first simple model.
We graded this model on accuracy score and it resulted in 0.7466465015648959. This was our lowest score. Therefore we used this as our baseline. It was something simple and understandable yet still decent and something we could build on. We also graded this model on precision and got a result of 0.45.

![image](https://user-images.githubusercontent.com/91674285/182030758-760c230c-47f8-4244-b091-7b572e7879a6.png)

For our second model, we created a Decision Tree Classifier that scored slightly better than our simple model. We used a RFE to determine the most important features and iterated with GridSearch to find the best parameters. We found bad road conditions, road defects, traffic device failure, obscured driver vision, and driver error were the most important features. We ran a decision tree with these features as well as all features. Important features: 0.7555023420925494 All features: 0.7563467557291995 We then ran a grid search, which scored roughly the same. We graded this model on precision and got a score of 0.6. When we added RFE to this model, the precision rose to 0.63.

![image](https://user-images.githubusercontent.com/91674285/182030785-77b23182-7753-475c-963f-33069292db24.png)

Lastly, we used a XGBoost classifier with GridSearchCV to find the best model. This model performed very similarly:

![image](https://user-images.githubusercontent.com/91674285/182030835-da16dc6a-f5aa-4284-ba48-284e1391a21c.png)

![image](https://user-images.githubusercontent.com/91674285/182030844-22b57791-994b-4777-82d8-0b2716147e70.png)

## Classification Results
Our best model had an accuracy score of 75%. It had a precision score of 63%. Our precision score is out of all the times the model said it was a less preventable crash, how many times were actually a less preventable crash. Iterative modeling did well to improve precision. By directing the Vehicle Safety Board to certain hotspots of defective roads, we could make a substantial and immediate impact on accidents.

The results of our model indicated that most of the crashes were Preventable. By involving drivers with driver education, we could address some of these preventable crashes. It would be particularly prudent to focus on driver education for ages 20-39. This would be an efficient and effective use of funds for the Vehicle Safety Board of Chicago.

## Recommendation

1. We recommend investing in fixing defective roads. This was the bigger contributor to less preventable crashes, followed by poor visibility, and vehicle defects which is backed by our final model that indicates 75% of crashes in the city were preventable.

2. We discovered in mapping road defects that the northern side of Chicago has more crashes caused by this than the southern side, we recommend that they Vehicle board of Chicago should focus efforts and funds more on the Northern side of the city because crashes are more likely to take place there.

3. We recommend fixing up road defects in northern Chicago. We also suggest a driver education campaign targeting a younger audience between ages 20-39. We could potentially incentivize this cohort. 
 
4. Lastly, we could target specific hot spot areas that are known to be a magnet for crashes.


