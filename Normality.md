# Normality test
Test of normality is necessary before doing any kind of parameteric test. Normality of data can be checked either visually or using test statistics. Alternatively,
if the data is not normal, we can do some transformation depending upon the types of data. If the data is not normal even after the transformation, non-paramteric test statistics can be used. 

### Install required packages
install.packages("ggplot2")

install.packages("ggpubr")

### Load required packages
library("ggplot2")

library("ggpubr")

### Load built in data
data("ToothGrowth") # to load data

head(ToothGrowth) # to view headings of the data

str(ToothGrowth) # to view structure of the data

### Checking normality visually
#### 1. Q-Q plot
ggqqplot(ToothGrowth$len) #As all the points fall approximately along the reference line, we can assume the data is normally distributed.

#### 2. Density curve
ggplot(ToothGrowth, aes(x=len)) + geom_density() #Bell shaped graph indicate normality  

ggplot(ToothGrowth, aes(x=len, fill=supp)) + geom_density(alpha=.3) #Density curve by group

### Test statistics
shapiro.test(ToothGrowth$len) #p-value = 0.1091 means data is normally distributed
