Visual Check of Numeric Variables
Suppose we are interested in determining whether the practice of meditation increases the amount of sleep that university students get per night. To gather more information, we surveyed 250 students about their sleeping and meditation habits over the previous year. Note that students were not randomly assigned to treatment groups; students were simply asked about their actions. Their responses were recorded in a dataset with these variables:

sleep — average hours of sleep per night (outcome variable)
meditate — indicates whether or not the individual reports consistent use of meditation (treatment group variable)
stress — a self-reported measure of stress on a 1-to-100 scale, with 1 representing no stress and 100 representing extremely high stress
graduate — indicates whether or not a student is in a graduate program versus an undergraduate program (0 = undergraduate; 1 = graduate).
We can use the bal.plot() function from the R package, cobalt, to visually check if any variables are severely imbalanced and whether propensity score methods might be useful. The function takes a formula where the left side specifies the treatment group indicator and the right side includes a variable we want to view. To check the stress variable, the formula would be meditate ~ stress. Then we specify the dataset name and the variable of interest in quotes as additional arguments.

# import library
library(cobalt)
# plot distributions for stress variable
bal.plot(
  x = meditate ~ stress, #formula
  data = sleep_data, #dataset
  var.name = "stress" #variable
  colors = c("#E69F00", "#009E73") #set fill colors
)
Note that we also set the optional argument colors to c("#E69F00", "#009E73") for better contrast.

Density plot of the stress levels of the meditation and non-meditation groups. The meditation group is centered around a score of 40 with a narrow spread, while the non-meditation group is centered around 55 with a much wider spread of stress scores.

The distributions in the plot appear to differ pretty substantially between the treatment groups, potentially indicating poor balance. The meditation group (green) is centered around a score of 40 with a narrow spread, while the non-meditation group (orange) is centered around 55 with a much wider spread of stress scores.
## instructions
1.
It’s time to start getting some hands-on experience with propensity score methods!

Imagine that you are working for a hospital and you are tasked with figuring out why some patients stay longer than others. You decide to investigate heart health first, and will look at ejection fraction. Ejection fraction (EF) is a measure of how much blood the heart pumps with each beat. A low EF may indicate poor heart health.

You have access to a dataset called los_data, which contains the following variables related to the health of 1,000 hospital patients who were admitted to the cardiology unit:

age — Age (years)
cholesterol — Indicates whether the patient has high cholesterol (0 = normal cholesterol; 1 = high cholesterol)
heart_attack — History of heart attack (0 = no heart attack history; 1 = previous heart attack)
low_ef — Low ejection fraction (0 = normal ejection fraction; 1 = low ejection fraction)
hospital_los — Length of hospital stay (days)
With this dataset, we will use propensity score methods to determine the causal effect of having a low ejection fraction on how long patients stay in the hospital.

The dataset los_data has been loaded for you in notebook.Rmd. Use the bal.plot() function to create a balance plot for the age variable. Save this plot as an object named age_plot.

Checkpoint 2 Passed

Stuck? Get a hint
2.
Print age_plot and view the plot of the distributions. Think about whether age appears balanced based on your plot.