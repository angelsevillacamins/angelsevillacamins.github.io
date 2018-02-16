---
layout: post
title: Affordable automatic deployment of Spark and HDFS with Kubernetes and Gitlab CI/CD
---
## Summary
Running an application on Spark with external dependencies, such as R and python packages, requires the installation of these dependencies on all the workers. To automate this tedious process, a continuous deployment workflow has been developed using Gitlab CI/CD. This workflow consists of: (i) Building the HDFS and Spark docker images with the required dependencies for workers and the master (Python and R), (ii) deploying the images on a Kubernetes cluster. For this, we will be using an affordable cluster made of mini PCs. More importantly, we will demonstrate that this cluster is fully operational. The Spark cluster is accessible using Spark UI, Zeppelin and R Studio. In addition, HDFS is fully integrated together with Kubernetes. Source code for both the custom Docker images and the Kubernetes objects definitions can be found [here](https://hub.docker.com/r/angelsevillacamins) and [here](https://github.com/Anchormen/spark-hdfs-on-kubernetes) respectively.

Go [here](https://anchormen.nl/blog/big-data-services/spark-and-hdfs-with-kubernetes/) to read the entire blog.