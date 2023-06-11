# Extended Agriculture-Vision: An Extension of a Large Aerial Image Dataset for Agricultural Pattern Analysis

## Extended Agriculture-Vision (Published in TMLR):

A continuous work of [Agriculture-Vision](https://github.com/SHI-Labs/Agriculture-Vision), with great collaborators to bring Agriculture and Computer Vision / AI communities together to benefit humanity!


## Overview
 1. [Paper](#Paper)
 2. [Dataset](#Dataset)


<!--  3. [Pre-training](#Pre-training)
 4. [Train_Segmentation](#Train_Segmentation)
 5. [Code_Structure](#Structure)
 6. [ToDo](#ToDo) -->
 
 
 ### Papers  <a name="Paper"></a>
 
Paper on TMLR:
 
[TMLR](https://openreview.net/pdf?id=v5jwDLqfQo), [ArXiv](https://arxiv.org/abs/2303.02460)
 
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
 
 
 
 
 
 ### Dataset  <a name="Dataset"></a>
 
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
 
 
 
 

 The data, paper and visualizations will be released soon. Stay tuned!
