#Two-way ANOVA test is used to evaluate simultaneously the effect of two grouping variables (A and B) on a response variable.
#Assumption of Two-way ANOVA: response variables are normally distributed and have equal variance across groups

#Required packages
library(stats)
library(dplyr)
library(car)

# You can use the ToothGrowth data available in R
# The ToothGrowth data consists of tooth growth values when Guinea pigs are treated with two types of delivery methods of vitamin C and at three different dose level of vitamin C
# Grouping variables: (i) delivary method of vitamin C and (ii) different dose level

data(ToothGrowth) # Load data in R
head(ToothGrowth) # Show the outline of ToothGrowth data 
str(ToothGrowth) # Check the structure

#Test the normality of tooth growth value
shapiro.test(ToothGrowth$len)

# p-value is greater than 0.05. It means data is normal.

# Now before checking homogeneity of variace across group change the dose to categorical variable in ToothGrowth data
fix(ToothGrowth)
# Click dose header and select type as character
# Check whether variance is same across group or not?
leveneTest(len~supp*dose,data=ToothGrowth) 

# p-value is greater than 0.05. It means data has homogeneity of variace across groups.

Two_way_Anova=aov(len~supp*dose,data=ToothGrowth) # Perform Two-way ANOVA

summary(Two_way_Anova) # Summary of ANOVA test
#Interpretation of results
#the p-value of supp is 0.000231 (significant), which indicates that the levels of supp are associated with significant different tooth length.
#the p-value of dose is < 2e-16 (significant), which indicates that the levels of dose are associated with significant different tooth length.
#the p-value for the interaction between supp*dose is 0.02 (significant), which indicates that the relationships between dose and tooth length depends on the supp method.

#Visualize the data
install.packages("ggpubr")

#Run "ggpubr" packages
library(ggpubr)

# Box-plot
ggboxplot(ToothGrowth, x = "dose", y = "len", color = "supp",palette = c("#00AFBB", "#E7B800"))
