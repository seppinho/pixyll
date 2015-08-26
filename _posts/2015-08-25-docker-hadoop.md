---
layout:     post
title:      Creating a Docker Image for Cloudera Hadoop MapReduce (CDH5)
date:       2015-08-26 09:00:21
categories: docker hadoop
---
There are many ways how Docker can be used. In this blog post I'll summarize the steps I did to create a running Docker image for the Cloudera Version (CDH5) of Hadoop. It runs in pseudo-distributed mode which means that all Hadoop services are running on the same node. This tutorial requires a running Docker service on your system.

## Ready-to-use image
- Before we start, you can of course easily use my Docker image, run Hadoop MapReduce jobs and skip the rest of the steps.  

{% highlight shell %}
docker pull seppinho/cdh5-hadoop-mrv1:latest
docker run -it -p 50030:50030 seppinho/cdh5-hadoop-mrv1:latest
sh /usr/bin/execute-wordcount.sh
{% endhighlight %}

## Step by step tutorial
- Start by pulling a fresh Docker Ubuntu image and run a new container for a quick test. A container is basically a running instance of an image.

{% highlight shell %}
docker pull ubuntu:14.04
docker run -i -t ubuntu:14.04
{% endhighlight %}


- Now, back on your local OS (type 'exit' to close the Ubuntu container from before) create a new folder including an empty Dockerfile. The Dockerfile includes all commands which should be executed when creating a new image. If you want to use [my Dockerfile](https://github.com/seppinho/cdh5-hadoop-mrv1/blob/master/Dockerfile) you also have to copy the `conf directory` which can be found [here](https://github.com/seppinho/cdh5-hadoop-mrv1). This also includes some other stuff (CMD, COPY) which will be introduced in a separate blog post.

{% highlight shell %}
mkdir new-docker-image
mkdir new-docker-image/conf
# copy files as mentioned above
cd new-docker-image
touch Dockerfile
edit Dockerfile
{% endhighlight %}

- When you are satisfied with your Dockerfile you can now build your first image. Just execute the following command in your image directory. Every time your Dockerfile has been changed, re-run the `build` command.

{% highlight shell %}
docker build --no-cache=false -t hadoop-image .
docker run -i -t -p 50030:50030  hadoop-image
{% endhighlight %}

- You should now be able to connect to http://localhost:50030 from your local OS or execute a job on the command line like this:

{% highlight shell %}
sh /usr/bin/execute-wordcount.sh
{% endhighlight %}

In the next blog post, I'll show how our Hadoop platform [Cloudgene](http://cloudgene.uibk.ac.at) uses such an image for an easy installation and execution process.
