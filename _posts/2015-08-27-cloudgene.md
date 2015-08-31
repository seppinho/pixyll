---
layout:     post
title:      Cloudgene, a Hadoop-As-A-Service approach
date:       2015-08-27 23:08:21
categories: cloudgene hadoop
summary: This post introduces the graphical Hadoop platform Cloudgene and shows how simple a Hadoop command line program (or a workflow of several programs) can be provided as a web service to everyone. Two services in Genetics based on Cloudgene are already available and showing promising success.
---

Already some years [ago](http://www.biomedcentral.com/1471-2105/13/200/abstract), my colleague [Lukas Forer](http://www.forer.it) and I developed a platform to simplify the complete lifecycle of a Hadoop program. This includes steps like putting data into HDFS, execute a MapReduce job from the command line or export data back to the local file system. These steps are of course doable with some basic Unix knowledge. Nevertheless, for people who are used to work with graphical interfaces or want to combine several tools (Hadoop, Spark, Unix, R) to a workflow, this can be a major barrier to discover the beauty of Hadoop. 
The simpliest possible MapReduce command looks like this:

{% highlight bash %} 
hadoop jar hadoop-examples.jar wordcount input output
{% endhighlight %}

### Introducing Cloudgene

To abstract this command we developed [Cloudgene](http://cloudgene.uibk.ac.at), consisting of (a) a workflow system (including the workflow definition language [WDL](http://cloudgene.uibk.ac.at/developer-guide/)) and (b) a cloud orchestration platform. The idea behind Cloudgene is quite simple: If you are able to execute your Hadoop program on the command line, take some minutes and write a YAML configuration to connect your program with Cloudgene. Doing so, you are able to transform your Hadoop command line program (or a set of programs) into a web-based service, present your collaborators a scalable best practices workflow and provide reproducible science.
The YAML configuration for the command above looks like this:
{% highlight yaml %} 
name: WordCount
description:  MapReduce-WordCount 
version: 1.0
website: http://hadoop.apache.org/

mapred:
  steps:
    - name: Wordcount
      jar: hadoop-examples.jar
      params: $input $output
      
  inputs:
    - id: input
      description: Input
      type: hdfs-folder
      
  outputs:
    - id: output
      description: Output
      type: hdfs-folder
      removeHeader: false
      download: true
{% endhighlight %}  

### Cloudgene in Action
Cloudgene simplified our lives a lot in the last years, and two very recent services based on Cloudgene show the success of our platform: The first service is the [mtDNA-Server](http://mtdna-server.uibk.ac.at), a heteroplasmy and contamination pipeline for next generation sequencing data developed by my colleague [Hansi Weißenteiner](http://haplogrep.uibk.ac.at). The other one is the quite popular [Michigan Imputation Server](https://imputationserver.sph.umich.edu) for genome imputation based on [minimac3](http://genome.sph.umich.edu/wiki/Minimac3). 

For now, check out one of the web services to get a feeling what Cloudgene can do for you. The services will be introduced here in near future.

In the next post, I'll show you how to combine the ideas of my [first](http://seppinho.github.io/docker/hadoop/2015/08/26/docker-hadoop/) blog post with Cloudgene resulting in a Hadoop-As-A-Service approach for local usage.
