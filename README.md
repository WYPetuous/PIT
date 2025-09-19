# Parallel Interactive Transformer for Single Infrared Image Super-resolution





---
This code is the PyTorch implementation of PIT model. Our PIT achieves **state-of-the-art** performance in Infrared Image Super-resolution

>**Abstract:****
>
><palign="center">
><imgwidth="800"src="figs/git.png">
></p>



##Requirements
-python 3.8
-pyTorch >= 1.8.0
-NVIDIA GPU +[CUDA](https://developer.nvidia.com/cuda-downloads)

###Installation
```bash
git clone https://github.com/WYpetuous/PIT.git
cd PIT
pip install -r requirements.txt
python setup.py develop
```

##TODO

*[x]Testing on Image SR
*[x]Training

---

##MORE
<a href="https://imgsli.com/NDE2MzIx">


##Models

-We provide the performance on

##Datasets


Used training and testing sets can be downloaded as follows: [M3FD_TNO_RoadScene](https://drive.google.com/drive/folders/1K8pRnyiwW6dJ0Kfr_yDVEI57qbXwoUjQ?usp=drive_link).


Download  training and testing datasets and put them into the folder`datasets/`. Go to the folder to find details of directory structure.

##Training
1.Please download the corresponding training datasets and put them in the folder`datasets/DF2K`. Download the testing datasets and put them in the folder`datasets/SR`.
2.Follow the instructions below to begin training our ART model.
```bash

python basicsr/train.py -opt options/train/train_PIT_SR_x2.yml
python basicsr/train.py -opt options/train/train_PIT_S_SR_x4.yml
```
Run the script then you can find the generated experimental logs in the folder`experiments`.


##Testing
1.Please download the corresponding testing datasets and put them in the folder`datasets/SR`. Download the corresponding models and put them in the folder`experiments/pretrained_models`.
2.Follow the instructions below to begin testing our ART model.
```bash
# test ART model for image SR. You can find corresponding results in Table 2 of the main paper.
python basicsr/test.py -opt options/test/test_PIT_SR_x2.yml
python basicsr/test.py -opt options/test/test_PIT_SR_x4.yml
```


##Results


##Citation

If you find the code helpful in your resarch or work, please cite the following paper(s).
```
@inproceedings{
}
```

##Acknowledgement

This work is released under the Apache 2.0 license.
The codes are based on[BasicSR](https://github.com/xinntao/BasicSR)and[ART](). Please also follow their licenses. Thanks for their awesome works.
