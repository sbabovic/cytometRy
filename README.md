Analyzing flow cytometry data using R
======================

This is a very basic guide to using R for analysis of flow cytometry data.  It is intended for biologists already comfortable with flow cytometry but with minimal or no knowledge of programming.  For people totally new to R, I highly recommend completing tutorials #1 and #2 on [Cyclismo.org](http://www.cyclismo.org/tutorial/R/) to get a basic sense of the syntax of the language.  An even more user-friendly introduction to R can be found at [CodeSchool](http://tryr.codeschool.com/levels/1/challenges/1).  People already familiar with other programming languages, or who already have some knowledge of R, may find [aRrgh](https://github.com/tdsmith/aRrgh/blob/master/README.md) highly useful. 

Before moving on, please read the guide for [Before you start](https://github.com/sbabovic/cytometRy/blob/master/README.md#before-you-start).

======================

This guide is largely derived from scripts provided by [insert name], but mistakes are all mine. 

======================

Have you completed everything in the [Before you start](https://github.com/sbabovic/cytometRy/blob/master/README.md#before-you-start) section?  Yes?  Good!

This document will be made up of a couple of parts: [Part I](https://github.com/sbabovic/flow-cytometry-using-R/blob/master/README.md#part-i) and [Part II](https://github.com/sbabovic/flow-cytometry-using-R/blob/master/README.md#part-ii).

### Part I 

First you need to set your working directory.  In Windows, this will look something like this (replace the path name with the folder which you'll use to store files for this tutorial, and be sure to replace the default back slash with a forward slash!)

    setwd("C:/Documents and Settings/username/My Documents/R tutorial")

On a Mac, this will look something like: 

    setwd("/Users/username/R tutorial")

Now load the libraries flowCore and flowViz: 

    library(flowCore)
    library(flowViz)
    
### Part II

Then you need to define the function fluortrans and draw2dgate

    fluortrans<-arcsinhTransform(transformationId="fluorTransform",a=0,b=(1/150),c=0)
    draw2dgate<-function(flowframe,ychannel,xchannel,maxevents){
        yrange<-c(range(flowframe)[1,ychannel],range(flowframe)[2,ychannel])
        xrange<-c(range(flowframe)[1,xchannel],range(flowframe)[2,xchannel])
        plot(exprs(flowframe)[1:maxevents,xchannel],exprs(flowframe)[1:maxevents,ychannel],pch=".",ylim=yrange,xlim=xrange,xlab=xchannel,ylab=ychannel)
        tmp<-locator(type='l', col=2)
        mat<-cbind(tmp$x,tmp$y)
        colnames(mat)<-c(xchannel,ychannel)
        return(mat)}

======================

# Before you start
 
You first need to install the actual program R.  [This page](http://a-little-book-of-r-for-biomedical-statistics.readthedocs.org/en/latest/src/installr.html) has a great set of instructions.  

The packages used to analyze flow data are part of a set called Bioconductor.  To install Bioconductor, open the R console and type in the following lines: 

    source("http://bioconductor.org/biocLite.R")
    biocLite()

This installs a core set of Bioconductor packages. 

You now need to install the packages flowCore and flowViz. 

    biocLite("flowCore")
    biocLite("flowViz")

You only need to install these packages once, but have to load them every time you need to use them, by using the 'library' command: 

    library(flowCore)
    library(flowViz)

While working in R, please take note of the following rules: 

- Capitalization matters; 'flowcore' is not the same as 'flowCore'
- R does not work well with file names that include spaces; avoid these whenever possible.
