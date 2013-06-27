flow-cytometry-using-R
======================

This document will be made up of a couple of parts: [Part I](https://github.com/sbabovic/flow-cytometry-using-R/blob/master/README.md#part-i) and [Part II](https://github.com/sbabovic/flow-cytometry-using-R/blob/master/README.md#part-ii).

### Part I 

First you need to set your working directory and load the libraries flowCore and flowViz. 

    setwd('/Users/sonja/Desktop/20130618 Post-transplant cycling')
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
