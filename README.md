# Predicting State GDP and Political Affiliation With Multivariate Statistical Linear Model

## Abstract
This report explores how one sector of the U.S. economy can impact broader economic and societal outcomes. With an increasing focus on the energy production and consumption, as well as heightened support for a global transition to renewable energy sources, we focus on how the U.S, energy sector affects a state's total GDP and political affiliations. We concluded that renewable energy consumption/production has a moderate level of predictive impact on broader economic and political shifts.

<img width="899" alt="Screen Shot 2022-08-22 at 4 15 04 PM" src="https://user-images.githubusercontent.com/89557209/186035166-4a55f5f8-5429-46e0-ba45-2a85fb7b5b03.png">

## Research Methods
We built  various linear models with energy production and consumption in each state as independent variables and total annual GDP and 2020 election votes as response variables. We aim to answer following questions:

(1) Is electricity production type correlated with total GDP per state?
(2) Which sources of electricity production is most significant in predicting GDP?
(3) In addition to energy production, is total energy consumption a significant predictor for total GDP per state?
(4) Is electricity production type correlated with state-level political affiliation?

Our project is broken into three components. First, we analyze total GDP with total energy consumption by state as a predictor to see if total energy consumption is relevant to total GDP. 

Then, we aim to investigate the relationship between energy production source and total energy consumption against and total GDP. This allows us to compare both energy production and comsumption in the context of our societal variables of interest. Our energy data comes from the National Energy Institute, providing the percentage of electricity that is produced in a given state by each source, such as solar, wind, coal, natural gas, etc. Our GDP data comes from Statistia Research Department. 

Finally, we are interested in the relationship between energy production and political affiliation. In this case, we use the percentage of voters who voted Republican vs. Democrat in the 2020 presidential race as a response, and electric energy production types and total energy consumption as predictors. 

## Data Collection & Exploratory Analysis

Our data consists of four datasets, merged by U.S. state:
(1) We use total GDP by state in 2020 (in billions of US dollars) with data collected by the Statista Research Department. This is our primary societal-level economic response variable. It is worth noting that GDP is only one metric of general economic trends, comprised of multiple sectors beyond our focus of energy. Since this project does not adjust for the impact on GDP caused by COVID-19 during the 2020 fiscal year, we recognize that the impact of covid as a confounding variable that needs to be considered in future research.
https://www.statista.com/statistics/248023/us-gross-domestic-product-gdp-by-state/ 
<img width="633" alt="Screen Shot 2022-08-22 at 12 56 06 PM" src="https://user-images.githubusercontent.com/89557209/186007507-5ebc809e-ca92-4747-96f3-697e97c28385.png">

(2) We use electricity production data from the National Energy Institute (NEI) in 2020 as our primary source of predictor variables. Data is organized by percent of total electricity produced in the fifty U.S. states and the District of Columbia by a subset of electricity production types. In this case we use nuclear, solar, coal, natural gas, hydroelectric, petroleum, wind, geothermal, and biomass/other. We note that electricity production is only one component of the energy sector, and that in many states, not all of these sectors have significant percentages of the total electricity production. However, electricity is of greater proximity to residences and businesses, and thus could have a higher impact on outside economic outcomes. 
 https://www.nei.org/resources/statistics/state-electricity-generation-fuel-shares 
 <img width="635" alt="Screen Shot 2022-08-22 at 12 44 55 PM" src="https://user-images.githubusercontent.com/89557209/186005581-f8467d73-0161-44f8-84d8-c417e3e411e0.png">
<img width="629" alt="Screen Shot 2022-08-22 at 12 46 26 PM" src="https://user-images.githubusercontent.com/89557209/186005847-3352b546-c0de-40b9-bd03-0827d9ec9cd8.png">

(3) In addition to energy production, we also explore total energy consumption (in British thermal units) by state in 2018  (the latest this data was avaialable). Although we do not have data for consumption by electricity sector, as in the production dataset, we are still able to explore the distinction between production and consumption. 
https://neo.ne.gov/programs/stats/inf/120.htm 
<img width="639" alt="Screen Shot 2022-08-22 at 12 47 08 PM" src="https://user-images.githubusercontent.com/89557209/186005972-1bfabf97-d9b5-4c0b-a0ee-83e2690ff4f4.png">

(4) To measure political affiliation in the U.S. with one response variable, we use data from the U.S. 2020 presidential election. Here we use data collected by Cook Political Report, exploring percentages of votes in a given state that went to the Republican or Democratic candidate. We do not explore independent candidates because of the small proportion of votes they comprise. We note that percentage of votes for each candidate is only one representation of political affiliation. 
 https://www.census.gov/newsroom/press-releases/2021/2020-presidential-election-voting-and-registration-tables-now-available.html 
 
 + edited (Aug 2022) I also added a dataset to include metrics to rank states by green energy production to do a further analysis: https://www.consumeraffairs.com/solar-energy/greenest-states-in-us.html#greenest-states-ranked

## Discussions 
### Addressing Collinearity in total GDP ~ energy production + consumption model:
There was substantial collinearity present in our predictor variables, with some interesting relationships. COAL and NATURAL GAS were negatively correlated to the total energy production, which could make sense if a state is dependent on fracking (a process that extracts natural gas) but also coal production, which in some places are in direct competition with one another. Alternatively, this relationship may occur because coal and natural gas tend to hold higher proportions of electricity consumption than other forms of electricity production. Therefore, an increase or decrease in either may correlate an increase or decrease overall in electricity consumption by state. 

<img width="541" alt="Screen Shot 2022-08-22 at 1 51 26 PM" src="https://user-images.githubusercontent.com/89557209/186016546-36d7e5f2-286c-4853-b0fb-4912a2ad085d.png">

While collinearity was mitigated through stepwise regression methods, we cannot be sure that the most useful predictors weren't inadvertently taken out through the stepwise algorithm. We used stepwise regression as an easy way to remove non-significant predictor variables for all of our models, but this was done at the cost of potentially missing important predictors and created smaller models than is potentially ideal. We note that Faraway discourages the use of stepwise and backwards regression except in the case of simple model comparisons or "highly structured heirarchical [sic] models" (Faraway 153), and so while we use ANOVA to determine how much faith we can have in our stepwise models, we cannot say with confidence that our stepwise models are the best variable reduction option. For future research, we recommend utilizing shrinkage methods more fully, such as PCR (which we did incorporate for our political affiliation model) and PLS.

We found that the model with log(GDP) as a response and both electricity energy production and consumption variables as predictors had the best predictive power, compared to either production or consumption variables by themselves. 

<img width="505" alt="Screen Shot 2022-08-22 at 1 53 21 PM" src="https://user-images.githubusercontent.com/89557209/186016847-9241c47b-7d7c-4499-9a9a-0456d89fa13d.png">

We also conducted ANOVA analysis between our models–one with all predictors and the reduced model– to confirm that the reduced model does as well as the bigger model. And 95% confidence intervals for the stepped model also validates out reduced model:
<img width="571" alt="Screen Shot 2022-08-22 at 1 56 30 PM" src="https://user-images.githubusercontent.com/89557209/186017381-d39e2b4d-f807-47d0-8bc7-01e5e29c2065.png">
<img width="325" alt="Screen Shot 2022-08-22 at 1 57 16 PM" src="https://user-images.githubusercontent.com/89557209/186017514-7422c01a-f894-4d42-83bf-55414b6d1095.png">

What our model suggests is that an increase in total energy consumption leads to an increase in the total GDP, which intuitively makes sense. Yet, what really caught our attention is the fact that for every one percent increase in net electricity produced by nuclear and/or solar energy, there is an increase in the total GDP. In the context of our electricity production dataset, which measures the percentage of net electricity generated with the given production method, our linear model suggests that shifting towards nuclear and solar energy production type generated a greater increase in the total GDP produced by state.

### Addressing outliers in total GDP ~ energy production + consumption model::
For our GDP model, we found that Texas is a problematic observation, since it is a leverage point, influential point, and outlier. This is because Texas consumes *by far* the most energy relative to its GDP. After removing Texas from our GDP model post-stepwise regression, the model fit was far better, and the p-values of the predictors changed substantially. 
<img width="621" alt="Screen Shot 2022-08-22 at 1 59 13 PM" src="https://user-images.githubusercontent.com/89557209/186017862-91fd7de6-3879-46ef-a6b0-da1d0f5b8de7.png">
*Note: state No.44 is Texas

However, unlike datasets that involve distinct datapoints that do not interact with each other in a larger system (such as patients, a collection of chemical isomers, or types of tea), we wanted to make conclusions about not only US states in isolate, but also the United States as a whole. Thus, we were hesitant to remove Texas permanently from our dataset, even if we did sacrifice achieving the best fit for our model.

Even after transforming GDP, our residuals were still not random. This is why we implemented the Huber regression method, so that the influence of extreme observations (such as Texas!) non-random errors . Interestingly, even though Washington (observation # 48) does not show up on any of our diagnostic plots, the Huber method significantly downweights this observation. This may be because Washington uses no solar energy for electricity but uses the most hydroelectric power (66%) out of any state, and has unusually high GDP for a state (618B, vs the median of 242B).

<img width="591" alt="Screen Shot 2022-08-22 at 2 01 53 PM" src="https://user-images.githubusercontent.com/89557209/186018375-c85fde67-9365-4261-a8b5-a588432377e4.png">

### Discussions for political affiliation ~ energy production:
For our political affiliation model, were able to conclude that electricity production type can have moderate predictive power for political affiliation in a given state. In particular, we find that predictions of Republican vote percentages are better than expected and are in fact more accurate than our GDP model, to our surprise. It is interesting that total consumption is not a significant predictor, since it implies that even highly Democratic states (such as California) use significant amounts of energy, calling attention to the fact that energy (over)use is a bipartisan issue. 

<img width="514" alt="Screen Shot 2022-08-22 at 2 04 26 PM" src="https://user-images.githubusercontent.com/89557209/186018803-c786d8e6-364e-4ea7-ac4f-307df94f08ac.png">

More so than in our GDP model, since more energy production predictors are included, collinearity is more of a problem, and so it is unclear if we can meaningfully interpret the coefficient values of our ordinary least squares model (even though in this case, our response was not log-transformed). Still, as a proof of concept analysis to test the influence of the energy sector on political outcomes, we see that an arguably significant relationship exists between political affiliation and types of energy production.

## Conclusion
A main limitation of this analysis stemmed from a lack of data availability. While finding total GDP breakdowns and 2020 election outcomes by US state was straightforward, we were unable to find energy production data that was not limited merely to electricity energy production by percent shares. This data set also combined energy outputs attributed to biomass *and* other forms of energy production into one variable ("BIOMASS_OTHER"), which made interpretation of the importance of this variable somewhat more difficult, since in fact a few states (such as Maine) actually produce a significant portion of their energy through biomass burning. Furthermore, we were only able to find *total* energy consumption data, and only for the year 2018--all our other data sets were from 2020. Datasets that broke down energy consumption by energy type (renewable/non-renewable etc.) eluded us, even after extensive searching on the Department of Energy website. This issue might be overcome in future research through compiling individual state data sets that may not otherwise be easily available in a 51-state/DC data set.

A more conceptual limitation of our extension model is that political affiliation trends don't vary primarily by state, but rather by population density (in other words, cities are overwhelmingly Democratic, while rural areas are primarily Republican). Thus, future research might include similar predictor/response variables but broken down to the county-level, in order to make more meaningful conclusions about relationships between political outcomes and energy use/production.

In conclusion, nuclear and solar production along with total energy consumption ended up being the most significant variables for predicting log(total GDP) of US states. Predictive power of our model was fairly high, but removing outlier states, especially Texas, improved our model drastically. Some influential observations such as Washington were hidden and only 'discovered' through the Huber method that was implemented as an error mitigation technique. For our political affiliation model, energy production variables ended up being important predictors, while energy consumption was not, and ended up having surprising predictive power, albeit with significant collinearity problems. 

