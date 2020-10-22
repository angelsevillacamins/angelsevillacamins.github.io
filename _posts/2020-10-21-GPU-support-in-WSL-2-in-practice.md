---
layout: post
title: GPU support in WSL 2 in practice Jupyter notebooks and Rstudio working seamlessly with a GPU using docker containers
---
## Summary
If you are reading this blog, probably you are wondering whether a GPU can be shared by Windows. This is a real problem because in virtual machines hosted on Windows, GPU support doesn’t work properly or it’s really hard to set up.

Even docker cannot use GPUs in Linux containers running in Windows as host. The only real solution if you want to run GPU-based code in a Linux container in Windows is literally getting rid of Windows; meaning, having a dual boot with a Linux distribution and run it there. If this is your case, you should continue reading this blog.

**If you are already a WSL 2 user, additional improvements over the standard installation are described as automated docker initialization and Linux distros export to avoid reinstallation of standard programs.**

Moreover, a docker image was developed with both Jupyter notebooks and Rstudio able to use Tensorflow and Keras with a GPU if available. Furthermore, it will be shown that both R and Python installations can be used seamlessly by both UIs without additional configuration including GPU support. Finally, some caveats will be described, such as GPU support not working for latest Windows insider build (20231) and a decrease in performance.

The custom Docker image and its Dockerfile can be found [here](https://hub.docker.com/r/angelsevillacamins/gpu-py3-jupyter-rstudio) and [here](https://github.com/Anchormen/wsl2-gpu) respectively.

See [here](https://anchormen.nl/blog/data-science-ai/guide-wsl2-configuration-gpu-support/) the complete blog post.