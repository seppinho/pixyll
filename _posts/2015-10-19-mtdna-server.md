---
layout:     post
title:      Hadoop Services for Everyone using Cloudgene and Docker
date:       2015-10-19 16:58:21
published: false
categories: cloudgene docker hadoop bioinformatics
---
This posts explains how you can register Hadoop applications to Cloudgene to manage and execute workflows. Two previous posts explained how we developed a prebuild [Hadoop Docker Image](http://seppinho.github.io/docker/hadoop/2015/08/26/docker-hadoop/) for Cloudera CDH5 and a Docker Image for our workflow system [Cloudgene](http://seppinho.github.io/cloudgene/hadoop/2015/08/27/cloudgene/). 

### Docker + Cloudgene = Hadoop Services 4 Everyone!
Genetics needs scalable services to manage and analyse the huge amount of data. For that, we think Hadoop is a perfect fit.  Nevertheless, a way is needed to abstract all the technical stuff from end users. For that reason, Lukas Forer and I developed [Cloudgene](http://seppinho.github.io/cloudgene/hadoop/2015/08/27/cloudgene/), a system which allows us to combine different of our applications (apps) with Cloudgene and provide them as web services to everyone. Even if the installation process of Cloudgene is easy (Thanks to Restlet on server side), (http://seppinho.github.io/docker/hadoop/2015/08/26/docker-hadoop/) a Hadoop Cluster is something simplified our life a lot more!
So the for beginners non trivial task is how can a application be combined with Cloudgene? The answer is quite simple, to combine a new Hadoop application with Cloudgene the two most important requirements are:
- You are aware (or developed your own) Hadoop application (e.g. MapReduce, Spark). This application is executable on the command line (e.g. hadoop jar wordcount.jar <in> <out>). Also a combination of several apps (e.g. MapReduce, Spark, Unix Tool, R) to a workflow is possible.  
- You know the basics of the Cloudgene Workflow Language developed by  [Lukas](www.forer.it) to connect your app to Cloudgene (also mentioned [here](https://github.com/pditommaso/awesome-pipeline)). A simple example (again Wordcount) has already been introduced [in the previous post](http://seppinho.github.io/cloudgene/hadoop/2015/08/27/cloudgene/). If you don't want to learn the YAML syntax but keen to integrate it into Cloudgene, please contact[us](http://seppinho.github.io/about/).

### Pull Cloudgene
Cloudgene with all dependencies (e.g. Hadoop, R) is provided as an automated build from Docker Hub.
{% highlight bash %}
docker pull seppinho/cloudgene-docker
{% endhighlight %}

### Application Registration
We prepared an [app repository](https://github.com/seppinho/cloudgene-apps-docker) including two sample applications. This  allows us to register different repositories (including several apps) making each Cloudgene installation user specific. As mentioned, in this repository Wordcount and mtDNA-Server is included. Specify your own repository with the --repository command line option.

### Start Cloudgene on Docker
Running this command will (a) configure Hadoop in pseudo-distributed mode, (b) install Cloudgene and all dependencies and (c) mount the repository. When accessing the web interface (http://localhost:8082), apps can now be managed and run graphically.
{% highlight bash %}
sudo docker run --privileged -it -p 8082:8082 seppinho/cloudgene-docker \ --repository https://github.com/seppinho/cloudgene-apps-docker
{% endhighlight %}


### Cloudgene in Real Life
Cloudgene is the underlying framework for the [Michigan Imputation Server](https://imputationserver.sph.umich.edu/) and is now in production since 1 1/2 years. We [imputed](http://genome.sph.umich.edu/wiki/Minimac3) over 1.4M Genomes and improved Cloudgene a lot to provide a failsafe service to everyone. 

If you are interested to integrate your use case into Cloudgene, please let [Lukas](www.forer.it) and [me](http://seppinho.github.io/about/) know.
