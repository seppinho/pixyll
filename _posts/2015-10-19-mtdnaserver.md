---
layout:     post
title:      Hadoop Services for Everyone using Cloudgene and Docker
date:       2015-10-19 16:58:21
categories: cloudgene docker hadoop bioinformatics
---

Hadoop is pretty famous for analysing huge datasets in batch (MapReduce) or in-memory (Spark). To abstract all the technical things (e.g. setting up a cluster, executing/managing Hadoop programs, HDFS Staging) from end users, [Lukas](http://www.forer.it) and I developed the Hadoop workflow system Cloudgene, introduced in [this blog entry](http://seppinho.github.io/cloudgene/hadoop/2015/08/27/cloudgene/). 
Even if the installation process of Cloudgene is quite doable, the prerequiste of having a running Hadoop Cluster is kind of a shortcoming. As a first step to solve this, we generated a [Hadoop Docker Image](http://seppinho.github.io/docker/hadoop/2015/08/26/docker-hadoop/) to set up a CDH5 cluster in pseudo-distributed mode. This image can be combined with Clodugene as showed here:
