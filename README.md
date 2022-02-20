# Statistical-Linear-Model
# Predicting State GDP and Political Affiliation Using Renewable Energy Data 


# ABSTRACT
This project explores how one sector of the U.S. economy can impact broader economic and societal outcomes. With an increasing focus on the energy production and consumption, as well heightened support for a global transition to renewable energy sources, we focus on how the U.S. energy sector affects high-level variables. We use the source of electricity produced in a state and that state's total energy consumption to predict total state GDP, as well as political affiliation. Here we construct three models to explore these questions. First, we find that total energy consumption and a state's total GDP are highly correlated, suggesting unsurprisingly that wealthier states consume more energy. Second, we construct a model with GDP as a response and electricity production source and total energy consumption as predictors, finding that solar and nuclear are significant predictors, along with total consumption. Finally, we construct a model with percentage of votes in a state going to Republican or Democrat candiates in the U.S. 2020 presidential election as a response, finding that nuclear, coal, natural gas, petroleum, geothermal and wind are significant predictors. We generally conclude that energy can have a moderate level of predictive impact on broader economic and political shifts; however, our modeling is limited by lack of information, collinearity, and nonuniform distributions of electricity generation type in U.S. states. 


# INTRODUCTION

The objective of this project is to analyze how one sector of the U.S. economy (i.e. energy) can influence broader societal outcomes, such as economic growth and elections. In this case, we are interested in building models based on energy supply (for electricity) in each state, to see what role the energy sector may have on a broader outcome. This report addresses the following questions:

(1) Is electricity production type correlated with total GDP per state?
(2) Which sources of electricity production is most significant in predicting GDP?
(3) In addition to energy production, is total energy consumption a significant predictor for total GDP per state?
(4) Is electricity production type correlated with state-level political affiliation?

Our project is broken into three components. First, we analyze total GDP with total energy consumption by state as a predictor to see if total energy consumption is relevant to total GDP. 

Then, we aim to investigate the relationship between energy production source and total energy consumption against and total GDP. This allows us to compare both energy production and comsumption in the context of our societal variables of interest. Our energy data comes from the National Energy Institute, providing the percentage of electricity that is produced in a given state by each source, such as solar, wind, coal, natural gas, etc. Our GDP data comes from Statistia Research Department. 

Finally, we are interested in the relationship between energy production and political affiliation. In this case, we use the percentage of voters who voted Republican vs. Democrat in the 2020 presidential race as a response, and electric energy production types and total energy consumption as predictors. 


# DATA

Our data consists of four datasets, merged by U.S. state:
(1) We use total GDP by state in 2020 (in billions of US dollars) with data collected by the Statista Research Department. This is our primary societal-level economic response variable. It is worth noting that GDP is only one metric of general economic trends, comprised of multiple sectors beyond our focus of energy. Additionally, this project does not adjust for the impact on GDP caused by COVID-19 during the 2020 fiscal year. 
https://www.statista.com/statistics/248023/us-gross-domestic-product-gdp-by-state/

(2) We use electricity production data from the National Energy Institute (NEI) in 2020 as our primary source of predictor variables. Data is organized by percent of total electricity produced in the fifty U.S. states and the District of Columbia by a subset of electricity production types. In this case we use nuclear, solar, coal, natural gas, hydroelectric, petroleum, wind, geothermal, and biomass/other. We note that electricity production is only one component of the energy sector, and that in many states, not all of these sectors have significant percentages of the total electricity production. However, electricity is of greater proximity to residences and businesses, and thus could have a higher impact on outside economic outcomes. 
 https://www.nei.org/resources/statistics/state-electricity-generation-fuel-shares 

(3) In addition to energy production, we also explore total energy consumption (in British thermal units) by state in 2018  (the latest this data was avaialable). Although we do not have data for consumption by electricity sector, as in the production dataset, we are still able to explore the distinction between production and consumption. 
https://neo.ne.gov/programs/stats/inf/120.htm 

(4) To measure political affiliation in the U.S. with one response variable, we use data from the U.S. 2020 presidential election. Here we use data collected by Cook Political Report, exploring percentages of votes in a given state that went to the Republican or Democratic candidate. We do not explore independent candidates because of the small proportion of votes they comprise. We note that percentage of votes for each candidate is only one representation of political affiliation. 
 https://www.census.gov/newsroom/press-releases/2021/2020-presidential-election-voting-and-registration-tables-now-available.html 

To efficiently conduct our analysis, we merged these data sets into a single data frame called "fulldata", which we invoke throughout our analysis:

# RESULTS AND DISCUSSION
There was substantial collinearity present in our predictor variables, with some interesting relationships. COAL and NATURAL GAS were negatively correlated, which could make sense if a state is dependent on fracking (a process that extracts natural gas) but also coal production, which in some places are in direct competition with one another. Alternatively, this relationship may occur because coal and natural gas tend to hold higher proportions of electricity consumption than other forms of electricity production. Therefore, an increase or decrease in either may correlate an increase or decrease overall in electricity consumption by state.

While collinearity was mitigated through stepwise regression methods, we cannot be sure that the most useful predictors weren't inadvertently taken out through the stepwise algorithm. We used stepwise regression as an easy way to remove non-significant predictor variables for all of our models, but this was done at the cost of potentially missing important predictors and created smaller models than is potentially ideal. We note that Faraway discourages the use of stepwise and backwards regression except in the case of simple model comparisons or "highly structured heirarchical [sic] models" (Faraway 153), and so while we use ANOVA to determine how much faith we can have in our stepwise models, we cannot say with confidence that our stepwise models are the best variable reduction option. For future research, we recommend utilizing shrinkage methods more fully, such as PCR (which we did incorporate for our political affiliation model) and PLS.

We found that the model with log(GDP) as a response and both electricity energy production and consumption variables as predictors had the best predictive power, compared to either production or consumption variables by themselves. However, since the response is log-transformed, this makes direct interpretation of our model more difficult.ease.

For our GDP model, we found that Texas is a problematic observation, since it is a leverage point, influential point, and outlier. This is because the state consumes *by far* the most energy relative to its GDP. After removing Texas from our GDP model post-stepwise regression, the model fit was far better, and the p-values of the predictors changed substantially. However, unlike datasets that involve distinct datapoints that do not interact with each other in a larger system (such as patients, a collection of chemical isomers, or types of tea), we wanted to make conclusions about not only US states in isolate, but also the United States as a whole. Thus, we were hesitant to remove Texas permanently from our dataset, even if we did sacrifice achieving the best fit for our model.

Even after transforming GDP, our residuals were still not random. This is why we implemented the Huber regression method, so that the influence of extreme observations (such as Texas!) non-random errors . Interestingly, even though Washington (observation # 48) does not show up on any of our diagnostic plots, the Huber method significantly downweights this observation. This may be because Washington uses no solar energy for electricity but uses the most hydroelectric power (66%) out of any state, and has unusually high GDP for a state (618B, vs the median of 242B).

For our political affiliation model, were able to conclude that electricity production type can have moderate predictive power for political affiliation in a given state. In particular, we find that predictions of Republican vote percentages are better than expected and are in fact more accurate than our GDP model, to our surprise. It is interesting that total consumption is not a significant predictor, since it implies that even highly Democratic states (such as California) use significant amounts of energy, calling attention to the fact that energy (over)use is a bipartisan issue. 

More so than in our GDP model, since more energy production predictors are included, collinearity is more of a problem, and so it is unclear if we can meaningfully interpret the coefficient values of our ordinary least squares model (even though in this case, our response was not log-transformed). Still, as a proof of concept analysis to test the influence of the energy sector on political outcomes, we see that an arguably significant relationship exists between political affiliation and types of energy production.


# CONCLUSION

A main limitation of this analysis stemmed from a lack of data availability. While finding total GDP breakdowns and 2020 election outcomes by US state was straightforward, we were unable to find energy production data that was not limited merely to electricity energy production by percent shares. This data set also combined energy outputs attributed to biomass *and* other forms of energy production into one variable ("BIOMASS_OTHER"), which made interpretation of the importance of this variable somewhat more difficult, since in fact a few states (such as Maine) actually produce a significant portion of their energy through biomass burning. Furthermore, we were only able to find *total* energy consumption data, and only for the year 2018--all our other data sets were from 2020. Datasets that broke down energy consumption by energy type (renewable/non-renewable etc.) eluded us, even after extensive searching on the Department of Energy website. This issue might be overcome in future research through compiling individual state data sets that may not otherwise be easily available in a 51-state/DC data set.

A more conceptual limitation of our extension model is that political affiliation trends don't vary primarily by state, but rather by population density (in other words, cities are overwhelmingly Democratic, while rural areas are primarily Republican). Thus, future research might include similar predictor/response variables but broken down to the county-level, in order to make more meaningful conclusions about relationships between political outcomes and energy use/production.

In conclusion, nuclear and solar production along with total energy consumption ended up being the most significant variables for predicting log(total GDP) of US states. Predictive power of our model was fairly high, but removing outlier states, especially Texas, improved our model drastically. Some influential observations such as Washington were hidden and only 'discovered' through the Huber method that was implemented as an error mitigation technique. For our political affiliation model, energy production variables ended up being important predictors, while energy consumption was not, and ended up having surprising predictive power, albeit with significant collinearity problems. 

