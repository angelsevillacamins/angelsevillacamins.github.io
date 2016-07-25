---
layout: post
title: Spark, RStudio and Shiny servers in a docker cluster hosted by Carina
---
## Summary
The objective of this blog is demonstrate that the integration of a Spark master node, RStudio and Shiny servers is possible in a docker image. Moreover, an indefinite number of Spark worker nodes can be deployed using the same image. Furthemore, a toy example of a Shiny application powered by SparkR is included.

## Introducction

### SparkR

SparkR is an R package designed to use Apache Spark from the R command line allowing distributed computations on large datasets. Importantly, the distributed machined learning library MLlib can be utilized in SparkR. For training proposes, it can be run in "standalone mode", which means using a single node, probably your own computer. 

My personal experience is that not all the programs or applications developed in standalone mode will work in a fully integrated cluster mode. Therefore, SparkR should be deployed in a cluster to obtain its full potential. 

It is interesting to mention that the deployment Spark has been previosly described on Digital Ocean ([here](http://www.infolace.com/blog/2015/02/27/create-an-ad-hoc-spark-cluster/)), EC2 (see [here](http://spark.apache.org/docs/latest/ec2-scripts.html)), Google cloud (see [here](https://cloud.google.com/dataproc/)) or Azure (see [here](https://blog.sixeyed.com/spark-on-azure-big-data-made-easy/)). Moreover, the integration of SparkR and Rstudio on AWS EC2 has been deeply desribed [here](http://www.r-bloggers.com/launch-apache-spark-on-aws-ec2-and-initialize-sparkr-using-rstudio/) and even using SparkR to power shiny applications [link](www.r-bloggers.com/using-apache-sparkr-to-power-shiny-applications-part-i). 

I would like to highlight the last two blogs, since they have been an important inspiration for this blog. The problem implementing SparkR on a cluster envioment such as AWS EC2 is that a deep knowledge of cluster deployment is needed and installing Spark is not straighfowrd.

### Docker

A potential solution is Docker, an open source project to deploy automatically applications into  "containers". These containers are based on images which contain a root file system and several execution parameters to constitute an independent virtualized operating system. From the docker [web site](https://docs.docker.com): "The concept is borrowed from Shipping Containers, which define a standard to ship goods globally. Docker defines a standard to ship software". In this [link](http://code.markedmondson.me/setting-up-scheduled-R-scripts-for-an-analytics-team/), an example of using a dockerized RStudio Server can be found. 

### Carina

Even though AWS, Google Cloud, Microsoft Azure and others providers offer interesting quotes, it could be better if SparkR can be run in a cloud environment for free. Carina is a docker environment based on Docker Swarm and it can be used to deploy an application using docker containers in a cluster. Each cluster of Carina is composed by 3 nodes with a memory capacity of 4 GB and 12 vCPUs each, thus, every cluster has total 12 GBs of RAM memory and 36 vCPUs. Carina offers free accounts at the time when this file was written (20/07/2016). For more details, go to the Carina [web site](https://getcarina.com).

### One process vs one application per container
Docker strongly advices one process per container rule, however, there is a tendency to use multiple services in one container moving to "one application per container" rule (see [this](https://blog.phusion.nl/2015/01/20/baseimage-docker-fat-containers-treating-containers-vms/) blog). To handle the multiple service pero container, the application supervisor can be used and even it is described in the Docker web site [here](https://docs.docker.com/engine/admin/using_supervisord/). 

Moreover, this technology has been used to deploy a Spark server cluster composed of a master node and an indefinite number of slave nodes [here](https://www.anchormen.nl/spark-docker/). This last application has been fundamental for the development of our image and the Spark server. 

Furthemore, RStudio and Shiny servers can be hosted simultaneously in the same cluster to test our SparkR applications and even publish them. To our knowledge, there is no other docker image able to integrate Spark, RStudio and Shiny servers. Futhemore, we did't find any other free alternative as we propose in this blog using Carina.

## Getting started

To get started in 15 minutes, follow the next instructions. For a more detailed description, go [here](https://github.com/angelsevillacamins/spark-rstudio-shiny/wiki/spark-rstudio-shiny-docker-image-in-detail).

1. Sign up for the Carina Beta [here](https://app.getcarina.com/app/signup).

2. Create a Carina cluster and scale up to **3 nodes**

3. Connect to your Carina cluster as explained in [here](https://getcarina.com/docs/getting-started/getting-started-on-carina).
If everything has run smoothly, you should see something like this after the `docker info` command:

  
  ```
$ docker info
  Containers: 5
   Running: 3
   Paused: 0
   Stopped: 2
  Images: 5
  Server Version: swarm/1.2.0
  Role: primary
  Strategy: spread
  Filters: health, port, dependency, affinity, constraint
  Nodes: 1
   1dba0f72-75bc-4825-a5a0-b2993c535599-n1: 172.99.70.6:42376
    └ Status: Healthy
    └ Containers: 5
    └ Reserved CPUs: 0 / 12
    └ Reserved Memory: 0 B / 4.2 GiB
    └ Labels: com.docker.network.driver.overlay.bind_interface=eth1, executiondriver=, kernelversion=3.18.21-2-rackos, operatingsystem=Debian GNU/Linux 7 (wheezy) (containerized), storagedriver=aufs
    └ Error: (none)
    └ UpdatedAt: 2016-05-27T19:27:24Z
    └ ServerVersion: 1.11.2
  ```

4. Run the following commands:

