---
title: "Addressing domain adaptation in few shot learning"
excerpt: ""
collection: projects
---
[Code link](https://github.com/jeetkanjani7/CloserLookFewShot)
=============
The problem of learning to generalize from limited examples at test time is referred to as few shot learning. 
Although, there have been few shot learning algorithms which have reported performance better than the state of the art, there is a lack of domain shift between the source and target domain as the novel classes used in those cases are sampled from the same dataset. This makes the current evaluation numbers flawed.

Using distance metric in baseline methods gives suprisingly good results compared to state of the art meta learning methods even when source and target datasets are sampled from the same dataset.

Furthermore, when there is a significant domain shift between source and target domain - the meta learning algorithms are inferior even to the baseline methods, highlighting the importance of learning to adapt to domain differences in few shot learning.

The meta learning algorithms tested are MatchingNet, ProtoNet, RelationNet and MAML. 