
# Box plot in R
### Required package
library(ggplot2)

### load built in data
- data(iris)
- str(iris)

### Box plot
ggplot(data=iris,aes(x=factor(Species),y=Sepal.Length))+geom_boxplot()+xlab("Species")+ylab("Sepal.lenght")
