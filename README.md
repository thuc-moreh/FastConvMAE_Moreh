## Pretraining ConvMAE on MAF
This model was tested on MAF VM9 (v23.1.2). SDA size is Medium.128GB.
Original repo: https://github.com/Alpha-VL/FastConvMAE/blob/main/PRETRAIN.md

## Usage
### Clone the repo
```bash
git clone https://github.com/thuc-moreh/FastConvMAE_Moreh.git
cd FastConvMAE_Moreh
```

### Install

- Create a conda environment and activate it:
```bash
conda create -n fastconvmae python=3.8
conda activate fastconvmae
update-moreh --target 23.1.2 --nightly --force
```

- Install pip packages

```bash
pip install -r requirements.txt
```

### Data preparation

You can download the ImageNet-1K (suggest using a subset of ImageNet-100lcs from Moreh) [here](https://image-net.org) and prepare the ImageNet-1K follow this format:
```tree data
imagenet
  ├── train
      ├── class1
      │   ├── img1.jpeg
      │   ├── img2.jpeg
      │   └── ...
      ├── class2
      │   ├── img3.jpeg
      │   └── ...
      └── ...
```
The repo uses a tiny subset of the ImageNet-1K dataset, which only contains 1 class. Data directory is `/nas/common_data/imagenet_tiny`

### Training
To pretrain FastConvMAE, run

```bash
python main_pretrain.py
```
The training log of 20 epochs is saved at `training_log_HAC9.txt`. 
Note:
- The training time of the first iteration on Moreh and Nvidia machines are roughly the same (3.5-4s), but on subsequent iterations NVIDIA VM only takes roughly 0.9s, while Moreh VM takes roughly 2,7s (3 times slower).
- Max memory usage on NVIDIA VM is 34032, while that of Moreh is 47156
- The learning rate and training loss convergence behaviors are roughly similar on both machines (depending on parameters initialization)

## Below is the orginial README
<div align="center">
<h1>🚀Fast ConvMAE🚀</h1>
<h3>Fast ConvMAE: Fast Pretraining of ConvMAE</h3>


</div>

This repo is the faster implementation of [ConvMAE: Masked Convolution Meets Masked Autoencoders](https://arxiv.org/abs/2205.03892)


## Updates
***17/June/2022***

Released the pre-training codes for ImageNet-1K.

## Introduction
Fast ConvMAE framework is a superiorly fast masked modeling scheme via complementary masking and mixture of reconstrunctors based on the ConvMAE. 

![tenser](figures/FastConvMAE.png)

## Pretrain on ImageNet-1K
The following table provides pretrained checkpoints and logs used in the paper.
| | Fast ConvMAE-Base|
| :---: | :---: |
| 50epoch pretrained checkpoints| N/A |
| logs | N/A |


## Main Results on COCO & ImageNet-1K
| Models | Masking | Tokenizer| Backbone | PT Epochs | PT Hours | COCO FT Epochs | $AP^{Box}$ | $AP^{Mask}$ |ImageNet Finetune Epochs | Finetune acc@1(%) | ADE 20K mIoU|
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| ConvMAE | 25 \% | RGB | ConvViT-B | 200 | 512 | 25 | 50.8 | 45.4 | 100| 84.4 | 48.5 |
| ConvMAE | 25 \% | RGB | ConvViT-B | 1600 | 4000 | 25 | 53.2 | 47.1 | 100 | 85.0 | 51.7 |
| MAE | 25 \% | RGB | ViT-B | 1600 | 2069 | 100 | 50.3 | 44.9 | 100 | 83.6 | 48.1 |
| SimMIM | 100 \% | RGB | Swin-B | 800 | 1609 | 36 | 50.4 | 44.4 | 100 | 84.0 | - |
| GreenMIM | 25 \% | RGB | Swin-B | 800 | 887 | 36 | 50.0 | 44.1 | 100 | 85.1 | - |
| ConvMAE | 100 \% | RGB | ConvViT-B | 50 | 266 | 25 | 51.0 | 45.4 | 100 | 84.4 | 48.3 |
| ConvMAE | 100 \% | C+T |ConvViT-B | 50 | 333 | 25 | 52.8 | 46.9 | 100 | 85.0 | 52.7 |
| ConvMAE | 100 \% | C+T |ConvViT-B | 100 | 666 | 25 | 53.3 | 47.3 | 100 | 85.2 | 52.8 |
| ConvMAE | 100 \% | C+T |ConvViT-L | 200 | N/A | 25 | N/A | N/A | 50 | 86.7 | 54.5 |
## Visualizations

NOTE: Grey patches are masked and colored ones are kept.

![tenser](figures/visualization_example.png)


## Getting Started
### Prerequisites
* Linux
* Python 3.7+
* CUDA 10.2+
* GCC 5+

### Training and evaluation
* See [PRETRAIN.md](PRETRAIN.md) for pretraining.


## Acknowledgement
The pretraining and finetuning of our project are based on [DeiT](https://github.com/facebookresearch/deit), [MAE](https://github.com/facebookresearch/mae), and [ConvMAE](https://github.com/Alpha-VL/ConvMAE). Thanks for their wonderful work.

## License
FastConvMAE is released under the [MIT License](https://github.com/Alpha-VL/ConvMAE/blob/main/LICENSE).


![visitors](https://visitor-badge.glitch.me/badge?page_id=Alpha-VL/FastConvMAE)

