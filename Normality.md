# Normality test
Test of normality is necessary before doing any kind of parameteric test. Normality of data can be checked either visually or using test statistics. Alternatively,
if the data is not normal, we can do some transformation depending upon the types of data. If the data is not normal even after the transformation, non-paramteric test statistics can be used. 

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
