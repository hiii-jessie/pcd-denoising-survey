# A Survey of Deep Learning-based Point Cloud Denoising

This repository provides the denoised point clouds produced by the compared methods on the PUNet test set, corresponding to the quantitative results reported in Tables 3 and 4 of our survey.

## Download

[Download denoised point clouds](https://drive.google.com/file/d/1SlUiGBeMkKXA2-Mo-1bSvMkhBGUzhXRJ/view?usp=sharing)

## Data

- **Test shapes:** The 20 shapes in the PUNet test split [Yu et al., CVPR 2018](https://openaccess.thecvf.com/content_cvpr_2018/html/Yu_PU-Net_Point_Cloud_CVPR_2018_paper.html), following the split used by ScoreDenoise.
- **Noisy inputs:** Gaussian noise at levels of 1%, 2%, and 3%, with 10K and 50K points. The test data were released by ScoreDenoise [Luo and Hu, ICCV 2021] and are available in the [ScoreDenoise repository](https://github.com/luost26/score-denoise).
- **File format:** Each setting contains one `.xyz` file per shape.

## Directory Structure

The denoised point clouds are organized as follows:

```
<Method>/PUNet_<points>_poisson_<noise>/<shape>.xyz
```

Here, `<points>` is `10000` or `50000`, and `<noise>` is `0.01`, `0.02`, or `0.03`.

For example:

```
StraightPCF/PUNet_50000_poisson_0.03/horse.xyz
```

The released method folders are:

`3DMambaIPF`, `ASDN`, `DeepPSR`, `DMRDenoise`, `GPDNet`, `IterativePFN`, `MAG`, `MODNet`, `P2P-Bridge`, `Pathnet`, `PCDNF`, `PD-LTS`, `PDFlow`, `PointCleanNet`, `Pointfilter`, `RePCD`, `ScoreDenoise`, `StraightPCF`, `Un-DMRDenoise`, `Un-Noise4Denoise`, `Un-ScoreDenoise`, `Un-TotalDenoising`.

## Evaluation

The evaluation follows the unit-sphere protocol of ScoreDenoise, implemented in [`models/utils.py`](https://github.com/luost26/score-denoise/blob/main/models/utils.py), with metrics computed using PyTorch3D.

The ground-truth data are obtained from the PUNet release used by ScoreDenoise:

- **Ground-truth point clouds:** `pointclouds/test/<points>_poisson/<shape>.xyz`
- **Ground-truth meshes:** `meshes/test/<shape>.off`

The released denoised point clouds are in the same coordinate frame as the noisy inputs. Normalization is performed within the metric functions.

Results are averaged over the 20 test shapes. CD and P2M values are multiplied by $10^4$, while HD values are multiplied by $10^3$, as reported in the paper.

### Evaluation Environment

The evaluation was performed using the following environment:

- Python 3.8.20
- PyTorch 1.11.0
- PyTorch3D 0.7.4
- CUDA 11.5
- `point_cloud_utils` 0.34.0 (for mesh loading)

## Acknowledgements

We thank the authors of all compared methods for sharing their work, code, and pretrained models. We are also grateful to the authors of PU-Net and ScoreDenoise for making the datasets and evaluation resources publicly available. Their contributions have been invaluable to this survey.

## Usage and Citation

The denoised point clouds are provided for academic research and evaluation purposes only. The original datasets and method implementations remain subject to their respective licenses and terms of use. No additional rights to these third-party resources are granted.
If you use these results in your research, please cite the original papers of the corresponding methods and our survey.
