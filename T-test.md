# One-sample T-test

# Paired sample T-test
Compare differences between two dependent means. Commonly applied for case-control studies or repeated measures. 
Assumptions of paired sample t-test
1. Dependent variable must be numeric or continuous
2. Dependent variable should be normally distributed
3. Variace across two measures should not be statistically different.

### Install required packages
install.packages("dplyr") 

install.packages("ggpubr")

install.packages("stats")


#Remember if you have already installed these packages, it is not required to install them again and again.
  
### Load required packages
library(dplyr)

library(ggpubr)

library(stats)

### Load data 
Copy your data in excel and run this command or there are several other option to import your data.
  
data=read.table("clipboard", header=TRUE) 

#I will prepare one data for the test, where a training was conducted to improve knowledge of participants of ICT. Their scores were measured before and after the training. 
  
before=c(12.2, 14.6, 13.4, 11.2, 12.7, 10.4, 15.8, 13.9, 9.5, 14.2)

after=c(13.5, 15.2, 13.6, 12.8, 13.7, 11.3, 16.5, 13.4, 8.7, 14.6)

#Create data frame
ICT=data.frame(time=rep(c("before","after"), each=10), score=c(before, after))

print(data)

### Check normality
shapiro.test(ICT$score) # Data is normally distributed

### Check homogeneity of variance
bartlett.test(score~time, data=ICT) # Data has equal variance

### Paired sample T-test
t.test(formula = score ~ time, data=ICT, alternative = "greater", mu = 0, paired = TRUE, var.equal = TRUE, conf.level = 0.95)

### Visualize data
ggboxplot(ICT, x = "time", y = "score", color = "time", palette = c("#00AFBB", "#E7B800"), order = c("before", "after"), ylab = "Score", xlab = "Time")

# Independent sample T-test


