---
layout:     post
title:      Hadoop Services for Everyone using Cloudgene and Docker
date:       2015-10-19 16:58:21
published: false
categories: cloudgene docker hadoop bioinformatics
---

Genetics needs scalable services to manage and analyse the huge amount of data. We think that Hadoop is a perfect fit for that.  To abstract all the technical stuff from end users, Lukas Forer and I developed [Cloudgene](http://seppinho.github.io/cloudgene/hadoop/2015/08/27/cloudgene/). This system allows us to combine a set of applications (apps) with Cloudgene and provide the workflows as web service to everyone. Even if the installation process of Cloudgene is quite doable, the prerequiste of having a runningHadoop Cluster is kind of a shortcoming. For that, we developed a [Hadoop Docker Image](http://seppinho.github.io/docker/hadoop/2015/08/26/docker-hadoop/).

## Connecting new apps to Cloudgene
So for end users, the most interesting question is how a application can be combined with Cloudgene. To do so, two things are important:
- You are aware (or developed your own) Hadoop application (e.g. MapReduce, Spark). This application is executable on the command line (e.g. hadoop jar wordcount.jar <in> <out>). Also a combination of several apps (e.g. MapReduce, Spark, Unix Tool, R) to a workflow is possible.  
- You know the basics of the Cloudgene Workflow Language developed by  [Lukas](www.forer.it) to connect your app to Cloudgene (also mentioned [here](https://github.com/pditommaso/awesome-pipeline)). A simple example (again the famous Wordcount) has been introduced [in this previous post](http://seppinho.github.io/cloudgene/hadoop/2015/08/27/cloudgene/). If you don't want to learn the YAML syntax but keen to integrate your app into Cloudgene, please contact [us](http://seppinho.github.io/about/).

### Cloudgene + Docker = Hadoop Services 4 Everyone
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
