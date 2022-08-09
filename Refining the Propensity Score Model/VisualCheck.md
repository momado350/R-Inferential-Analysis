Refining the Propensity Score Model
As you may have noticed, propensity score methods are an iterative process: we check variable balance, model propensity scores, perform weighting, then check balance again. If imbalance still exists, we can change the propensity score model. A main assumption of propensity score weighting is that we’ve modeled the propensity scores correctly — a poor model could lead to biased estimates of the treatment effect!

Let’s update our propensity score model from the student sleep data to see if imbalances between groups can be reduced further.

The initial propensity score model only included the stress variable as a predictor of meditation, but what happens if we add the graduate variable as a second predictor? We need to update the formula in the weightit() function:

# import library
library(WeightIt)
# update weightit object
iptw_sleep_update <- weightit(
  #new formula
  formula = meditate ~ stress + graduate,
  data = sleep_data,
  estimand = "ATT",
  method = "ps"
)
We re-check balance again to see if the new propensity score model produces a better balance between groups.

# import library
library(cobalt)
# create Love plot of updated model
love.plot(
  x = iptw_sleep_update, #updated model,
  binary = "std", #show SMD
  thresholds = c(m = 0.1), #guidelines
  colors = c("#E69F00", "#009E73") #fill colors
)
A Love plot that shows standardized mean differences across the x-axis and points for unadjusted and adjusted SMD's for stress, graduate status, and propensity scores. The unadjusted scores are far outside the guidelines of plus or minus 0.1. The adjusted scores are now all within these guidelines.

Success! Both plots show that this new propensity score model produces improved balance. The SMDs now fall between -0.1 and 0.1.

Note that it can take multiple tries to find a good propensity score model. If we needed to further refine our model, we might add more complex terms to the equation, such as polynomial terms or interactions.

Instructions
1.
Update the formula argument of the weightit model to add the heart_attack variable to the propensity score model as a predictor of low ejection fraction. Then uncomment and run the code to assign the output to iptw_ef2.

Checkpoint 2 Passed

Stuck? Get a hint
2.
Create a new Love plot showing the standardized mean differences and thresholds of ±0.1 using the updated weightit model. Save your plot as love_update.

Checkpoint 3 Passed

Stuck? Get a hint
3.
Print love_update and inspect the plot. Did your new model improve the balance?