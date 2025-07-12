# Parallel Interactive Transformer for Single Infrared Image Super-resolution





---
This code is the PyTorch implementation of PIT model. Our PIT achieves **state-of-the-art** performance in Infrared Image Super-resolution

> **Abstract:** ** 
>
> <p align="center">
> <img width="800" src="figs/git.png">
> </p>

|                          *img_092 (x4)*                           |                          *img_098 (x4)*                           |                          *HR*                           |                          *LR*                           |*SwinIR*                           |*ART (ours)*                           |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |:----------------------------------------------------------: |:----------------------------------------------------------: |
| <img src="figs/Resize_ComL_img_092_HR_x4.png"  height=110 width=135> | <img src="figs/Resize_ComL_img_098_HR_x4.png"  height=110 width=135> | <img src="figs/ComS_img_092_HR_x4.png" width=101 height=51> <img src="figs/ComS_img_098_HR_x4.png" width=101 height=51> | <img src="figs/ComS_img_092_Bicubic_x4.png" width=101 height=51> <img src="figs/ComS_img_098_Bicubic_x4.png" width=101 height=51> | <img src="figs/ComS_img_092_SwinIR_x4.png" width=101 height=51> <img src="figs/ComS_img_098_SwinIR_x4.png" width=101 height=51> |<img src="figs/ComS_img_092_ART_x4.png" width=101 height=51> <img src="figs/ComS_img_098_ART_x4.png" width=101 height=51> |

## Requirements
- python 3.8
- pyTorch >= 1.8.0
- NVIDIA GPU + [CUDA](https://developer.nvidia.com/cuda-downloads)

### Installation
```bash
git clone https://github.com/WYpetuous/PIT.git
cd PIT
pip install -r requirements.txt
python setup.py develop
```

## TODO

* [x] Testing on Image SR
* [x] Training
* [ ] More tasks
## Contents

1. [Models](#Models)
1. [Datasets](#Datasets)
1. [Training](#training)
1. [Testing](#Testing)
1. [Results](#Results)
1. [Citation](#citation)
1. [Acknowledgement](#Acknowledgement)

---
## Models



- We provide the performance on Urban100 (x4, SR), Urban100 (level=50, Color-DN) LIVE1 (q=10, CAR), and SIDD (Real-DN). We use the input 160 × 160 to calculate FLOPS.
- Download  the models and put them into the folder `experiments/pretrained_models`  . Go to the folder to find details of directory structure.

## Datasets


Used training and testing sets can be downloaded as follows:


Download  training and testing datasets and put them into the folder `datasets/`. Go to the folder to find details of directory structure.

## Training
### Train on SR
1. Please download the corresponding training datasets and put them in the folder `datasets/DF2K`. Download the testing datasets and put them in the folder `datasets/SR`.
2. Follow the instructions below to begin training our ART model.
    ```bash
    # train ART for SR task, cropped input=64×64, 4 GPUs, batch size=8 per GPU
    python -m torch.distributed.launch --nproc_per_node=1 --master_port=2414 basicsr/train.py -opt options/train/train_ART_SR_x2.yml --launcher pytorch

    CUDA_VISIBLE_DEVICES=6 nohup python basicsr/train.py -opt options/train/train_ART_SR_x2.yml

    python -m torch.distributed.launch --nproc_per_node=4 --master_port=2414 basicsr/train.py -opt options/train/train_ART_SR_x3.yml --launcher pytorch
    python -m torch.distributed.launch --nproc_per_node=4 --master_port=2414 basicsr/train.py -opt options/train/train_ART_SR_x4.yml --launcher pytorch

    # train ART-S for SR task, cropped input=64×64, 4 GPUs, batch size=8 per GPU
    python -m torch.distributed.launch --nproc_per_node=4 --master_port=2414 basicsr/train.py -opt options/train/train_ART_S_SR_x2.yml --launcher pytorch
    python -m torch.distributed.launch --nproc_per_node=4 --master_port=2414 basicsr/train.py -opt options/train/train_ART_S_SR_x3.yml --launcher pytorch
    python -m torch.distributed.launch --nproc_per_node=4 --master_port=2414 basicsr/train.py -opt options/train/train_ART_S_SR_x4.yml --launcher pytorch
    ``` 
    Run the script then you can find the generated experimental logs in the folder `experiments`.


## Testing
### Test on SR
#### Test with ground-truth images
1. Please download the corresponding testing datasets and put them in the folder `datasets/SR`. Download the corresponding models and put them in the folder `experiments/pretrained_models`. 
2. Follow the instructions below to begin testing our ART model.
    ```bash
    # test ART model for image SR. You can find corresponding results in Table 2 of the main paper.
    python basicsr/test.py -opt options/test/test_ART_SR_x2.yml
    python basicsr/test.py -opt options/test/test_ART_SR_x3.yml
    python basicsr/test.py -opt options/test/test_ART_SR_x4.yml
    # test ART-S model for image SR. You can find corresponding results in Table 2 of the main paper.
    python basicsr/test.py -opt options/test/test_ART_S_SR_x2.yml
    python basicsr/test.py -opt options/test/test_ART_S_SR_x3.yml
    python basicsr/test.py -opt options/test/test_ART_S_SR_x4.yml
    ``` 


## Results

We provide the results on image SR, color image denoising, real image denoising, and JPEG compression artifact reduction here. More results can be found in the main paper. The visual results of ART can be downloaded [here](https://drive.google.com/drive/folders/1b92XHwxuvBLOAiHAjWe-VFKN01hQUiO_?usp=sharing). 

<details>
<summary>Image SR (click to expan)</summary>

- Results of Table 2 in the main paper

<p align="center">
  <img width="900" src="figs/SR.png">
</p>

- Visual results

<p align="center">
  <img width="900" src="figs/Visual_SR_1.png">
</p>

<p align="center">
  <img width="900" src="figs/Visual_SR_2.png">
</p>

</details>

<details>
<summary>Color Image Denoising(click to expan)</summary>

- Results of Table 4 in the main paper

<p align="center">
  <img width="900" src="figs/ColorDN.png">
</p>

- Visual results

<p align="center">
  <img width="900" src="figs/Visual_DN.png">
</p>

</details>

<details>
<summary>Real Image Denoising (click to expan)</summary>

- Results of Table 7 in the main paper

<p align="center">
  <img width="900" src="figs/RealDN.png">
</p>

</details>

<details>
<summary>JPEG Compression Artifact Reduction (click to expan)</summary>

- Results of Table 5 in the main paper

<p align="center">
  <img width="900" src="figs/CAR.png">
</p>

</details>

## Citation

If you find the code helpful in your resarch or work, please cite the following paper(s).
```
@inproceedings{
}
```

## Acknowledgement

This work is released under the Apache 2.0 license.
 The codes are based on [BasicSR](https://github.com/xinntao/BasicSR) and [ART](). Please also follow their licenses. Thanks for their awesome works.
