---
layout:     post
title:      Cloudgene, a Hadoop As-A-Service approach
date:       2015-08-27 23:08:21
categories: cloudgene hadoop
---

Already some years  [ago](http://www.biomedcentral.com/1471-2105/13/200/abstract), my colleague [Lukas Forer](http://www.forer.it) and I developed a platform to simplify the complete lifecycle of a Hadoop program. This includes steps like putting data into HDFS, execute a MapReduce job from the command line or export data back to the local file system. These steps are of course doable with some basic Unix knowledge. Nevertheless, for people who are used to work with graphical interfaces, this can be a major barrier to discover the beauty of Hadoop. For example, a typical MapReduce command looks like this:

{% highlight bash %} 
sudo -u cloudgene hadoop jar hadoop-examples.jar wordcount input output
{% endhighlight %}

### Introducing Cloudgene

To abstract this command, we developed [Cloudgene](http://cloudgene.uibk.ac.at) consisting of (a) a workflow system and (b) a cloud orchestration platform. The idea behind Cloudgene is quite simple: If you are able to execute your Hadoop program on the command line, take some minutes and write a YAML configuration to connect your program with Cloudgene. With some basic text lines you are able transform your Hadoop command line program into a web-based service, present your collaborators a scalable best-practices workflow and provide reproducible science.
A typical YAML configuration file looks like this. Please find the complete working Hadoop example [here](https://github.com/seppinho/mapreduce).
{% highlight yaml %} 
name: WordCount
description:  MapReduce-WordCount 
version: 1.0
website: http://hadoop.apache.org/

mapred:
  steps:
    - name: Wordcount
      jar: Examples.jar 
      params: mapreduce.wordcount.WordCountSimple $input $output
      
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
Cloudgene simplified our lives a lot in the last years, and two very recent services based on Cloudgene show the success of our platform: The first service is the [mtDNA-Server](http://mtdna-server.uibk.ac.at), a heteroplasmy and contamination pipeline for next generation sequencing data developed by my colleague [Hansi Weißenteiner](haplogrep.uibk.ac.at). The other one is the quite popular [Michigan Imputation Server](http://imputationserver.sph.umich.edu) for genome imputation. 
For now, check out one of the web services to get a feeling what Cloudgene can do for you. The services will be introduced in richer detail in near future

In the next post, I'll show you how you can combine the ideas of my [first](http://seppinho.github.io/docker/hadoop/2015/08/26/docker-hadoop/) blog post (Hadoop Docker Image) with Cloudgene resulting in a local Hadoop-As-A-Service approach.
