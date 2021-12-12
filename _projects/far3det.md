---
title: "Far3Det"
excerpt: "Towards Far field 3D detection"<br/><img src='/images/far3det.png'>"
collection: projects
---
[Project Page](https://mscvprojects.ri.cmu.edu/2021teamf/)
===========



**Overview**
We focus on the task of far-field 3D detection (Far3Det), the 3D detection of objects beyond a certain distance from an observer, e.g., >50m. Far3Det is particularly important for autonomous vehicles (AVs) operating at highway speeds, which requires the detection of far-field obstacles to ensure sufficient braking distances. We first point out that existing AV benchmarks (e.g., nuScenes and Waymo) underemphasize this problem since they evaluate performance only up to a certain distance (50m). One reason is that obtaining ground-truth far-field 3D annotations is difficult, particularly for LiDAR sensors that may produce only a few sparse returns for far-away objects. However, contemporary RGB cameras are much higher-resolution and capture stronger far-field signatures, motivating our exploration of LiDAR and RGB fusion for Far3Det. To do so, we derive high-quality far-field annotations for standard benchmarks. We demonstrate that simple distance-based late fusion of LiDAR and RGB detections significantly improves the state-of-the-art. Our results challenge the conventional wisdom that active LiDAR outperforms passive RGB for 3D understanding; once one looks far enough “out”, high-resolution passive imaging can be more effective.

**Contributions**
We derive an initial dataset for the problem of far-field 3D object detection (Far3Det) and perform an empirical evaluation of baseline algorithms on it. One salient conclusion is that RGB cameras can be more effective in the far-field. We revisit various late-fusion strategies for multimodal detection and find that simple fusion (that applies different fusion strategies for detections at different ranges) can produce significant improvements.
We hope our work will encourage further research on Far3Det.