# Predicting Employee Turnover
This project aims to use machine learning tools to predict company's employee turnover based on multiple predicting features. Some factors may have contributed to employees' decision to quit the job and a high rate of turnover for a company could have a negative impact since the company has to spent extra time, money, and human resources to initiate recruiting processes that could have been avoided if the company could have somehow managed to improve the working environment so employees are more likely to stay. Finding out top contributing factors to why employees quit their jobs is essential to improving working environment, increasing employee efficiency and satisfaction, and saving company tons of money and resources from investing into endless avoidable extra recruiting processes.

The dataset consists of 10 columns:
- Employee satisfaction level
- The last employee performance evaluation
- Number of projects employees contributed to
- Employee average monthly working hours
- Years employees have been working at the company
- Whether employees have had work accidents
- Whether employees left the comapny
- Whehter employees receved a promotion within the past 5 years
- Deparment employees are in
- Salary of employees

![Fig1](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/7a52b5d3-9922-4746-a4df-5df377dc86aa)

As can be seen, there are a total of 14,999 entries in the table and this project is interested in predicting the 7th variable: Whether employees left the company. Using other variables, this project aims to build a model that can predict whether an employee would quit and therefore improve the top factors that may contribute to such a decision.

Now taking a look at the column statistics:
![Fig2](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/74f5aec0-ca4e-4b24-a517-120fc82f76c9)

All columns appear to be well distributed, not skewed, as evident by the proximity of the mean and median (50%) values of each column, except for the last three columns, where it appears a small fraction of people have experienced work accidents in the past, or received a promotion, or have left.

After additional checks, the dataset does not have null values in columns, which is good, but do have some dupliated rows. After removing those duplications, let's see if the variable we're trying to predict are well balanced: Whether employees left the company
![Fig3](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/0ce98086-3ee0-4a7c-9510-61e1aadee3d9)

Nope. Of the unique rows we have left, 10,000 employees stayed at the companies whereas only 1,991 employees left. This corresponds to 83% vs 17% proportion between the two samples. Not very well balanced, but not too bad so don't really need to downsample or upsample to balance them out.

Now let's look at some plots to see the relationships between some of the variables

First, let's see what a boxplot of number of projects vs average monthly hours can tell us:
![Fig4](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/02a7ec74-6ba4-4ae5-add2-3aeff088c73d)

There appears to be a trend with people working on less project also have lower average monthly hours. Two groups of people left in this plot: those who worked extra hard with a lot of projects and working hours, and those on the other end of the spectrum. The first group likely felt they overworked and the working environment was too stressful and therefore quit. The other group were likely fired because of poor performance. To see that, let's see if there's correlation between working hours and satisfaction, performance evaluation, and promotion.

Scatter plot of working hours vs employee satisfaction:
![Fig5](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/81f1a8af-1ad2-4034-809a-81067f0c3421)

The data shows a lot of unnatural chunks, which is indicative that this is a synthetic dataset rather than a real one. But we could still get some information from this. First and foremost, the group that worked the most hours apparently have the lowest satisfaction level. Unhappiness probably contributed why the left the company. For the other group that left in the bottom left of this plot, even though they have less working hours, it's likely that they underperformed, or felt pressure from peers that worked a lot, and therefore didn't perform well at the company. There's also a group who left that appear to have a high level of satisfaction but also worked for more than 200 hours. This group still quit, which is strange and maybe there're other factors affecting their decisions.

Now take a look at two plots: employee evaluation vs working hours and employee promotion vs working hours.
![Fig6](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/bdcdf721-1f18-48c0-bfc4-c500b22add55)

There doesn't appear to be a strong correlation between long working hours/a lot of contributions and employee performance evaluation. Once again, those who left are those who overperformed and those who underperformed. Are there any reasons why the company doesn't reward people for working long hours? Or does the company know their employees are working long hours? How's the evalution metric calculated?

![Fig7](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/80e6432d-1d54-43b6-a526-397ce8923c0d)

The promotion vs working hour plot tells a bit more. The company doesn't appear to have promoted a lot of people in the past five years and overworked people apparently is not getting the proper reward: very few of them are being promoted. Those who work a lot and didn't get promoted left, which is understandable. Something is wrong with this company's performance evaluation metric and promotion system.

Next, let's see how long employee have worked at the company has anything to do with their satisfaction level:
![Fig8](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/a81bdcf7-7510-4017-a754-bc833fde3dfd)

The majority of the people who quit are those who haven't worked at the company for very long and have very low satisfaction level. They probably are not a fan of the working hours or the company culture and working environment. Fourth year seems very weird where for the people who left, they have extremely low satisfaction level. The company might need to check what's going on when employee steps into their fourth year at the company. There are also groups where employees have high satisfaction level but still quit, possibly because they didn't get a promotion that they thought they deserve as indicated by a previous figure and found a better offer elsewhere. No employee who have worked at the company for a very long time have quit. They are probably managers, directors etc.

Now how about salary distribution vs years at the company?
![Fig9](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/b93b45f6-bc21-4f7b-b756-2a4c7b968acf)

Distribution looks simliar across years working at the company. Don't see a big problem here.

Something important to check: if there's a relationship between number of projects and those who quit. This is kind of similar to the first visualization, but more intuitive:
![Fig10](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/0cd2173c-e97f-4ba0-8e03-0dfddbab621b)

Obviously, no one wants to work for too many projects. The majority of employees worked on the most number of projects quit. It appears the most reasonable number of projects is about 3-5 projects, where the ratio between number of employees stayed and quit are highest.

Is employee turnover a company-wide issue or is something department related?
![Fig11](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/8825718e-b35d-4f70-91f5-ac504e99b315)

Looks like the proportion of those who stayed and left are similar across departments. So employee turnover is not really because some department's poor managing, but really it's a company-wide issue that needs to be address from higher up management level within the company.

Finally, make a heatmap and see if some of the variables are correlated.
![Fig12](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/8b51a8e6-4c9c-43ab-a4bb-935198923fa6)

Employee's decision of leaving is negatively correlated with their level of satisfaction. Performance evluation, number of projects, and average monthyly working hours are all positively correlated. 


Next, create some models to predict whether an employee would quit or not. Before doing so, categorical variables are all converted to numerical representations by assigning them dummy variables with the exception of salary, which is ordianal, so need to be represented by actual numerical values such as 0, 1, and 2 wrt low, medium, and high income.

For any classification tasks, it's worth first trying a basic logistic regression model to see how the model works with the given data.
For logistic regression, it doesn't handle well outliers so these need to be removed. A boxplot can show whether there're any outliers in the data. The number of years an employee has worked at the companies is the variable that need to be treated with because working at the company for too long or too short of a time might not provide an unbiased evaluation.
![Fig13](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/19355c37-2dfa-43d6-918b-ca33f99c40fe)

Indeedn, there are quite a lot of outliers. These outliers are removed if they're 1.5 times the interquartile range above or below the 75% or 25% percentile. A total of 824 outliers were removed.

Using this dataset, we split the train and test set with a 75% and 25% split and make sure we enable the stratify option within the train_test_split function so that both samples are split according to their proportions in the actual dataset.

We train the logistic regression model with a maximum of 500 iterations and the result is actually not that good as shown in the confusion matrix.
![Fig14](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/01094b88-2830-401a-bdb5-adf5c476c5d7)

Ideally we want the number to be the biggest across the diagonal. But the confusion matrix is showing that the model is not doing well predicting employees who would quit. The actual evaluation can be seen with a classification report:

![Fig15](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/d85f34dd-49a0-41ea-8189-1c2cb9267cc3)

  Although the average scores for precision, recall, f1 and accuracy are okay, performance on predicting people that would quit is very low, with precision of 44%, recall of 26%, f1 of 33%. Maybe this model is heavily affected by the small proportion of employee who left in the dataset compared to those who did not leave.


But let's see what trees can do!
Since trees are not quite sensitive to those outliers as logistic regressions do, the original encoded dataset with those outliers are used.

Using the same train test split as before with stratify option on, the data were trained on a Decision Tree Classifier. GridSearchCV was used to fine tune the model with different options of hyperparameters. GridSearchCV was set to do a 10-fold cross validation on the training dataset and AUC score was used to evaluate the best model, along other evaluation metrics such as precision, recall, f1, and accuracy.

The best performing model according to the AUC score actually performed pretty good, much better than logistic regression did.
![Fig16](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/93d77d3a-5151-4091-94d8-4d7973866224)
![Fig17](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/ae8424cf-c3a0-4b8d-9e08-f90e3e937fe9)

The decision tree model is successfully predicting 91.9% of employees who'd quit according to the recall score. With the AUC score being 97.5%. The confusion matrix is showing the same story. Very nice!

Next using the best estimator of this model, the top features that'd lead to employees quit have been identified according to gini importance:
![Fig18](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/26d72e0d-4915-4bc6-990e-bf0be44a5c6b)

Only those with non-zero importance values are displayed. As expected, the top five factors that directly linked to employee turnover are satisfaction level, employee performance evaluation, number of projects, years employees have been working at the company, and average monthly working hours.


Can an ensemble method perform even better? Let's see how a random forest model performs.
Again, using the same train test split, a random forest model was used along with GridSearchCV to fine tune the hyperparameters. 10-fold cross validation was used just like in the decision tree case. Same evaluation metrics were employed.

The random forest model took a while to train. So depending on the training cases and number of hyperparameters that need to be tuned, it might be a good idea to save the training results to a pickle file for future use to avoid wasting time on repeated training. 
The best performing model was selected and the model performs very well:
![Fig19](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/1930bf42-96e6-498e-99e2-580b73eac9ff)

It's marginally better compared to the decision tree model, with AUC score of 98.3% now.
Here's the confusion matrix of the model:
![Fig20](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/d1dbbe9b-2275-4f7e-b7fe-0ccccdd484d8)

Random forest does a slightly better job with the precision score, meaning less false positive are being predicted now. Recall performance is similar to decision tree.

And here's the top features that contributed to employee leaving according to the random forest model:
![Fig21](https://github.com/zhexingli/PredictingEmployeeTurnover/assets/18060088/e72ce2da-24ae-426a-93a3-ac8fcb5836c2)

Overall, the top five factors are the same as what decision tree model predicted, except with a slightly different order. In this case, salary is another factor that joined this ranking along with other features that are of non-zero importance, but negligible compared to the top five or six factors we are seeing here.


Since the random forest model performs slightly better, this was picked as the champion model and its performance on the test set was evaluated:
Precision: 98.7%, Recall: 92.8%, F1: 95.7%, Accuracy: 98.6%, AUC: 96.3%.
The performance is similar to what was seen for the training and cross validation set so it's safe to say the model is not overfitting nor underfitting and is good to be implemented for future uses!

### Conclusions:
- Random forest model was the best performing model out of the three that were tested and should probably be uesd for future implementations.
- Although random forest is the best model overall, it's only slightly better than the decision tree model. Considering decision tree training only took a split of a second whereas random forest training took almost an hour on a 6-core 12-thread computer, the company may want to opt for the decision tree model in this case if it needs to save time and resources.
- Depending on what the company actually cares about, may want to retrain the models to focus on recall, or precision instead.
- From the model results and visualization presented earlier, the company 100% needs to rethink about its company culture and working environment and focus on how to retain their employee and increase the employee happiness.
- Overworked employee don't appear to be well compensated, maybe the company should consider giving them more promotions. This may be directly related to their satisfaction level.
- Limit the number of hours and number of projects an employee can work on to maintain their good work-life balance. The company working environment maybe too stressful for some by working too long per week. Ideally limit the number of projects each employee can take to 3-5.
- If employees have to work extra hours, make sure they are well compensated for those extra hours.
- The company needs to investigate why there are so many employees that are dissatisfied with the company at the fourth year of their time at the company.
- Other than the abovementioend points, company may want to invest in more activities company wide to boost the overall employee satisfaction level.
