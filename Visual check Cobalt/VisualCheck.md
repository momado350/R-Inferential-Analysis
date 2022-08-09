Visual Check of Categorical Variables
Distribution plots are great for numeric variables, but we need a different type of plot for categorical variables. Fortunately, we can use the exact same bal.plot() function from cobalt with no need to specify the variable type. By updating the arguments for x and var.name to use graduate, we will get a bar plot to examine balance for the categorical variable graduate.

# import library
library(cobalt)
# plot distributions for stress variable
bal.plot(
  x = meditate ~ graduate, #new formula
  data = sleep_data, #dataset
  var.name = "graduate", #new variable
  colors = c("#E69F00", "#009E73") #set fill colors
)
A bar plot of the proportion of undergraduate and graduate students split by treatment (meditation) status. There are more treated than control undergraduates, and there are more control than treated graduates.

From this plot, we see that the ratio of undergraduates to graduates is much larger for the meditation group (green) than for the non-meditation group (orange).

Both plots so far suggest that there are differences between the treatment and control groups with respect to the stress and graduate variables. However, balance plots don’t precisely quantify the degree of imbalance in the dataset. To get a more detailed picture, we can check balance numerically.

Instructions
1.
Let’s return to the heart health dataset.

Use the bal.plot() function to create a balance plot for the heart_attack variable. Save this plot as an object named heart_plot.

Checkpoint 2 Passed

Stuck? Get a hint
2.
Print heart_plot to view the plot. Does heart attack history appear balanced across treatment groups?