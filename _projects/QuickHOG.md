---
title: "QuickHOG: Real time pedestrian detection"
excerpt: ""
collection: projects
---
[Code link](https://github.com/jeetkanjani7/QuickHOG)
===========

1 Abstract
==========
We introduce a parallel implementation of the histogram of oriented gradients
algorithm for object detection. Our implementation uses the GPU and the
NVIDIA CUDA framework. Our implementation is END to END which makes
us able to get a running time improvement of 86X over the standard sequential
implementation[1] and 1.2X over fastHOG[2]. The purpose is to implement it
on OxSight SmartSpecs used by the visually impaired.

2  Introduction
===============
There have been many papers on the HOG approach for linear classification
before the introduction of deep neural networks. The significant papers which
proposed a good running time improvements are [2] and [3]. While [3] uses the
cheaper and more easily implemented bilinear interpolation, we mirror [1] by
using trilinear interpolation for binning. While[2] uses trilinear interpolation,
the algorithm flow makes an expensive step of copying data back to the CPU
in between which is overcomed in our implementation.

3 HOG Descriptor
================
The histogram of oriented algorithm for object detection was introduced in [1].
The HOG detector is a sliding window algorithm. This means that for any given
image a window is moved across at all locations and scales and a descriptor is
computed. For that window a pretrained classifier is used to assign a matching
score to the descriptor. The classifier used is a linear SVM classifier and the
descriptor is based on histograms of gradient orientations. Firstly the image is
padded and a gamma normalization is applied. Padding means that extra rows
and columns of pixels are added to the image. Each new pixel gets the color of its
closest pixel from the original image. This helps the algorithm deal with the case
when a person is not fully contained inside the image. The gamma normalization
has been proven to improve performance for pedestrian detection [1] but it
may decrease performance for other object classes. To compute the gamma
1
correction the color for each channel is replaced by its square root. Gradient
orientations and magnitude are obtained for each pixel from the preprocessed
image. If a color image is used the gradient with the maximum magnitude
(and its corresponding orientation) is chosen. This is done by convoluting the
image with the 1-D centered kernel [-1 0 1] by rows and columns. Several other
techniques have been tried (including 3x3 Sobel mask or 2x2 diagonal masks)
but the simple 1-D centered kernel gave the best performance (for pedestrian
detection). Each detection window is divided into several groups of pixels,
called cells. For each cell a histogram of gradient orientations is computed.
For pedestrian detection the cells are rectan- gular and the histogram bins are
evenly spaced between 0 and 180 degrees. The contribution of each pixel to the
cell histogram is weighted by a Gaussian centered in the middle of the block
and then interpolated trilinearly in orientation and position. This has the effect
of reducing aliasing. For more details on the interpolating see [1]. Multiple
cells are grouped into blocks, with each cell being part of multiple blocks. Each
block will therefore contain multiple cell histograms. Each block histogram is
normalized. For pedestrian detection the L2-Hys norm [3] is used (the L2-norm
followed by clipping to 0.2 and renormalizing. All the blocks inside a detection
window form a HOG descriptor. This is used as input for a pretrained linear
SVM classifier. For people detection the best results have been achieved using
16x16 pixel blocks containing 2x2 cells of 8x8 pixels. The block stride is 8 pixels
(one cell) so the histogram of a cell is normalized over 4 blocks. Each histogram
has 9 bins. The Gaussian used for weighting pixel values has = 8. The detection
window is 64x128. The scale ratio is 1.05. Finally an algorithm based on mean
shift is used to fuse the detections over the 3D position and scale space.

4 GPGPU and the NVIDIA CUDA
===========================
We use 3,749,760 threads to compute the linear SVM evaluation for a single
1920x1080 image. The bottleneck in a CUDA application is often global memory
access, rather than mathematical computations, which are essentially free. The
speed of the memory access is also affected by the thread memory access pattern.
If memory accesses are coalesced, that is if threads in the same multiprocessor
access consecutive memory locations, fewer memory operation will be required,
so speed will be considerably high. The algorithm being memory bandwidth
limited, the link between GPU and CPU(PCIe or NVLink) plays a crucial role
in determining the running time of the algorithm. The running times were
tested on NVIDIA Geforce GTX 950M with 640 CUDA cores and PCI Express
for CPU connectivity with a memory bandwidth of the order of 3 GB/s for our
system. This bandwidth is less for the SmartSpecs and hence the improvements
over [2] would be significantly High.

5 Algorithm
===========
![Quick HOG steps](./images/QuickHOG.png)