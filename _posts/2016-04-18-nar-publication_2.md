---
layout:     post
title:      NAR WebServer Issue Publication - mtDNA-Server
date:       2016-04-18 23:00:21
categories: mtdna
---

Providing Hadoop as a Service is the main goal of Cloudgene, as described in one of my previous [blog entries](http://seppinho.github.io/cloudgene/hadoop/2015/08/27/cloudgene/). 
Since Cloudgene is only the platform, useful use cases need to be implemented and integrated in Cloudgene. 
Here I want to introduce our newest service called **mtDNA-Server**, which have been published in the **NAR WebServer Issue 2016**.

## mtDNA-Server 101
mtDNA-Server provides a free service for the analysis of human mitochondrial DNA data, currently focusing on reliable
identification of heteroplasmy (>= 1%) and contamination.

Even if the task itself is quite straightforward (there are quite a few analysis pipelines out there) many traps are waiting for end users.
Therefore, mtDNA-server (a) helps user to avoid such traps, (b) provides all data files including an interactive web report for download 
and (c) suggests postprocessig guidlines for downstream analysis.

We think that this will be, similar to HaploGrep, a very useful
resource for researchers. Right now (May 2016), over **11k samples** have already been analysed.

### mtDNA-Server Main Features
- Upload data as FASTQ (SE/PE) or SAM/BAM
- Parallel MapReduce alignment of your data
- Heteroplasmy detection 
- Contamination identification 
- Haplogroup assignment with [HaploGrep2](http://seppinho.github.io/mtdna/2016/04/17/nar-publication/)
- Variant annotation
- Quality control metrics

### mtDNA-Server in Action
So just give it a [try](https://mtdna-server.uibk.ac.at) and check out the paper [here](http://nar.oxfordjournals.org/content/early/2016/04/15/nar.gkw247).
