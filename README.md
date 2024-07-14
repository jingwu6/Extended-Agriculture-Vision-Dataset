# Extended Agriculture-Vision: An Extension of a Large Aerial Image Dataset for Agricultural Pattern Analysis

## Extended Agriculture-Vision (Published in TMLR):

A continuous work of [Agriculture-Vision](https://github.com/SHI-Labs/Agriculture-Vision), with great collaborators to bring Agriculture and Computer Vision / AI communities together to benefit humanity!


## Overview
 1. [Paper](#Paper)
 2. [Dataset](#Dataset)
 3. [Quick Start](#Quick)


 
 
 ### 1. Papers  <a name="Paper"></a>
 
Extended Agriculture-Vision on TMLR:
 
[TMLR](https://openreview.net/pdf?id=v5jwDLqfQo)

[ArXiv](https://arxiv.org/abs/2303.02460)

[Supplementary](https://openreview.net/attachment?id=v5jwDLqfQo&name=supplementary_material)
 
 ```
@article{
wu2023extended,
title={Extended Agriculture-Vision: An Extension of a Large Aerial Image Dataset for Agricultural Pattern Analysis},
author={Jing Wu and David Pichler and Daniel Marley and Naira Hovakimyan and David A Wilson and Jennifer Hobbs},
journal={Transactions on Machine Learning Research},
issn={2835-8856},
year={2023},
url={https://openreview.net/forum?id=v5jwDLqfQo},
note={}
}

@article{wu2023extended,
 title={Extended Agriculture-Vision: An Extension of a Large Aerial Image Dataset for Agricultural Pattern Analysis},
 author={Wu, Jing and Pichler, David and Marley, Daniel and Wilson, David and Hovakimyan, Naira and Hobbs, Jennifer},
 journal={arXiv preprint arXiv:2303.02460},
 year={2023}
}
 ```
 
 
 
 
 
 ### 2. Dataset  <a name="Dataset"></a>


 #### To download a subset of the full dataset, please use the following link:

https://www.dropbox.com/scl/fo/7yzzc8hqtvaki2y1md6h4/h?rlkey=su71dij6xfb964zfwe1d6kros&e=1&dl=0.


 #### To download the full dataset:
 
 The Extended Agriculture-Vision can be downloaded with the following command:
 ```
 aws s3 cp  s3://intelinair-data-releases/agriculture-vision/TMLR_benchmarks_2023/ Path_to_Save --no-sign-request --recursive
 ```
 
 For example, to download the dataset in your current location, use:
  ```
 aws s3 cp  s3://intelinair-data-releases/agriculture-vision/TMLR_benchmarks_2023/ . --no-sign-request --recursive
 ```
 
  Previous supervised dataset can be downloaded with the following command:
 ```
 aws s3 cp s3://intelinair-data-releases/agriculture-vision/cvpr_challenge_2021/supervised supervised --no-sign-request --recursive
 ```
 
 
### 3. Quick Start on Pre-trained Weights  <a name="Quick"></a>
#### 3.1 Pre-trained Models

|Dataset          | Pre-trained Methods|Architecture | Link | 
| ------- | :---------: | ------------ | ---- | 
|Extended AgVision|MoCoV2 | ResNet-18    | [download](https://zenodo.org/record/8170135/files/Res_18.pth?download=1) | 
|Extended AgVision|MoCoV2 | ResNet-50    | [download](https://zenodo.org/record/8170160/files/Res_50.pth?download=1)   | 



#### 3.2 To load pre-trained ResNet-18 with RGBN channels (The same when applied to ResNet-50,101)
```
import torch
import torchvision.transforms as transforms
import torchvision.models as models

# Create a new ResNet-18 model with four channels input
resnet18_four_channels = models.resnet18(pretrained=False)
resnet18_four_channels.conv1 = torch.nn.Conv2d(4, 64, kernel_size=7, stride=2, padding=3, bias=False)
resnet18_four_channels = torch.nn.Sequential(*list(resnet18_four_channels.children())[:-1], torch.nn.Flatten())

# Load the saved weights into the new model
resnet18_four_channels.load_state_dict(torch.load('Res_18.pth'))
```

#### 3.3 To load pre-trained ResNet-18 with RGB channels (The same when applied to ResNet-50,101)
```
import torch
import torchvision.transforms as transforms
import torchvision.models as models

# Create a new ResNet-18 model with three channels input
resnet18_three_channels = models.resnet18(pretrained=False)
resnet18_three_channels = torch.nn.Sequential(*list(resnet18_three_channels.children())[:-1], torch.nn.Flatten())

# Load the saved weights from the model with four channels
saved_state_dict = torch.load('Res_18.pth')
# Discard the extra channel in the weights (assuming the first channel needs to be discarded)
saved_state_dict['0.weight'] = saved_state_dict['0.weight'][:, :-1, :, :]

# Load the modified state_dict into the new model
resnet18_three_channels.load_state_dict(saved_state_dict)
```
