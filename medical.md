---
title: "Plotting Practice"
author: "Vivek Pruthi"
date: "November 16, 2017"
output:
  word_document: default
  pdf_document: default
  html_document: default
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

```{r,echo=FALSE,results='hide'}
time<-Sys.time()


```

Update time for this document is `r time`

We have the medical expense data available from different states and we want to find out the relation between the Mean covered charges and the Mean total Payments. In the following figure we are trying to get that relation for the state of NY:

```{r firstplot,echo=FALSE,message=FALSE,error=FALSE,cache=TRUE}
meddata<-read.csv("medical.csv",header = TRUE,sep = ",",stringsAsFactors = FALSE)
#names(meddata)
library(ggplot2)
library(dplyr)
library(ggthemes)
library(scales)
#head(meddata)
meddata%>%filter(Provider.State=="NY")%>%ggplot(aes(x=Average.Covered.Charges,y=Average.Total.Payments))+ggtitle("Mean Covered Charges vs Mean Total Payments in NY")+scale_x_continuous(labels = comma)+scale_y_continuous(labels = comma)+geom_point()+theme_economist()
```

***

Second plot will try to find out the relation between the Mean covered charges and the Mean total Payments by medical condition and provider's state
```{r secondplot,echo=FALSE,fig.width=14,fig.height=11,cache=TRUE}
meddata%>%ggplot(aes(x=Average.Covered.Charges,y=Average.Total.Payments))+geom_point()+scale_x_continuous(labels = comma)+scale_y_continuous(labels = comma)+facet_grid(DRG.Definition~Provider.State)+ggtitle("Mean Covered Charges vs Mean Total Payments",subtitle = "By Medical Condition and Provider's state")+theme(axis.text.x=element_text(angle=90, hjust=1),strip.text.y = element_text(size = 8,angle = 0))
```



