# Flexible-CLmser: Regularized Feedback Connections for Biomedical Image Segmentation

The skip connections in U-Net pass features from
the levels of encoder to the ones of decoder in a symmetrical
way, which makes U-Net and its variants become state-of-the-art
approaches for biomedical image segmentation. However, the U-
Net skip connections are unidirectional without considering feed-
back from the decoder, which may be used to further improve the
segmentation performance. In this paper, we exploit the feedback
information to recurrently refine the segmentation. We develop a
deep bidirectional network based on the least mean square error
reconstruction (Lmser) self-organizing network, an early network
by folding the autoencoder along the central hidden layer. Such
folding makes the neurons on the paired layers between encoder
and decoder merge into one, equivalently forming bidirectional
skip connections between encoder and decoder. We find that
although the feedback links increase the segmentation accuracy,
they may bring noise into the segmentation when the network
proceeds recurrently. To tackle this issue, we present a gating
and masking mechanism on the feedback connections to filter
the irrelevant information. Experimental results on MoNuSeg,
TNBC, and EM membrane datasets demonstrate that our method
are robust and outperforms state-of-the-art methods.

This repository holds the Python implementation of the method described in the paper published in BIBM 2021.

Boheng Cao, Shikui Tu*, Lei Xu, "Flexible-CLmser: Regularized Feedback Connections for Biomedical Image Segmentation", BIBM2021

![Image](https://github.com/SJTUMisaka/Flexible-CLmser/blob/main/model_1.png)
## Content

1. [Structure](#Structure)
2. [Requirements](#Requirements)
3. [Data](#Data)
3. [Training](#Training)
4. [Testing](#Testing)
5. [Acknowledgement](#Acknowledgement)

## Structure

--checkpoints

\# pretrained models

--data

\# data for MoNuSeg, TNBC, and EM

--pytorch_version

\# code

## Requirements

- Python 3.6 or higher.
- PIL >= 7.0.0
- matplotlib >= 3.3.1
- tqdm >= 4.54.1
- imgaug >= 0.4.0
- torch >= 1.5.0
- torchvision >= 0.6.0

...

## Data
The author of [BiONet](https://github.com/tiangexiang/BiO-Net) has already gathered data of three datasets (Including EM  https://bionets.github.io/Piriform_data.zip). Please refer to the official website (or project repo) for license and terms of usage.
MoNuSeg: https://monuseg.grand-challenge.org/Data/
TNBC: https://github.com/PeterJackNaylor/DRFNS

We also provide our data (For EM only includes stack 1 and 4) and pretrained models here:
https://pan.baidu.com/s/1pHTexUIS8ganD_BwbWoAXA 
password：sjtu

or

https://drive.google.com/drive/folders/1GJq-AV1L1UNhI2WNMDuynYyGtOYpjQEi?usp=sharing

## Training

As an example, for EM segmentation, you can simply run:

`python main.py --train_data ./data/EM/train --valid_data ./data/EM/test --exp EM_1 --alpha=0.4`

Some of the available arguments are:

| Argument          | Description                                                | Default                     | Type  |
| ----------------- | ---------------------------------------------------------- | --------------------------- | ----- |
| `--epochs`        | Training epochs                                | 300                  | int   |
| `--batch_size`    |  Batch size                                          | 2                | int   |
| `--steps`        | Steps per epoch                                               | 250                        | int   |
| `--lr`             | Learning rate | 0.01                | float   |
| `--lr_decay`    | Learning rate decay                                         | 3e-5                          | float   |
| `--iter`            | recurrent iteration                                             | 3                        | int |
| `--train_data`         | Training data path           | ./data/monuseg/train                        | str |
| `--valid_data`         | Validating data path           | ./data/monuseg/test                        | str |
| `--valid_dataset`         | Validating dataset type           | monuseg                        | str |
| `--exp`        | Experiment name(use the same name when testing)                         | 1                        | str  |
| `--evaluate_only` |  If only evaluate using existing model            | store_true | action   |
| `--alpha`  | Weight of skip/backward connection             | 0.4            | float  |

## Testing
For MonuSeg and TNBC, you can just use our code to test the model, for example

`python main.py --valid_data ./data/tnbc --valid_dataset tnbc --exp your_experiment_id --alpha=0.4 --evaluate_only`

For EM, our code can not give the Rand F-score directly, but our code will save the ground truth and result in /checkpoints/your_experiment_id/outputs, you can use the tool ImageJ and code of https://imagej.net/tutorials/segmentation-evaluation-after-border-thinning to get Rand F-score.
## Acknowledgement

This project would not have been finished without using the codes or files from the following open source projects:

 [BiONet](https://github.com/tiangexiang/BiO-Net)



## Reference

Please cite our work if you find our code/paper is useful to your work.

```
tbd
```
