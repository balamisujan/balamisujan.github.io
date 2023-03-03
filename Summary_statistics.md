## Exploratory data analysis

### Install required packages
- install.packages("stats")
- install.packages("dplyr") 

### Load required libraries
- library(stats)
- library(dplyr)

### Loading data
- data(iris)
- str(iris)

### Summary
- summary(iris)
- tapply(iris$Sepal.Length,iris$Species, summary)
- group_species=group_by(iris,Species)
- summary=summarise(group_species,count=n(),mean=mean(Sepal.Length),"standard deviation"=sd(Sepal.Length))
- summarydata=as.data.frame(summary)
- kable (summarydata,digits = 3,align = 'c')
