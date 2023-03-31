## Summary statistics
Simply summarize your data by exploring its mean, median, mode, range, interquartile range, percentile, standard deviation, standard error etc.
 
### Install required packages
- install.packages("stats")
- install.packages("dplyr") 

### Load required packages
- library(stats)
- library(dplyr)

### Load inbuild data (or your data)
- data(iris)
- str(iris) # to view structure of data

### Find summary of your data
- summary(iris)
- tapply(iris$Sepal.Length,iris$Species, summary)
- group_species=group_by(iris,Species)
- summary=summarise(group_species,count=n(),mean=mean(Sepal.Length),"standard deviation"=sd(Sepal.Length))
- summarydata=as.data.frame(summary)
- kable (summarydata,digits = 3,align = 'c')
