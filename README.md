# SimFlowSR: Self-similarity Aggregation over Consistent Information Flow for Single Image Super-Resolution

<div align="center">
<img src="./static/images/SimFlowSR_logo.png" width="600"/>

## [[Paper Link]](https://arxiv.org/abs/XXXX.XXXXX) [[Project Page]](https://ming053l.github.io/PhaSR/) [[Model zoo]](https://drive.google.com/drive/folders/XXXXX) [[Visual Results]](https://drive.google.com/drive/folders/XXXXX)

[Chia-Ming Lee](https://ming053l.github.io/), [Chih-Chung Hsu](https://cchsu.info/)

National Yang Ming Chiao Tung University, National Cheng Kung University
</div>

## Overview

**TL;DR:** PhaSR combines parameter-free Retinex normalization with geometric-semantic cross-modal attention for state-of-the-art shadow removal and ambient lighting normalization with highest efficiency.

- **Background and Motivation**

Shadow removal under diverse lighting conditions requires disentangling illumination from intrinsic reflectance. Existing methods struggle with: (1) confusing shadows with intrinsic material properties, (2) limited generalization from single-light to multi-source ambient lighting, and (3) loss of physical priors through encoder-decoder bottlenecks.

- **Main Contribution**

PhaSR addresses these challenges through **dual-level physically aligned prior integration**:

1. **PAN (Physically Aligned Normalization)** - Parameter-free preprocessing via Gray-world normalization, log-domain Retinex decomposition, and dynamic range recombination, consistently improving existing architectures by 0.15-0.34 dB.

2. **GSRA (Geometric-Semantic Rectification Attention)** - Cross-modal differential attention (`A_rect = A_sem - λ·A_geo`) harmonizing DepthAnything-v2 geometry with DINO-v2 semantics.

<img src="./static/images/SimFlowSR_arch.png" width="600"/>

**Benchmark results on shadow removal and ambient lighting normalization.**

| Model | Params | FLOPs | ISTD+ | WSRD+ | Ambient6K |
|:-----:|:------:|:-----:|:-----:|:-----:|:---------:|
| OmniSR | 24.55M | 78.32G | 33.34 | 26.07 | 23.01 |
| DenseSR | 24.70M | 81.13G | 33.98 | 26.28 | 22.54 |
| **PhaSR** | **18.95M** | **55.63G** | **34.48** | **28.44** | **23.32** |

## Updates

- ✅ 2025-11-16: Project page released.
- ⏳ Code and pretrained models coming soon.

## Environment
- [PyTorch >= 1.7](https://pytorch.org/)
- [BasicSR == 1.3.4.9](https://github.com/XPixelGroup/BasicSR/blob/master/INSTALL.md)

### Installation
```bash
git clone https://github.com/ming053l/phasr.git
conda create --name phasr python=3.8 -y
conda activate phasr
conda install pytorch==1.12.1 torchvision==0.13.1 cudatoolkit=11.6 -c pytorch -c conda-forge
cd phasr
pip install -r requirements.txt
python setup.py develop
```

## How To Test
```bash
python phasr/test.py -opt options/test/PhaSR_test.yml
```

## How To Train
```bash
CUDA_VISIBLE_DEVICES=0,1,2,3 python -m torch.distributed.launch --nproc_per_node=4 --master_port=4321 phasr/train.py -opt options/train/train_PhaSR.yml --launcher pytorch
```

## Citations

If our work is helpful to your research, please kindly cite:
```bibtex
@article{lee2024phasr,
  title={PhaSR: Generalized Image Shadow Removal with Physically Aligned Priors},
  author={Lee, Chia-Ming and Lin, Yu-Fan and Hsiao, Yu-Jou and Jung, Jing-Hui and Liu, Yu-Lun and Hsu, Chih-Chung},
  journal={arXiv preprint arXiv:XXXX.XXXXX},
  year={2024}
}
```

## Acknowledgments

Our work builds upon [OmniSR](https://github.com/xxx/omnisr), [DenseSR](https://github.com/xxx/densesr), [DepthAnything-v2](https://github.com/xxx/depth-anything-v2), and [DINO-v2](https://github.com/facebookresearch/dinov2). We are grateful for their outstanding contributions.

## Contact
If you have any questions, please email [your-email] to discuss with the authors.
