Estimating Causal Effects
Now that we have a good balance, we can proceed to the last step of a propensity score analysis: estimating the causal treatment effect.

If we think back to the beginning of our lesson, the motivation for studying student sleep was to estimate the effect of meditation on average sleep in university students. So, to estimate the causal treatment effect of meditation, we need to fit a regression model for the outcome variable (hours of sleep) and incorporate the propensity score weights from our weightit model.

The final regression model should include hours of sleep as the outcome variable, use of meditation as the treatment group variable, and stress level and graduate status as the other predictor variables.

To use the propensity score weights from IPTW, we set the weights argument of the glm() function equal to the estimated IPTW weights. These are stored in our updated weightit model that we called iptw_sleep_update.

outcome_mod_weight <- glm(
  #outcome model
  formula = sleep ~ meditate + stress + graduate,
  #dataset 
  data = sleep_data,
  #IPTW weights
  weights = iptw_sleep_update$weights 
)
To get the estimated treatment effect, we use the coeftest() function from the lmtest package. Weighting can cause our standard errors to be inaccurate. To get the best estimate of the treatment effect, we need a more robust calculation of the standard errors, so we add the argument vcov. = vcovHC made available by the sandwich package. We won’t cover this in detail here, but this adjustment means we are using a heteroscedasticity-consistent estimation of the covariance matrix for estimates of the coefficients.

# import library
library(lmtest)
library(sandwich)
# perform tests of regression coefficients
coeftest(
  outcome_mod_weight, #weighted outcome model
  vcov. = vcovHC #robust standard errors
)
As we can see in the following output, the coefficient for the meditation variable is 1.02. If we have met the assumptions of IPTW, this means that we can conclude that a typical student who practiced meditation got an additional 1.02 hours of sleep because of meditation.

z test of coefficients:
 
              Estimate  Std. Error  z value   Pr(>|z|)
(Intercept)   8.971964    0.669241  13.4062  < 2.2e-16 ***
meditate      1.024871    0.215333   4.7595  1.941e-06 ***
stress       -0.045191    0.013664  -3.3072  0.0009422 ***
graduate     -0.770913    0.280460  -2.7487  0.0059823 **
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 '' 1
NOTE: You may need to adjust the width of this section of the screen to make it large enough to view the output properly.

Instructions
1.
A weightit model using the los_data dataset has been created for you in notebook.Rmd and saved as iptw_ef2.

Fit a regression model with length of hospital stay as the outcome and age, cholesterol level, and heart attack history as predictors. Use the IPTW weights from iptw_ef2. Save your model as outcome_mod.

Checkpoint 2 Passed

Stuck? Get a hint
2.
Use the coeftest() function to estimate the treatment effect from the model you just fit and assign the result to att_robust. Be sure to use robust standard error estimates.

Checkpoint 3 Passed

Stuck? Get a hint
3.
Print the output of att_robust to view the results of your analysis. Do your results match the conclusion that follows?

Based on the regression coefficient for the low_ef variable from the final outcome model, we can conclude that low ejection fraction causes a typical cardiology patient to stay in the hospital about 1.2 days longer than if they did not have a low ejection fraction.