# Normality test

### load required packages
library("ggplot2")

library("ggpubr")

### load built in data
data("ToothGrowth")

head(ToothGrowth)

str(ToothGrowth)

### Checking normality visually
#### 1. Q-Q plot
ggqqplot(ToothGrowth$len) #As all the points fall approximately along this reference line, we can assume normality.

#### 2. Density curve
ggplot(ToothGrowth, aes(x=len)) + geom_density() #Bell shaped graph indicate normality  
ggplot(ToothGrowth, aes(x=len, fill=supp)) + geom_density(alpha=.3) #Density curve by group

### Test statistics
shapiro.test(ToothGrowth$len) #p-value = 0.1091 means data is normally distributed

- note: If data is not normal try some transformation depending upon your data types.
