---
layout:     post
title:      Hadoop Services for Everyone using Cloudgene and Docker
date:       2015-10-19 16:58:21
published: false
categories: cloudgene docker hadoop bioinformatics
---

In my last two posts I explained how to build a [Hadoop Docker Image](http://seppinho.github.io/docker/hadoop/2015/08/26/docker-hadoop/) for Cloudera (MRv1 and MRv2) and introduced our [Hadoop-As-A-Service approach](http://seppinho.github.io/cloudgene/hadoop/2015/08/27/cloudgene/) named Cloudgene.

### Docker + Cloudgene = Hadoop Services for Everyone!
In this post I'll explain how a Hadoop application can be integrated into Cloudgene and started as a service. I'll demonstrate that on two applications: The already introduced Hadoop Wordcount example and one of our genetic services, called mtDNA-Server. mtDNA-Server is a service to check Next Generation Sequencing data for heteroplasmies and contamination.

So two combine an application with Cloudgene the two most important requirements are:
- You have a Hadoop application which is already executable on the command line (e.g. the Wordcount jar file)
- You know the basics of the Cloudgene workflow language to connect your app to Cloudgene. A simple example has already been shown [in my previous post](http://seppinho.github.io/cloudgene/hadoop/2015/08/27/cloudgene/)

### Pull Cloudgene
Cloudgene with all dependencies is provided via an automated build on Docker Hub.
{% highlight bash %}
docker pull seppinho/cloudgene-docker
{% endhighlight %}

### Connect an Application to Cloudgene
We prepared an [app repository](https://github.com/seppinho/cloudgene-apps-docker) including two sample applications. This feature allows us to combine Cloudgene with different repositories and we can combine applications as we want. In this repository Wordcount and mtDNA-Server is included. We implemented the --repository command line option to do so.

### Start Cloudgene on Docker
Running this command (a) Hadoop is configured, (b) Cloudgene and all dependencies (e.g. R Cran) installed and (c) a repository is mounted automatically. When accessing the web interface, both apps can be run via the GUI.
{% highlight bash %}
sudo docker run --privileged -it -p 8082:8082 seppinho/cloudgene-docker \ --repository https://github.com/seppinho/cloudgene-apps-docker
{% endhighlight %}


### Does it scale?
Cloudgene is the underlying framework for the Michigan Imputation Server and is now in production since over a year. We imputed over 1.4M Genomes and improved Cloudgene a lot to provide failsafe services to everyone. If you are interested to integrate your use case into Cloudgene, please let [Lukas](www.forer.it) and [me](http://seppinho.github.io/about/) know.
