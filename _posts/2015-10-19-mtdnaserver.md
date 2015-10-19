---
layout:     post
title:      Hadoop Services for Everyone
date:       2015-10-19 16:58:21
categories: cloudgene docker hadoop bioinformatics
---

Hadoop is pretty famous for analysing huge datasets in batch (MapReduce) or in-memory (Spark). 

To abstract all the technical things (e.g. setting up a cluster, executing/managing Hadoop programs, HDFS Staging) from end users, [Lukas](http://www.forer.it) and I developed the Hadoop workflow system Cloudgene, introduced in [this blog entry](http://seppinho.github.io/cloudgene/hadoop/2015/08/27/cloudgene/). 
Even if the installation process of Cloudgene is quite doable, the prerequiste of having a running Hadoop Cluster is kind of a shortcoming. As a first step to solve this, we generated a [Hadoop Docker Image](http://seppinho.github.io/docker/hadoop/2015/08/26/docker-hadoop/) to set up a CDH5 cluster in pseudo-distributed mode. This image can be combined with Clodugene as showed here:

## Connecting new apps to Cloudgene
Imagine you are the developer of a new Hadoop application to analyse some kind of (big) data. Since you're not interested in beeing the guy who applys your application to all datasets, you want to present your co-workers a "do-it-yourself" service. This is exactly the job of Cloudgene. To combine your application with Cloudgene, two things are important:

- Your Hadoop (e.g. MapReduce/Spark) application is executable on the command line (e.g. hadoop jar wordcount.jar <in> <out>). You can also combine of several technologies (e.g. MapReduce, Spark, Unix Tool, R) to a Cloudgene workflow.  
- You know the basics of the [Cloudgene Workflow Language](http://cloudgene.uibk.ac.at/developer-guide/) developed by [Lukas](www.forer.it) to connect your app to Cloudgene. A simple example (again the famous (and boring) Wordcount) has been introduced [in this post](http://seppinho.github.io/cloudgene/hadoop/2015/08/27/cloudgene/). 

### Ready to deploy your application
To deploy your application, simply pull the latest Docker Image of Cloudgene with all dependencies from Docker Hub.

{% highlight bash %}
docker pull seppinho/cloudgene-docker
{% endhighlight %}

### Application Registration
We already prepared an [app repository](https://github.com/seppinho/cloudgene-apps-docker) including two sample applications (Wordcount and mtDNA-Server). This feature allows us to register different repositories (each containing several apps) making each Cloudgene installation user-specific. Specify your own repository with the --repository command line option.

### Start Cloudgene on Docker
Running this command will (a) configure Hadoop in pseudo-distributed mode, (b) install Cloudgene and all dependencies and (c) register the repository. When accessing the web interface (http://localhost:8082), applications can now be managed and run graphically. So time to simply share the link with your co-workers.

{% highlight bash %}
sudo docker run --privileged -it -p 8082:8082 seppinho/cloudgene-docker \ --repository https://github.com/seppinho/cloudgene-apps-docker
{% endhighlight %}


### Cloudgene in Real Life
Cloudgene is the underlying framework of the [Michigan Imputation Server](https://imputationserver.sph.umich.edu/) and is now in production since 1 1/2 years. We [imputed](http://genome.sph.umich.edu/wiki/Minimac3) over 1.4M Genomes and improved Cloudgene a lot to provide a stable service to everyone. 

If you are interested to integrate your app into Cloudgene, please let [me](http://seppinho.github.io/about/) know.
