Re-checking Overlap and Balance
If propensity score weighting is successful, we expect the distribution of propensity scores in the treatment group to be similar to that of the control group.

To check the overall balance of propensity scores, we can again use the bal.plot() function from the cobalt package. This time we pass the weightit object to the x argument and "prop.score" to the var.name argument, with no need for the data argument. Lastly, we set which equal to both so we can view the propensity scores before (“unadjusted”) and after (“adjusted”) weighting is performed.

# import library
library(cobalt)
 
# create balance plot of propensity scores
bal.plot(
  x = iptw_sleep, #weightit object
  var.name = "prop.score", #propensity scores
  which = "both", #before and after
  colors = c("#E69F00", "#009E73") #sets fill colors
)
Two density plots side by side showing the distributions of propensity scores for the treatment and control groups. The left plot is from before weighting. The two distributions are nearly the same height, but the control group is centered near 0.1 while the treatment group is centered near 0.3, so they have limited overlap. The right plot is from after weighting. The treatment distribution is the same as the left plot, but the control distribution is now shorter and centered closer to 0.3, so they overlap more than they did in the left plot.

The distributions of propensity scores look similar after IPTW, but we should check the balance of individual variables, too. The love.plot() function in cobalt visually checks the standard mean differences (SMD) between treatment groups for all variables before and after weighting. We can also show guidelines at ±0.1 SMD by setting thresholds = c(m = 0.1).

love.plot(
  x = iptw_sleep, #weightit object
  binary = "std", #use SMD
  thresholds = c(m = 0.1), #guidelines
  colors = c("#E69F00", "#009E73") #sets fill colors
)
A Love plot that shows standardized mean differences across the x-axis and points for unadjusted and adjusted SMD's for stress and propensity scores. The unadjusted scores are far outside the guidelines of plus or minus 0.1. The adjusted scores are just outside these guidelines.

Oh no! Based on this plot, it appears as if the propensity score weighting was unsuccessful: the SMDs between groups are outside the ±0.1 cutoffs for the stress variable and for the propensity scores themselves. Since there is still some residual imbalance between treatment groups, we should backtrack to step 2 and refine the propensity score model.

Instructions
1.
Time to assess the quality of the propensity score weighting you completed in the previous exercises! The los_data dataset has been loaded for you, and code has been provided for the weightit model, which is saved as iptw_ef.

Use the bal.plot() function to show the distribution of propensity scores before and after the IPTW procedure and save the plot as ps_bal.

Checkpoint 2 Passed

Stuck? Get a hint
2.
Print and inspect ps_bal. Do you think an adequate balance has been achieved?

Checkpoint 3 Passed

Stuck? Get a hint
3.
Use the love.plot() function to plot the balance of variables after the propensity score weighting/IPTW. Save this plot as ps_love.

Checkpoint 4 Passed

Stuck? Get a hint
4.
Print and inspect ps_love. Take note of the standardized mean differences. Do the values match what you expected from the balance plot?