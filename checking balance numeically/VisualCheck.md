Checking Balance Numerically
While visual assessments of balance are definitely helpful, we can also assess overlap and balance numerically using the standardized mean difference (SMD) and variance ratio for each variable.

Observing an SMD of exactly zero or a variance ratio of exactly one is pretty uncommon. Therefore, the following guidelines can be used to indicate good balance:

SMD between -0.1 and 0.1
Variance ratio between 0.5 and 2.0
The bal.tab() function from the cobalt package is a complement to the bal.plot() function that quantifies the balance of variables in a dataset. The bal.tab() function has similar arguments and syntax to the bal.plot() function. We need to update our formula to include both variables of interest. Then we can show SMDs for all variables and variance ratios for all continuous variables in the sleep dataset by specifying binary = "std" and disp.v.ratio = TRUE, respectively:

# import library
library(cobalt)
# print table of SMDs and variance ratios
bal.tab(
  x = meditate ~ stress + graduate, #formula
  data = sleep_data, #dataset
  disp.v.ratio = TRUE, #display variance ratio
  binary = "std" #SMDs for binary variables
)
The output of the bal.tab() that follows shows that the stress variable has an SMD of -0.9132 and a variance ratio of 0.5461 between the treatment and control groups. The graduate variable has an SMD of -0.6548.

Balance Measures
            Type    Diff.Un   V.Ratio.Un
stress    Contin.   -0.9132       0.5461
graduate  Binary    -0.6548
 
Sample Sizes
        Control Treated
All        190      60
The SMDs clearly fall outside the range of -0.1 to 0.1, which suggests there is an imbalance between the treatment and control groups. The variance ratio for the stress variable is only just within the acceptable range. Time to put propensity score methods to the test to see if we can reduce this imbalance!

Instructions
1.
Again working with our heart health dataset, use the bal.tab() function to get balance metrics for age, cholesterol, and heart_attack in the los_data dataset. Make sure you set disp.v.ratio to TRUE and binary to "std". Save the table as bt.

Checkpoint 2 Passed

Stuck? Get a hint
2.
Print bt to view the results. Do any variables appear to have poor balance? Do these results make sense based on the balance plots you made in the previous two exercises?