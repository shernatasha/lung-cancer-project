![Facebook Cover 851x315 px (2)](https://user-images.githubusercontent.com/58491399/101442228-bde1a700-38cf-11eb-90dd-724620f00c7a.jpeg)

## Index
**1.** [Abstract](https://github.com/shernatasha/projects/blob/master/README.md#abstract) \
**2.** [Introduction](https://github.com/shernatasha/projects/blob/master/README.md#introduction) \
**3.** [Data Description](https://github.com/shernatasha/projects/blob/master/README.md#datadescription) \
**4.** [Methods](https://github.com/shernatasha/projects/blob/master/README.md#methods) \
**5.** [Results](https://github.com/shernatasha/projects/blob/master/README.md#results) \
**6.** [Conclusion](https://github.com/shernatasha/projects/blob/master/README.md#conclusion)\
**7.** [Appendix](https://github.com/shernatasha/projects/blob/master/README.md#appendix) 

## Abstract
It is well-known that some common causes of cancer are diet, physical activity, radiation and infections. But, is there a possible link between cancer and basic demographic factors such as race, income and age? In this study we will be taking a look at lung cancer data from various United States counties and seeing if there is any significance between these demographics and lung cancer cases. We did this by fitting two linear models, one with incidence rates and one with death rates to see which factors were significant in each. Our findings concluded that those with higher education and income had lower incidence and death rates but also that race played a significant role in both our models. In our report we will delve deeper into how we conducted our analysis as well as a more detailed interpretation of our results.

## Introduction 
In the USA cancer is the second leading cause of death, right behind heart disease. It affects an average of 1.8 million people each year. With no guaranteed way to prevent one from getting cancer, and still no “true” cure, more people are getting concerned. One reason we are still unable to find a perfect cure for cancer is due to the fact that there are so many types. Therefore, it is important to note that the data we are working with only contains information about lung cancer. Majority of lung cancer cases are caused by smoking or other activities that induce risk to the respiratory system. This includes exposure to smoke, radon gas, or radiation therapy. According to the [American Cancer Society](https://www.cancer.org/latest-news/facts-and-figures-2020.html?fbclid=IwAR0B6h3tzgNV1YByus6WBd5sYXvUkiYRMruYBJyIl7G3TVXGUNNeAsvu0Yg), from 1991 to 2017 lung cancer death rates have been steadily declining due to the decreasing levels of smoking rates. Thus, the general purpose of this study is to see what route we could take to stay on the trend of declining lung cancer rates. This includes studying the relationship between the variables we are given in our dataset and the incidence/death rates.

For our first question of interest we are looking into which variables affect incident and death rates the most in general. For example, with a quick glance at our data we have several expectations for our results. The first one being that poverty should affect the death rate more so than the incidence rates. The reason is that people who are living in poverty may be able to detect their symptoms of lung cancer early on, but may not be able to afford the proper treatment. Another expectation we have is that private healthcare should affect the incidence rate more while public coverage affects death cases more. We believe this is due to the fact that if you have private healthcare, it is more likely for you to be diagnosed early on with cancer. Meanwhile with public healthcare, you may be diagnosed later on and thus, not have the resources for treatment.

This leads to our second area of interest, which is looking more specifically at each individual county. Since the dataset we are given has information sorted by each county, we kept it as is instead of combining data from the same states together. This is to prevent any loss of information from aggregating the numbers. We will look into the top and bottom three counties for both the incidence and death rate. From this we are going to analyze what variables play a role in differentiating the top and bottom three counties. 

Therefore, in this study we will be investigating the results for the following two questions:
   1. Which variables contribute more to death and more to incident numbers? Why?
   2. What are the top three counties with the highest and lowest incidence and death rate? Do they have any specific attributes?
         - This allow us to showcase our findings from question 1 by taking examples straight from our data 

## Data	Description 

Our dataset contains data about lung cancer demographics relating to US counties collected between 2010 - 2016.

**Description of Variables** \
**deathRate:** Average deaths per 100,000 people (a) \
**avgAnnCount:** Average number of cases diagnosed annually (a) \
**incidenceRate:** Average number of cases per 100,000 people(a) \
**medianIncome:** Median income per US county (b) \
**popEst2015:** Population of the US county (b) \
**povertyPercent:** Percentage of county population in poverty (b) \
**binnedInc:** Median income per capita (b) \
**MedianAge:** Median age of county residents (b) \
**Geography:** County name (b) \
**PctHS25_Over:** Percentage of county residents ages 25 and over with their highest education attained being a high school diploma (b) \
**PctBachDeg25_Over:** Percentage of county residents ages 25 and over with their highest education attained being a bachelor's degree (b) \
**PctEmployed16_Over:** Percentage of county residents ages 16 and over who are employed (b) \
**PctUnemployed16_Over:** Percentage of county residents ages 16 and over who are unemployed (b) \
**PctPrivateCoverageAlone:** Percentage of county residents with private health coverage alone (no public assistance) (b) \
**PctPublicCoverageAlone:** Percentage of county residents with government-provided health coverage alone (b) \
**PctWhite:** Percentage of county residents who identify as White (b) \
**PctBlack:** Percentage of county residents who identify as Black (b) \
**PctAsian:** Percentage of county residents who identify as Asian (b) \
**PctOtherRace:** Percentage of county residents who identify in a category which is not White, Black, or Asian (b) \
> The variables with (a) were collected between 2010 - 2016 and the variables with (b) were collected from the 2013 US Census

A fair amount of cleaning was done to our dataset as we had quite a few observations with missing values. We removed 714 out of the 3047 observations our raw dataset had. We also decided to remove some variables in our dataset as we felt we had a large number of predictors and were worried about variables such as “Percentage of Married Households” and “Household Size” adding noise to our model. Another important effect of removing extra variables was that we were able to avoid the risk of overfitting our model which can happen when there are not only too many predictors present but also predictors which would not be good indicators. An example being what does a high correlation between the number of lung cancer deaths and percentage of married households really tell us about our data. We know that an overfit model can cause our regression model to become tailored to the number of predictors we include. It will fit the extra “noise” in our dataset and reflect our sample instead of fitting the overall population. 

Since we choose to analyze which predictors were more significant for death versus incidence we choose incidence rate as the dependent for one model and the death rate for our other model. The reason we chose the rate values instead of the raw numbers (total cases and total deaths) was because the rates take population size into account. Since we are comparing the cancer cases and deaths from different U.S. counties we need to take into consideration that each county will differ with population size. If we had just used the total number of cases and total number of deaths, this would make it very difficult for us to draw any reasonable conclusions as the larger counties would have higher numbers for both cases and deaths. Thus making our analysis biased towards the larger counties. Therefore by using the rates we are able to appropriately compare the cancer statistics between the different counties while taking their sizes into account. 

Before we begin fitting models and drawing conclusions from our summary statistics, it is important to determine whether our model has any relationships which are worth investigating. We decided to create pairs plots for both our sets of data (death and incidence) to take a look at the variable relations.

Incidence Data            |  Death Data
:-------------------------:|:-------------------------:
![Incidence Model](https://user-images.githubusercontent.com/58491399/101408468-4d1b9a00-3891-11eb-9804-4a4458aab4bc.png)  | ![Death Model](https://user-images.githubusercontent.com/58491399/101408736-b1d6f480-3891-11eb-811f-54e29259696a.png)
> Click on the plots to expand the picture 

**Figure 1: Pairs Plots for Our Two Models**

We can see in both of our plots that we definitely see relationships between many of the variables, especially between our respective dependent and independent variables. Therefore we would like to move forward and begin fitting models to further investigate these relationships.

For our additional data point we decided to choose Washington DC for our county because although it is part of the US, it is not an official state. For the values of the variables, we found information regarding lung cancer data collected in 2020 for Washington DC from the [American Cancer Society](https://cancerstatisticscenter.cancer.org/#!/state/District%20of%20Columbia) and combined this with US 2020 census information from [DC Health Matters](https://www.dchealthmatters.org/index.php?module=demographicdata&controller=index&action=index). We chose these values since we were interested to see how data from a different year would compare to our dataset. We know that lung cancer cases have not been increasing significantly over the past few years but the population of the U.S. has been on a slow rise. Therefore we were interested in how a slow rising population as well as a steady cancer rate would compare to the rest of our data. We expected this point to be an outlier as with the U.S. population growing over the years since our data was collected, you would expect the number of cases to also rise. 

## Methods 
> In this section we will be describing the methods used to perform our analysis.

After assessing the relations between our variables we began our model fitting. We started off the models with the same independent variables except for one: 

- avgAnnCount 
- avgDeathsPerYear 
- medIncome 
- popEst2015 
- povertyPercent 
- MedianAge 
- PctPrivateCoverageAlone 
- PctPublicCoverageAlone 
- PctWhite 
- PctBlack 
- PctAsian 
- PctOtherRace 
- PctHS25_Over 
- PctBachDeg25_Over 
- PctUnemployed16_Over 
> The incidence model did not include avgDeathsPerYear as we felt it did not make sense to use this variable as a predictor for the number of cases 

We fit both models with all the independent variables and perform a thorough analysis including taking a look at the residuals. We start off with the full model to ensure that we are starting off with a functioning model before we start to do any computations and perform any analysis. We also want to ensure that the underlying assumptions are met such as constant variance and normally distributed errors.

Then to ensure we had the best performing subset of parameters from our dataset we decided to use not only stepwise regression but also backward elimination. We know that although it is best to keep as many predictors as possible to ensure that we are able to find all and any factors which relate to our dependent variable it is also important to not have a large amount of predictors as the variance of our dependent variables increase with the number of predictors. Therefore, with the large number of predictors we had in our data, we believed that variable selection would help us to eliminate any noise created by extra predictors as well as identify any multicollinearity. The reason for us choosing to perform two variable selection methods was that so we can compare the models we got out of both and see if there were any differences in model fit. This would ensure that we would be going forward with a model we would feel confident using to answer our questions about this data. 

After we found a subset of predictors we felt confident in analyzing, our next step was to take a look at the residuals again to make sure there are no significant changes as well as assess the normality assumptions again. Then we wanted to check whether our variable selection had taken care of any multicollinearity present in our model so we first plotted the correlation matrices for both our models. If we saw any highly correlated variables in our plot we would use the variance inflation factors to take a closer look. The VIFs measure the collinearity between the respective beta’s of the regressors and VIF values larger than 10 identify serious multicollinearity problems. It is important to identify any multicollinearity present in a linear model as it can cause sensitive regression coefficients. 

Next we look for high leverage and influential points. Points with high leverage are important to identify as although they do not affect our regression coefficients they will affect our model summary statistics which is important for us as we are looking to see which predictors are more significant for death versus incidence. Influential points are important to identify as they do have an impact on our regression coefficients by pulling our regression line away from the majority and towards itself. 

We will identify leverage points by computing our hat matrix and taking a look at the diagonal values. The diagonal values are than compared to **2p/n** where **p** is the number of regressors and **n** is the number of observations. We compare our diagonals to this **2p/n** value as we consider any diagonal larger than this distant enough from the majority of our data to be considered a leverage point. Once we identify these leverage points we will then check to see if any are influential. We consider observations that have not only large diagonal values in the hat matrix but also a large Cook’s distance to be influential. 

Once we had identified our influential observations we needed to take a closer look to determine what should be done with them. Is there a reason these observations are influential? Would removing the observations and refitting our model give us a better fitting regression line? Is the data point valid or was there a mistake made in data collection? These questions need to be asked before discarding what could be valuable observations. 

One of the last steps we would like to conduct is model validation. Before we interpreted our findings and began to answer our questions about the data we assessed the validity of the model. This is to not only ensure that we as the creators had created a model which would accurately operate in our analysis but also be useful for others to conduct their own analysis’. Since we are unable to collect new data for our dataset we decided to perform model validation by cross validation. Here we split our data into two sets, one for estimating and the other for predicting. We use the estimating set to build our regression model and our prediction set to assess the predictability of the estimation set. To test how well our estimation set predicts values we compute the R<sup>2</sup>, the root mean square prediction error (RMSPE) and the mean absolute prediction error (MAPE). We know the R<sup>2</sup> tells us how well the model fits, the RMSPE tells us how spread out our residuals are and the MAPE tells us how accurate our predictions are. 

Finally, once we have a model we believe is valid and feel confident using we can take a look at the summary of our models and begin performing our analysis. Here, we will do a residual analysis on our now completed models, take a look at the summary statistics, conduct a hypothesis test to see if there is a significant linear relationship between at least one of the predictors and the response and be able to interpret our findings.

## Results 

We started by assessing our residual plots of our full incidence model to assure that our constant variance assumption and normality assumptions were met. 

Normal Q-Q            |  Residuals vs. Fitted
:-------------------------:|:-------------------------:
![130775558_2820270421588786_8754615875456693759_n](https://user-images.githubusercontent.com/58491399/101423002-e2785780-38ac-11eb-8c9c-d6e547bd5814.png) | ![129712940_712835399359695_2629368532734819007_n](https://user-images.githubusercontent.com/58491399/101423216-6b8f8e80-38ad-11eb-8b5c-fd14799d3b02.png)

> Click on the plots to expand the picture 

**Figure 2: Residual Analysis of Full Incidence Model**

We see from the Normal Q-Q plot that  the residuals do adequately meet the normality assumption. The deviation on the left side of the plot suggests a slight negative skew to the distribution of the residuals but they are not large enough to be of concern. We also see a few points on the right side of the graph which could be potential influential points or of high leverage. We will look closer at these after our variable selection to see if they still may be of concern. Next we see in our Residuals vs. Fitted plot that our model seems to be adequate to the linear relationship assumption. We have a very even distribution of points around zero which is a good sign of evenly distributed residuals. Though we see our data is slightly to the right of the graph, since it is not an obvious deviation we will not read too much into it. If we had a few more data points whose fitted values were less than 450, we would see the variation even out. Similarly we analyzed the Scale - Location plot and again saw a similar outcome to the Residuals vs. Fitted plot where we had points evenly distributed about the horizontal line with a slight skew to the right of the graph. Thus this plot confirms that our constant variance assumption is met. Lastly, the Residuals vs. Leverage plot showed that we did not have any high leverage points to be concerned about. 

Similarly with our full death model we see that:

Normal Q-Q            |  Residuals vs. Fitted
:-------------------------:|:-------------------------:
![Full Death - Normality](https://user-images.githubusercontent.com/58491399/101427023-f58e2600-38b2-11eb-9abb-adede829b521.png) | ![Full Death - Residuals vs  Fitted](https://user-images.githubusercontent.com/58491399/101427095-19ea0280-38b3-11eb-9790-ef7d51f1f5be.png)


> Click on the plots to expand the picture 

**Figure 3: Residual Analysis of Full Death Model**

Our Normal Q-Q plot has some slight deviations than the incidence model but this could be due to our death data containing more extreme values then our incidence data. Overall the plot looks to be lightly tailed as the majority of the data fits normally for the most part except for a few observations which may be potential influences. Then looking at the Residuals vs.  Fitted plot we see a very even spread of data with a few extra points on the right side, but nothing to be worried about. We have our data evenly spread about the zero line which shows that the linear relationship assumption has been met. We see the same three observations singled out on both the Normal Q-Q and Residuals vs. Fitted plots meaning that it will be important to take a closer look at these. Next, we analyzed the Scale-Location plot and again saw our points evenly distributed among the horizontal line which confirms that our constant variance assumption has been met. Lastly we saw on our Residuals vs. Leverage Plot that there are no high leverage points to be concerned about.

Now that we have established that our model meets all the necessary multiple regression assumptions we will perform variable selection to try and find the best performing subset of regressors. As mentioned in the methods section of our report, we decided to use two different variable selection methods: stepwise regression and backward elimination. After compiling both of our codes our result was that both methods of variable selection gave us the exact model. These are our newly fitted regression equations:

Death Model            |  Incidence Model
:-------------------------:|:-------------------------:
![DeathModel](https://user-images.githubusercontent.com/58491399/101448907-b1b01680-38dc-11eb-925f-6a4785df715d.png) | ![IncidenceModel](https://user-images.githubusercontent.com/58491399/101448994-d4422f80-38dc-11eb-9c1d-fcb189b045ef.png)
> Click on the plots to expand the picture 

**Figure 4: Models Produced From Variable Selection**

We can see with these newly fitted models that before performing any hypothesis tests and looking for significant predictors there are already some differences in predictors for both of our models. Though we see many similarities between the two our incidence model seems to focus more on race than the death model. Once we replotted our residual plots for both the new death and incidence model we saw that there were no significant changes in the plots and found that removing some predictors still kept our normality and linear regression assumptions the same. Therefore we moved on to checking for any multicollinearity in these new models.

We decided to use a correlation matrix to first visualize any presence of multicollinearity before computing our variance inflation factors. 

Death Model            |  Incidence Model
:-------------------------:|:-------------------------:
![Screenshot (1584)](https://user-images.githubusercontent.com/58491399/101449205-3438d600-38dd-11eb-8ec1-1bf13d3c5abd.png) | ![Screenshot (1585)](https://user-images.githubusercontent.com/58491399/101449306-634f4780-38dd-11eb-9a16-4d0980c1f3e8.png)
> Click on the plots to expand the picture 

**Figure 5: Correlation Matrices for Both Models**

From these visualizations we can see that our death model has some high correlation coefficients which should be investigated whereas we do not see anything alarming in our incidence model. We checked our VIFs for the incidence model to ensure we had not missed anything and indeed we had low VIF values for all our predictors. We then took a look at the variance inflation factors of our death model to further investigate the high coefficient values. 

<p align="center">
  <img width="585" alt="vifdeathmodel" src="https://user-images.githubusercontent.com/58402986/101544241-2f663780-395a-11eb-829d-709fb8a9b59f.PNG">
</p>

**Figure 6: VIFs for Our Death Model**

We see here that as we expected there are some very high VIFs that we would have expected to see based on our correlation matrices. The variables avgDeathsPerYear and popEst2015 have VIFs quite larger than 10 which makes them serious indicators of multicollinearity. Therefore to increase the validity of our prediction equation and also decrease the sensitivity of our regression coefficients we removed both these predictors from our model. After refitting our model we took a look at our VIFs again and they had all decreased to values less than five which was a good indication that the two variables we removed were causing some multicollinearity issues within our model. We also noticed from our new model that our adjusted R<sup>2</sup> had increased meaning we now had a better fitting model. 

Next we choose to evaluate whether our models have any influential or high leverage points which are of concern. We saw in our residual plots that there were some points which had been identified as potential influences, here we will examine them closer. 

Death Model Leverage       |  Incidence Model Leverage
:-------------------------:|:-------------------------:
<img width="649" alt="deathleverage" src="https://user-images.githubusercontent.com/58402986/101543432-1315cb00-3959-11eb-90e1-0f086af8ac76.PNG"> | <img width="663" alt="incidenceleverage" src="https://user-images.githubusercontent.com/58402986/101543360-faa5b080-3958-11eb-8b34-b0ecb34a186b.PNG">
> Click on the image to expand the picture 

**Figure 7: Death and Incidence Model Leverage Code**

The first thing we noticed when computing our influential points was that the new data point which we introduced was not considered high leverage nor influential. This was surprising to us as we had believed that introducing a new point which contained more recent data would come out as influential when compared to the rest of our dataset. We determined that it could simply be that the lung cancer rates over the years have not increased as much as we believed them to. We took a closer look at comparing our new datapoint to the dataset and noticed that although the values for population, number of cases and a few other variables were much larger than the rest of our data, the proportion of cases were the same. Meaning that although we had more people, more cases and more death, our rate variables were still proportionate to the rest of our data thus indicating that we did not have any significant increases in incidence nor death since our data set had been collected.

The figure above shows our code for finding the points with high leverage. Upon further investigation of these points, most of them either have a really low or high incidence/death rate. For example, Hudspeth County has a really low incidence rate of 214.8, which is also the county with the third lowest incidence rate. While it does also have a low population estimate of 3379, this number is still in the 105th place from the bottom up in terms of the population. This means that there are 104 counties with a lower population number. If we take 104 minus the two counties that have a lower incidence rate than Hudspeth, we are left with 102 counties that not only have a lower population but also have a higher incidence rate. Thus we believe this is one of the reasons for these points to have high leverage. However, after calculating the Cook’s distance we discovered that these points with high leverage are not influential points. Their Cook’s distance was lower than 1, and after creating a model without these points we receive a lower adjusted R<sup>2</sup>. Therefore, we chose to keep our stepwise regression model as is without removing any points.

Before moving on the interpretation of our findings, we will discuss the results of our model validation. For our incidence model we found that the R<sup>2</sup> for the estimation model was 0.1396 which was slightly lower than our fitted model. Our RMSPE was 50.57 and our MAPE was 37.73. For our death model, the cross validation gave us an R<sup>2</sup> of 0.40, a RMSPE of 21.91 and a MAPE of 16.60. Right away we see that death values are more desirable but not necessarily better. We see high values in our root mean squared prediction error as well as our mean absolute prediction error and a relatively low R<sup>2</sup> value. Though this indicates that our model does not fit our observed data very well we can take a look at our coefficients below in Figure 8 and see that they have small standards of error and most even proved to be very significant against our alpha value of 0.05. We also saw from our residual plots that our models met all the necessary assumptions, showing that we did not have a biased model.

If we had studied delivery times for mail or housing prices vs size we would expect a much higher adjusted R<sup>2</sup> and lower error values. However, since we are looking at humans in our study we expect there to be a lot of variation and high errors. We know that humans are inherently harder to predict unlike physical processes.  Thus we are not surprised to see that we have a low adjusted R<sup>2</sup> and high errors. Looking at these values we can conclude to the reader that this model should not be used for prediction. Even though the intention was to simply detect which predictors were more significant for death vs incidence it is important to mention this incase our model would like to be used for any further analysis.

## Conclusion 

Death Model Summary       |  Incidence Model Summary
:-------------------------:|:-------------------------:
<img width="522" alt="deathsum" src="https://user-images.githubusercontent.com/58402986/101566923-bc25eb00-3984-11eb-8273-acbe1547cdde.PNG"> | <img width="492" alt="incidencesum" src="https://user-images.githubusercontent.com/58402986/101566867-9dbfef80-3984-11eb-88e6-f54be959d97d.PNG">
> Click on the image to expand the picture 

**Figure 8: Death and Incidence Model Summary**

This is the summary of our death and incidence model after performing stepwise regression. Right away we notice that both models have very small p-values which allows us to reject our null hypothesis and conclude that at least one regressor is significant in terms of our dependent variable. For our death model, we have six variables that are no longer included in our model: avgDeathsPerYear, medIncome, MedianAge, PctEmployed16_Over, PctBlack, and PctAsian. While for our incidence model, we have three variables: PctBachDeg25_Over, PctEmployed16_Over, and PctAsians.

To address our questions of interest, we will go through several of the variables and discuss the impact it has on our models. Starting off with avgAnnCount, we see it has more effect on the incidence model which makes sense since this variable is the number of reported cases annually. However, the variable medIncome affects the death model a lot more than the other. The reason for this is presumably because treatment for cancer costs more than a diagnosis. Therefore, one’s income level has a more important role in life or death. As we have mentioned previously, one of our expectations was for povertyPercent to affect the death model more, and we see that this is indeed the case. The reasoning for this could be that poverty doesn't necessarily have an impact on being diagnosed but more so on dying. We know that cancer treatments can be very expensive and since those in poverty are less likely to be able to not afford private health care and maybe not even be able to pay public health care bills they are not able to recieve the proper care and treatment. 

We see that PctHS25_Over and PctUnemployed16_Over are the only two educational variables that remain in the model after performing stepwise regression. We believe this is due to the fact that the other two variables are more positive or on the side of a higher level of education. Therefore the more educated one is, the easier it is for one to take preventative measures. Under this assumption, it becomes more clear that having a lower level of education results in a higher impact on our incidence model. Another reason is that if we assume an “incident” of lung cancer is recorded when one is diagnosed with it, then the age range of our variable will have very low numbers of incidents. Our variables are 16+ or 25+ but if we assume that the age range goes up to 60 for instance, then that is still very young because most incidences occur at age 70. The same reasoning applies to our death model. We noticed that PctEmployed16_Over has a high p-value of 0.9061 here. If we let the age range for PctEmployed16_Over be from 16-40, then it will not be surprising if the number of incidents are low. Therefore, this variable doesn’t affect our death model. While the same logic could apply for PctUnemployment16_Over, we believe that this does have an impact on our death model because this variable already represents a situation that is not as desirable.

The US does not have universal health care and so citizens can either choose between private or public health coverage. While private health care is more expensive, it is more flexible and so the majority end up choosing this option. It is no surprise that private and public health care appears to affect both our models. However, we do see that private health care affects our models more than public health coverage since the p-values are lower. We believe this is because more people tend to opt for private coverage only. The p-values for the public and private coverage in the incidence model is also slightly smaller than the ones in our death model. The difference does not seem to be significant but this could be because of how these insurances cover the diagnostic portion more so than the full treatment. 
 
Moving on to the variables about races in our model, we see that PctAsians is not included in both the incidence and death model. Our adjusted R<sup>2</sup> does not change when we try removing this variable and so this variable does not affect our model. One reason for this could be the fact that the percentage of asians in the US is relatively small and looking at our given dataset, PctAsians has the highest number of zeros with 194 total. This could mean that PctAsian is more inaccurate compared to the other percentages or perhaps the numbers were so low it got rounded to 0. On the other hand, PctWhite tends to be really high for the majority of the counties. This aligns with what we see in our model summaries; which is really low p-values for PctWhite meaning it does have a significant effect. PctBlack has the second highest number of percentages after PctWhite, which is why we believe it affects our incidence model. However, we noticed it does not affect our death model and a reason for this could be because most numbers for PctBlack are fairly small when the death rate is high. We also have some missing values for this variable as well which totals up to 72 entries. We were surprised to see that PctOtherRace in both our models, however we agree that this does make sense because the US is a huge and diverse country. Thus, it would be rather strange to only see one race in our model.


To further support the effect of the variables we have mentioned, we will answer the second question by looking at our sorted data:


![highestincidencerate](https://user-images.githubusercontent.com/58402986/101435758-c03d0480-38c1-11eb-86c6-7713a9750c9f.jpg)
**Figure 9: Top 3 Counties with the Highest Incidence Rate** 


![lowestincidencerate](https://user-images.githubusercontent.com/58402986/101436959-0a26ea00-38c4-11eb-9d82-51663c512a17.jpg)
**Figure 10: Bottom 3 Counties with the Lowest Incidence Rate** 


![highestdeathrate](https://user-images.githubusercontent.com/58402986/101437038-37739800-38c4-11eb-8c25-3b4bf56a70f7.jpg)
**Figure 11: Top 3 Counties with the Highest Death Rate** 


![lowestdeathrate](https://user-images.githubusercontent.com/58402986/101437096-52460c80-38c4-11eb-8bc8-129116adf3e9.jpg)
**Figure 12: Bottom 3 Counties with the Lowest Death Rate**

An interesting point is that Aleutians West Census Area has a very low poverty percentage, which is also correlated with the high median income. Our expectation was that it is more likely for the county to have a low incidence rate if the majority of its people have the resources to keep themselves healthy. However, the same goes for being able to afford cigarettes for example. This could explain why counties with high incidence rates also have a high median income, and similar poverty percentages as counties with low incidence rates.

Poverty percentage appears to be lower in the counties with the lowest incidence rate, however the difference does not appear to be significant. The county with the highest incidence rate: Williamsburg City has a lower poverty percentage than Hudspeth County and Presidio County. This aligns with our stepwise regression model as we did not include poverty percentage since we believed it does not make a significant difference. Meanwhile in our death model, we see that the poverty percentage has a bigger impact. The numbers do appear to be much smaller for the counties with the lowest death rate, while they are higher for the counties with the highest death rate.

We have concluded that people with higher education, higher income, and private health insurance are most likely to have lower incidence and/or death rates. We made our conclusion based on our multiple regression analysis of our lung cancer data set. It is interesting to note that we can see that there are many demographic factors which have an impact not only on cancer deaths but also cancer cases. Thus we can see that health, radiation, infections and smoking are not the only factors which can affect developing lung cancer. Though our model is specific to lung cancer we can make the assumption that all forms of cancer have some demographic factors which relate to it. Therefore we need to better understand which factors relate to the majority of cancers to be able to make more general conclusions.



## Appendix 

1. Our R code is listed in two seperate files on our repository: \
        - deathlm.R contains our code for the death model which we computed \
        - incidencelm.R contains our code for the incidence model which we computed
        
2. The dataset we used to conduct our analysis can be found saved on our page as the cancer_reg.csv file \
        - As mentioned in the data description of our report we did not use everything within this dataset \
        - We also did not create this file, this data set was found at the following link: [OLS Regression Challenge](https://data.world/nrippner/ols-regression-challenge)   
