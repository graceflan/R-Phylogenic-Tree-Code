# R-Phylogenic-Tree-Code

### Load libraries
```
library(ape)
library(phytools)
library(gtools)
library(ggtree)
library(cowplot)
library(ggimage)
library(treeio)
library(gridExtra)
```
### Load in .tre file
```
tree <- read.astral(""Annotated and rooted phylogenetic tree file name".tre")
```
### make a label with the three QS separated by underscores
```
Q1 <- as.numeric(tree@data$pp1)
Q <- as.data.frame(Q1)
Q$Q2 <- as.numeric(tree@data$pp2)
Q$Q3 <- as.numeric(tree@data$pp3)
Q$node <- tree@data$node
node <- tree@data$node
allQS <- as.data.frame(node)
for (x in (1:length(allQS$node))) {allQS$QS[x] <- paste(round(Q$Q1[x], digits = 2), "/", round(Q$Q2[x], digits = 2), "/", round(Q$Q3[x], digits = 2), sep = "")}
```
### To change tip label
```
tree@phylo$tip.label["tip number"] <-Species name
```
### Print the tree
```
p1 <- ggtree(tree@phylo, ladderize=T, branch.length = "none") %<+% allQS + 
  geom_nodelab(aes(x=branch, label=QS),hjust= 0.7, vjust=-1, size=2) +
  geom_tiplab(size=3, hjust= -0) + xlim_tree(25) 
p1
```
