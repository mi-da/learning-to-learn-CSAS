---
title: "Learning to learn in Collective Self-adaptive Systems: Automated Reasoning for System Design Patterns"
output: html_notebook
---

# Dataset

```{r fig.align="center"}
dataset
```


# Clustering Analysis

The notion of similarity between papers refersto similarity between their attributes (see dataset). Since the attributes identified by our classification are categorical, we adopt the Gower Distance measure.

```{r ig.align="center"}
gower.dist <- daisy(x, metric = c("gower"))
```

HAC  starts  by  treating  each  observation  (i.e.,paper)  as  a  separate  cluster.  Then,  it  repeatedlyidentifies and merge the two most similar clusters.

```{r fig.align="center"}
aggl.clust.c <- hclust(gower.dist, method = "complete")
plot(aggl.clust.c,cex = 0.7)
```


There are two methods allowing establishing evaluation  criteria for the number ofclusters K to adopt: silhouette values and the bootstrap method.

Silhouette Analysis:

```{r fig.align="center"}
ggplot(data = data.frame(t(cstats.table(gower.dist, aggl.clust.c, 10))), 
       aes(x=cluster.number, y=avg.silwidth)) + 
  geom_point(size=1.5)+
  geom_line(size=0.5)+
  scale_x_continuous(breaks = scales::pretty_breaks(n = 10), limits=c(2, 10)) +
  scale_y_continuous(breaks = scales::pretty_breaks(n = 10)) +
  ggtitle("") +
  labs(x = "K", y = "Average silhouette width") +
  theme_minimal(base_size = 15) +
  geom_hline(yintercept=0.18, linetype="dashed", 
                color = "red", size=1)
```


Silhouette Analysis Bootstrap of Clusters and Visualization:

* 2 CLUSTERS:

```{r fig.align="center"}
kchoice<-2
invisible(capture.output(cboot.hclust <- clusterboot(gower.dist,distances=TRUE,clustermethod=hclustCBI, k=kchoice,method="complete",seed="123456789")))
cboot.hclust$bootmean  
cboot.hclust$bootbrd 
```

```{r fig.align="center"}
dendro <- as.dendrogram(aggl.clust.c)
dendro.col <- dendro %>%
 set("branches_k_color", k = 2, value =   c("#2E9FDF","red")) %>% 
  set("branches_lwd", 1) %>%
  set("labels_colors", k = 2, value =   c("#2E9FDF","red")) %>% 
  set("labels_cex", 1)
circlize_dendrogram(dendro.col)
```

* 3 CLUSTERS:

```{r fig.align="center"}
kchoice<-3
invisible(capture.output(cboot.hclust <- clusterboot(gower.dist,distances=TRUE,clustermethod=hclustCBI, k=kchoice,method="complete",seed="123456789")))
cboot.hclust$bootmean  
cboot.hclust$bootbrd 
```

```{r fig.align="center"}
dendro <- as.dendrogram(aggl.clust.c)
dendro.col <- dendro %>%
 set("branches_k_color", k = 3, value =   c("#2E9FDF", "red","#E7B800")) %>% 
set("branches_lwd", 1) %>%
set("labels_colors", k = 3, value =   c("#2E9FDF", "red","#E7B800")) %>% 
set("labels_cex", 1)
circlize_dendrogram(dendro.col)
```

* 4 CLUSTERS:

```{r fig.align="center"}
kchoice<-4
invisible(capture.output(cboot.hclust <- clusterboot(gower.dist,distances=TRUE,clustermethod=hclustCBI, k=kchoice,method="complete",seed="123456789")))
cboot.hclust$bootmean  
cboot.hclust$bootbrd 
```

```{r fig.align="center"}
dendro <- as.dendrogram(aggl.clust.c)
dendro.col <- dendro %>%
  set("branches_k_color", k = 4, value =   c("#2E9FDF","red","#E7B800","darkgreen")) %>% 
  set("branches_lwd", 1) %>%
  set("labels_colors", k = 4, value =   c("#2E9FDF","red","#E7B800","darkgreen")) %>% 
  set("labels_cex", 1)
circlize_dendrogram(dendro.col)
```

* 9 CLUSTERS:

```{r fig.align="center"}
kchoice<-9
invisible(capture.output(cboot.hclust <- clusterboot(gower.dist,distances=TRUE,clustermethod=hclustCBI, k=kchoice,method="complete",seed="123456789")))
cboot.hclust$bootmean  
cboot.hclust$bootbrd 
```

```{r fig.align="center"}
dendro <- as.dendrogram(aggl.clust.c)
dendro.col <- dendro %>%
  set("branches_lwd", 1) %>%
  set("labels_colors", k = 9, value=c("#2E9FDF","red","#E7B800","darkgreen", "blue","darkorange","black","gray","purple")) %>% 
  set("labels_cex", 1)
circlize_dendrogram(dendro.col)
```
