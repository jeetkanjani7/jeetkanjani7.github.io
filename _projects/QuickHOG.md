---
title: "QuickHOG: Real time pedestrian detection"
excerpt: "<br/><img src='/images/QuickHOG.png'  height='500' width='500'>"
collection: projects
---

We introduce a parallel implementation of the histogram of oriented gradients
algorithm for object detection. Our implementation uses the GPU and the
NVIDIA CUDA framework. Our implementation is END to END which makes
us able to get a running time improvement of 86X over the standard sequential
[implementation](https://lear.inrialpes.fr/people/triggs/pubs/Dalal-cvpr05.pdf) and 1.2X over [fastHOG](http://www.robots.ox.ac.uk/~lav/Papers/prisacariu_reid_tr2310_09/prisacariu_reid_tr2310_09.html). The purpose is to implement it
on OxSight SmartSpecs used by the visually impaired.

[Code](https://github.com/jeetkanjani7/QuickHOG) [Paper](https://jeetkanjani7.github.io/files/QuickHOG.pdf)
===========
