Propensity Score Weighting
Now that you know about the basics of propensity scores, let’s talk about some possible applications.

Propensity scores often show up in matching and stratification. However, we will focus on propensity score weighting because it is a popular choice with strong performance.

Propensity score weighting transforms estimated propensity scores into weights that emphasize or diminish certain observations in our dataset. One widely used type of propensity score weighting is known as inverse probability of treatment weighting (IPTW).

IPTW weights are calculated differently depending on whether we want to estimate the average treatment effect (ATE) or the average treatment effect on the treated (ATT). Note that with ATE we are looking at the effect across the entire population, both the treated and control groups. ATT is just on the treated group.

The formulas for the treatment and control group weights for each estimand are below. p represents the propensity score for a particular individual.

ATE	ATT
Treatment Weight	1/p	1
Control Weight	1/(1-p)	p/(1-p)
It may not be immediately obvious, but these formulas tell us that IPTW makes the treatment and control groups appear more similar in two ways:

By giving MORE weight to individuals who look like those in the opposite treatment assignment.
By giving LESS weight to individuals who look like those in their own treatment assignment.
Check out the following table that shows some example weights for treatment and control observations using IPTW for the ATE.

treatment group	propensity score	weight
treatment	0.1	10.0
treatment	0.5	2.0
treatment	0.9	1.1
control	0.1	1.1
control	0.5	2.0
control	0.9	10.0
Note the pattern:

The treated individual with the low propensity score of 0.1 (looks more like a control) is given a high weight of 10.
The treated individual with the high propensity score of 0.9 (looks like the other treated individuals) is given a low weight of 1.1.
The weighting goes in the opposite direction for the controls.
The justification for this method is that someone who looks more like the individuals in the other treatment group is a better counterfactual for them, so we count these individuals as more important. This helps balance our treatment groups without discarding any observations.

Instructions
1.
Let’s look at a sample of the data from our heart health example.

A small dataset called los_sample has been loaded for you in notebook.Rmd. This dataset contains a sample of observations from los_data for two variables:

low_ef — indicates the control (low_ef = 0) or treatment (low_ef = 1) group
ps — indicates the propensity score for each observation
Print los_sample using the print() function. Note that the dataset is arranged by treatment group with propensity scores in ascending order within each group.

Checkpoint 2 Passed

Stuck? Get a hint
2.
Uncomment the code to make a variable called ATE_weight with the weights when calculating the ATE. Then print los_sample again to view the ATE weights. Why do you think the range of ATE weights is not as large for low_ef = 0 in this sample?

Checkpoint 3 Passed

Stuck? Get a hint
3.
Uncomment the code to make a variable called ATT_weight. This time the weights are for the ATT. Print los_sample again to view the ATT weights in comparison to the ATE weights. How does the weighting compare? Think about what’s similar and what’s different and why that might be.