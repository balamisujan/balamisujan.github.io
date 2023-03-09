library(igraph)
library(Hmisc)
library(Matrix)

data=read.table("clipboard",header=TRUE, row.names =1)
taxa=read.table("clipboard",header=TRUE, row.names =1)

#data dimension
dim(data)

#Filter OTUs with low abundance (e.g. less than 10 reads)
otu.table.filter=data[,colSums(data) >= 10]

#Find out how many OUTs you have removed after filtering
print(c(ncol(data),"versus",ncol(otu.table.filter)))

#Network analysis
#Prepare correlation matrix
otu.cor=rcorr(as.matrix(data), type="spearman")

#Obtain p-value information
otu.pval=forceSymmetric(otu.cor$P)

#select only the taxa by using row names of Otu.pval
sel.tax=taxa[rownames(otu.pval),,drop=FALSE]

#Sanity check
all.equal(rownames(sel.tax), rownames(otu.pval))

#Filter the association based on p-values and level of correlations
p.yes=otu.pval<0.05

#Select the r values for the filter probality of < 0.5.
r.val=otu.cor$r
p.yes.r=r.val*p.yes

#Select OTUs by level of correlation
p.yes.r=abs(p.yes.r)>0.75 
p.yes.rr=p.yes.r*r.val

#Create an adjacency matrix
adjm=as.matrix(p.yes.rr)

#Add taxonomic information from the metadata associated with adjacency matrix
colnames(adjm)=as.vector(sel.tax$Genus)
rownames(adjm)=as.vector(sel.tax$Genus)


net.grph=graph.adjacency(adjm,mode="undirected",weighted=TRUE,diag=FALSE)

#Obtaining edge weight based on the Spearman correlation
edgew=E(net.grph)$weight

#Creating a vector to remove the isolated nodes (nodes with no interactions)
bad.vs=V(net.grph)[degree(net.grph) == 0] 

#Removing the isolated nodes from the graph object using the function
net.grph=delete.vertices(net.grph, bad.vs)

plot(net.grph,
     vertex.size=4,
     vertex.frame.color="black",
     edge.curved=F,
     edge.width=0.1,
     layout=layout_with_kk,
     edge.color=ifelse(edgew < 0,"red","blue"),
     vertex.label.color="black",
     vertex.label.family="Arial",
     vertex.label.font=1)
