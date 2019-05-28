# Tensorflow Retrieval Baseline
This repository provides a retrieval/space embedding baseline using multiple retrieval datasets and ranking losses. 

This code is based on  [triplet-reid](https://github.com/VisualComputingInstitute/triplet-reid) repos.

Evaluation Metrics: Normalized Mutual Information (NMI), Recall@K

### Deep Fashion In-shop retrieval datasets
All the following experiments assume a training mini-batch of size 60. The architecture employed is the one used in [In Defense of the Triplet Loss for Person Re-Identification](https://arxiv.org/abs/1703.07737) but ResNet is replaced by a DenseNet169

| Method    | Normalized | Margin | NMI   | R@1   | R@4   | # of classes | #samples per class |
|-----------|------------|--------|-------|-------|-------|--------------|--------------------|
| Semi-Hard | Yes | 0.2    | 0.902 | 87.43 | 95.42 | 10| 6|
| Lifted Structured | No | 1.0    | 0.903 | 87.32 | 95.59 | 10| 6|