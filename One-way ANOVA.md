#One-way ANOVA in R
#load required packages
library("ggplot2")
library("ggpubr")

#load data
data("PlantGrowth")
str(PlantGrowth)

#Check normality of weight
ggqqplot(PlantGrowth$weight) #create Q-Q plot
ggplot(PlantGrowth, aes(x=weight)) + geom_density() #create density curve
shapiro.test(PlantGrowth$weight) #normality test statistics

#Test for homogeneity of variance
bartlett.test(weight~group,data=PlantGrowth) 

#Doing One-way ANOVA
ANOVA=aov(weight~group,data=PlantGrowth)
summary(ANOVA) #summary of anova

#posthoc test
TukeyHSD(ANOVA)

#Box-Plot
ggboxplot(PlantGrowth,x="group",y="weight",width=0.8,fill="lightblue")
