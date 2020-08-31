---
title: "Convex Optimization"
excerpt: "parallel implementation of Non Maximum suppression<br/><img src='/images/nms.png'>"
collection: projects
---
Well, I was looking at SVM and found that classifying your training set using  SVM  deals with optimization problem under constraints:

yi (W.xi +b) > 0 for data to respect hyperplane/Margin.

and min ||w||

as ||w|| = 2/m and the margin has to be maximized! A simple derivation of that: