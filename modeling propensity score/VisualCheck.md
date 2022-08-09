Modeling Propensity Scores
Returning to our student sleep data, we are interested in the effect of meditation on sleep. It seems intuitive that people with high levels of stress might struggle with sleep AND might be less likely to engage in coping mechanisms such as meditation. We can use propensity scores to model this interaction.

Propensity scores reflect the probability of being in the treatment group, as opposed to the control group, given a set of characteristics. Because this probability corresponds to a binary outcome—either being in the treatment group or the control group—we can model the propensity scores using logistic regression. The outcome of the regression will predict whether or not an individual is in the treatment group. It will use potential confounding variables as predictors.

With regards to our sleep data, the propensity score should model the probability of practicing meditation based on the other characteristics in the data. Let’s start with a propensity score model with the meditate variable as the outcome and the stress variable as a predictor.

The glm() function in R makes modeling propensity scores via logistic regression simple. By default, the glm() function fits a linear regression model, so we need to modify the family argument to specify that the treatment group variable is binary. To do this, we set the family argument to "binomial":

prop_model <- glm(
  formula = meditate ~ stress, #formula
  data = sleep_data, #dataset
  family = "binomial" #specify logistic regression
)
To get a sense of what the propensity scores produced from a logistic regression look like, let’s take a look at a histogram of the propensity scores from prop_model.

Histogram showing frequency of propensity scores ranging from 0.0 to 0.8. The distribution is hill-shaped but right-skewed and centered near 0.2.

The plot indicates that our model produced a lot of low probabilities of being treated for our observations. This makes sense given that the bal.tab() output in the last exercise showed us we had 190 students in the non-meditation group and only 60 in the meditation group.

Instructions
1.
Since, in our heart health example, we are trying to estimate the causal effect of low ejection fraction on length of hospital stay, the propensity score model should model the probability of having low ejection fraction given other characteristics.

The dataset los_data has been loaded for you in notebook.Rmd. Use the glm() function to run a logistic regression that models the probability of having low ejection fraction given age and cholesterol level. Save the results as ef_model.

Checkpoint 2 Passed

Stuck? Get a hint
2.
Uncomment and run the code to create a histogram (named ef_hist) of the propensity scores predicted from the ef_model logistic regression. The histogram will print automatically. Do you have a lot of low or high scores, or is the distribution more symmetric?