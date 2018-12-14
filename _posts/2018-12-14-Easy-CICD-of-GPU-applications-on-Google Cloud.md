---
layout: post
title: Easy CI/CD of GPU applications on Google Cloud including bare-metal using Gitlab and Kubernetes
---
## Summary
Are you a data scientist who only wants to focus on modelling and coding and not on setting up a GPU cluster? Then, this blog might be interesting for you. We developed an automated pipeline using gitlab and Kubernetes that is able to run code in two GPU environments, GCP and bare-metal; no need to worry about drivers, Kubernetes cluster creation or deletion. The only thing that you should do is to push your code and it runs in a GPU!
Source code for both the custom Docker images and the Kubernetes objects definitions can be found [here](https://github.com/Anchormen) and [here](https://hub.docker.com/u/angelsevillacamins) respectively.
See [here](https://anchormen.nl/blog/data-science-ai/gpu-applications-on-google-cloud/) the complete blog post.