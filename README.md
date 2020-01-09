# Tensorflow Retrieval Baseline
This repository provides a retrieval/space embedding baseline using multiple retrieval datasets and ranking losses. This code is based on  [triplet-reid](https://github.com/VisualComputingInstitute/triplet-reid) repos.

### Evaluation Metrics
1. Normalized Mutual Information (NMI)
2. Recall@K

### Deep Fashion In-shop Retrieval Evaluation
All the following experiments assume a training mini-batch of size 60. The architecture employed is the one used in [In Defense of the Triplet Loss for Person Re-Identification](https://arxiv.org/abs/1703.07737) but ResNet is replaced by a DenseNet169.
Optimizer: Adam, Number of iterations = 25K

| Method    | Normalized | Margin | NMI   | R@1   | R@4   | # of classes | #samples per class |
|-----------|------------|--------|-------|-------|-------|--------------|--------------------|
| [Semi-Hard](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/triplet_semihard_loss) | Yes | 0.2    | 0.902 | 87.43 | 95.42 | 10| 6|
| Hard-Negative | No | 1.0    | 0.904 | 88.38 | 95.74 | 10| 6|
| [Lifted Structured](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/lifted_struct_loss) | No | 1.0    | 0.903 | 87.32 | 95.59 | 10| 6|
| [N-Pair Loss](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/npairs_loss) | No | N/A    | 0.903 | 89.12 | 96.13 | 30| 2|
| [Angular Loss](https://github.com/geonm/tf_angular_loss) | Yes | N/A  | 0.8931 |  84.70 | 92.32 | 30| 2|
| Custom [Contrastive Loss](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/contrastive_loss) | Yes | 1.0  | 0.826 |  44.09 | 67.17 | 15| 4|

### CUB200-2011 Retrieval Evaluation
Mini-batch size=120. Architecture: Inception_Net V1.
Optimizer: Momentum. Number of iterations = 10K

| Method    | Normalized | Margin | NMI   | R@1   | R@4   | # of classes | #samples per class |
|-----------|------------|--------|-------|-------|-------|--------------|--------------------|
| [Semi-Hard](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/triplet_semihard_loss) | Yes | 0.2    | 0.587 | 49.03 | 73.43 | 20| 6|
| Hard Negatives | No | 1.0    | 0.561 | 46.55 | 71.03 | 20| 6|
| [Lifted Structured](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/lifted_struct_loss) | No | 1.0    | 0.502 | 35.26 | 59.82 | 20| 6|
| [N-Pair Loss](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/npairs_loss) | No | N/A    | 0.573 | 46.52 | 59.26 | 60| 2|
| [Angular Loss](https://github.com/geonm/tf_angular_loss) | Yes | N/A    | 0.546 | 45.50 | 68.43 | 60 | 2|
| Custom [Contrastive Loss](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/contrastive_loss) | Yes | 1.0    | 0.476 | 37.27 | 62.39 | 30| 4|

### Stanford Online Products Retrieval Evaluation
Mini-batch size=120. Architecture: Inception_Net V1.
Optimizer: Adam. Number of iterations = 30K

| Method    | Normalized | Margin | NMI   | R@1   | R@4   | # of classes | #samples per class |
|-----------|------------|--------|-------|-------|-------|--------------|--------------------|
| [Semi-Hard](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/triplet_semihard_loss) | Yes | 0.2    | 0.893 | 71.22 | 81.77 | 20| 6|
| Hard Negatives | No | 1.0    | 0.895 | 72.03 | 82.55 | 20| 6|
| [Lifted Structured](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/lifted_struct_loss) | No | 1.0    | 0.889 | 68.26 | 79.72 | 20| 6|
| [N-Pair Loss](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/npairs_loss) | No | N/A    | 0.893 | 72.60 | 82.59 | 60| 2|
| [Angular Loss](https://github.com/geonm/tf_angular_loss) | Yes | N/A    | 0.878 | 60.30 | 72.78 | 60 | 2|
| Custom [Contrastive Loss](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/contrastive_loss) | Yes | 1.0    | 0.825 | 19.05 | 32.28 | 30| 4|


    
### Requirements
* Python 3+ [Tested on 3.4.7 / 3.7]
* Tensorflow 1 and TF 2.0 [Tested on 1.8 / 1.14 / 2.0]

### Code Setup
1. Update the directories' paths in constants.py. 
2. Use train.py and train_tf2.py for TF 1.X and TF 2.X, respectively.
3. Use embed.py and embed_tf2.py for TF 1.X and TF 2.X, respectively.
4. eval.py.

### Supported Ranking losses
* Triplet Loss with hard mining - 'hard_triplet'
* Triplet Loss with semi-hard mining - 'semi_hard_triplet'
* Lifted Structure Loss - 'lifted_loss'
* N-pairs loss - 'npairs_loss'
* Angular loss - 'angular_loss'
* Contrastive loss - 'contrastive_loss'

Keep an eye on `ranking/__init__.py` for new ranking loss

### Recommeneded Setting for each loss

| Method    | Setting |
|-----------|------------|
| [Semi-Hard](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/triplet_semihard_loss) | L2-Norm Yes, Margin =0.2 |
| Hard Negatives | L2-Norm No , Margin =1.0 |
| [Lifted Structured](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/lifted_struct_loss) | L2-Norm No , Margin =1.0 | 
| [N-Pair Loss](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/npairs_loss) | L2-Norm No , Margin =N/A | 
| [Angular Loss](https://github.com/geonm/tf_angular_loss) | L2-Norm Yes, Margin =N/A | 
| Custom [Contrastive Loss](https://www.tensorflow.org/api_docs/python/tf/contrib/losses/metric_learning/contrastive_loss) | L2-Norm Yes, Margin =1.0 | 


### Wiki
* [Done] [Explain the fast contrastive loss sampling procedure](https://github.com/ahmdtaha/tf_retrieval_baseline/wiki/Contrastive-loss-with-tf.Data)
* [Done] The contrastive loss in the repos is customized to avoid nan during training. When the anchor and positive belong to the same class and the distance between their embeddings is near zero, the derivative turns into nan. [Lei Mao](https://leimao.github.io/article/Siamese-Network-MNIST/) provides a nice detailed mathematical explanation for this issue.

### TODO
* [TODO] bash script for train, embed and then eval
* [TODO] Evaluate space embedding during training.
* [TODO] After supporting TF 2.0 (eager execution), It become easier to support more losses -- Maybe add Margin loss.


### Misc Notes
* I noticed that some methods depend heavily on training parameters like the optimizer and number of iterations. For example, the semi-hard negative performance drops significantly on CUB-dataset if Adam optimizer is used instead of Momentum! The number of iterations seems also matter for this small dataset.
* The Tensorflow 2.0 implementation uses more memory even when disabling the eager execution. I tested the code with a smaller batch size -- ten classes and five samples per class. After training for 10K iterations, the performance achieved is NMI=0.54, R@1=42.64, R@4=66.52. 

## Release History

* 0.0.1
    * CHANGE: Jan 8, 2020. Update code to support Tensorflow 2.0
    * CHANGE: Dec 31, 2019. Update code to support Tensorflow 1.14
    * First Commit: May 24, 2019. Code tested on Tensorflow 1.8