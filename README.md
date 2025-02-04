# Extended Agriculture-Vision

A comprehensive aerial image dataset for agricultural pattern analysis, extending the original [Agriculture-Vision](https://github.com/SHI-Labs/Agriculture-Vision) project. This dataset bridges the gap between Agriculture and Computer Vision/AI communities to advance agricultural technology.

## 🎯 Latest Updates

- **December 2023**: Dataset selected as foundation for CVPR workshop challenge: [Agriculture Vision 2024](https://www.agriculture-vision.com/)
- **October 2023**: Full dataset release
- **September 2023**: Research paper published in [TMLR](https://openreview.net/pdf?id=v5jwDLqfQo)

## 📚 Dataset Access

### Quick Download (Challenge Subset)
Access the dataset subset supporting AgVision 2024 Challenge via [Dropbox](https://www.dropbox.com/scl/fo/7yzzc8hqtvaki2y1md6h4/h?rlkey=su71dij6xfb964zfwe1d6kros&e=1&dl=0).

### Full Dataset Download
Use AWS CLI to download the complete Extended Agriculture-Vision dataset:

```bash
# Download complete TMLR 2023 dataset
aws s3 cp s3://intelinair-data-releases/agriculture-vision/TMLR_benchmarks_2023/ . \
    --no-sign-request --recursive

# Download previous supervised dataset (2021)
aws s3 cp s3://intelinair-data-releases/agriculture-vision/cvpr_challenge_2021/supervised \
    supervised --no-sign-request --recursive
```

## 🚀 Pre-trained Models

Available models trained on Extended Agriculture-Vision:

| Architecture | Method | Download Link |
|--------------|--------|---------------|
| ResNet-18    | MoCoV2 | [Download](https://zenodo.org/record/8170135/files/Res_18.pth?download=1) |
| ResNet-50    | MoCoV2 | [Download](https://zenodo.org/record/8170160/files/Res_50.pth?download=1) |

### Usage Examples

#### Loading ResNet with RGBN Channels
```python
import torch
import torchvision.models as models

def load_resnet_rgbn(model_path, architecture='resnet18'):
    # Create model with four-channel input
    model = getattr(models, architecture)(pretrained=False)
    model.conv1 = torch.nn.Conv2d(4, 64, kernel_size=7, stride=2, padding=3, bias=False)
    model = torch.nn.Sequential(*list(model.children())[:-1], torch.nn.Flatten())
    
    # Load weights
    model.load_state_dict(torch.load(model_path))
    return model

# Example usage
model = load_resnet_rgbn('Res_18.pth', 'resnet18')
```

#### Loading ResNet with RGB Channels
```python
import torch
import torchvision.models as models

def load_resnet_rgb(model_path, architecture='resnet18'):
    # Create model with three-channel input
    model = getattr(models, architecture)(pretrained=False)
    model = torch.nn.Sequential(*list(model.children())[:-1], torch.nn.Flatten())
    
    # Load and modify weights
    state_dict = torch.load(model_path)
    state_dict['0.weight'] = state_dict['0.weight'][:, :-1, :, :]
    model.load_state_dict(state_dict)
    return model

# Example usage
model = load_resnet_rgb('Res_18.pth', 'resnet18')
```

## 📖 Citations

If you use this dataset in your research, please cite:

```bibtex
@article{wu2023extended,
    title={Extended Agriculture-Vision: An Extension of a Large Aerial Image Dataset for Agricultural Pattern Analysis},
    author={Wu, Jing and Pichler, David and Marley, Daniel and Hovakimyan, Naira and Wilson, David A and Hobbs, Jennifer},
    journal={Transactions on Machine Learning Research},
    issn={2835-8856},
    year={2023},
    url={https://openreview.net/forum?id=v5jwDLqfQo}
}
```

## 📑 Related Papers

- [TMLR Publication](https://openreview.net/pdf?id=v5jwDLqfQo)
- [ArXiv Preprint](https://arxiv.org/abs/2303.02460)
- [Supplementary Materials](https://openreview.net/attachment?id=v5jwDLqfQo&name=supplementary_material)

## 🔗 Related Links

- [Agriculture Vision 2024 Challenge](https://www.agriculture-vision.com/agriculture-vision-2024/prize-challenge-2024)
- Original [Agriculture-Vision Project](https://github.com/SHI-Labs/Agriculture-Vision)
