Performing IPTW in R
If this seems like a lot of work, don’t worry! The WeightIt package in R has functions to model the propensity scores and simultaneously perform propensity score weighting. We don’t need to make a separate logistic regression or compute the weights manually using a formula.

IPTW can be performed in R with the weightit() function from the WeightIt package. There are several key arguments to this function that allow us to tweak how weighting is performed.

formula—represents the propensity score model to use.
method—determines the weighting method that will be used. While there are various options, we will use “ps” to perform IPTW using logistic regression.
estimand—specifies the desired treatment effect estimand: “ATE” for average treatment effect, “ATC” for average treatment effect on the controls, or “ATT” for average treatment effect on the treated.
To perform IPTW for the ATT on the student sleep data, we fill in these arguments accordingly. Remember that our propensity score model includes meditate as the outcome and only stress as the predictor.

# import library
library(WeightIt)
# model propensity scores and IPTW weights
iptw_sleep <- weightit(
  formula = meditate ~ stress, #propensity model
  data = sleep_data, #dataset
  method = "ps", #use IPTW
  estimand = "ATT" #estimand
)
The weightit() function models the propensity scores and creates the IPTW weights in one step. We save these outputs in a weightit object we name iptw_sleep, which we will use in our next step.

Instructions
1.
Great job so far!

Now you will perform IPTW using the los_data dataset, which has been loaded for you in notebook.Rmd. Use the weightit() function to model propensity scores and perform IPTW for the ATT. Remember we are modeling the probability of having low ejection fraction given age and cholesterol level.

Save the results as iptw_ef.