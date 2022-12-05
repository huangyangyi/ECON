<!-- PROJECT LOGO -->

<p align="center">

  <h1 align="center">ECON: Explicit Clothed humans Obtained from Normals</h1>
  <p align="center">
    <a href="https://ps.is.tuebingen.mpg.de/person/yxiu"><strong>Yuliang Xiu</strong></a>
    ·
    <a href="https://ps.is.tuebingen.mpg.de/person/jyang"><strong>Jinlong Yang</strong></a>
    ·
    <a href="https://hoshino042.github.io/homepage/"><strong>Xu Cao</strong></a>
    ·
    <a href="https://ps.is.mpg.de/~dtzionas"><strong>Dimitrios Tzionas</strong></a>
    ·
    <a href="https://ps.is.tuebingen.mpg.de/person/black"><strong>Michael J. Black</strong></a>
  </p>
  <h2 align="center">arXiv 2022</h2>
  <div align="center">
    <img src="./assets/teaser.gif" alt="Logo" width="100%">
  </div>

  <p align="center">
  <br>
    <a href="https://pytorch.org/get-started/locally/"><img alt="PyTorch" src="https://img.shields.io/badge/PyTorch-ee4c2c?logo=pytorch&logoColor=white"></a>
    <a href="https://pytorchlightning.ai/"><img alt="Lightning" src="https://img.shields.io/badge/-Lightning-792ee5?logo=pytorchlightning&logoColor=white"></a>
    <br></br>
    <a href=''>
      <img src='https://img.shields.io/badge/Paper-PDF-green?style=for-the-badge&logo=arXiv&logoColor=green' alt='Paper PDF'>
    </a>
    <a href="https://discord.gg/Vqa7KBGRyk"><img src="https://img.shields.io/discord/940240966844035082?color=7289DA&labelColor=4a64bd&logo=discord&logoColor=white&style=for-the-badge"></a>
    <a href="https://youtu.be/j5hw4tsWpoY"><img alt="youtube views" title="Subscribe to my YouTube channel" src="https://img.shields.io/youtube/views/j5hw4tsWpoY?logo=youtube&labelColor=ce4630&style=for-the-badge"/></a>
  </p>
</p>

<br/>

ECON is designed for **"Human digitization from a color image"**, which combines the best properties of implicit and explicit representations, to infer high-fidelity 3D clothed humans from in-the-wild images, even with **loose clothing** or in **challenging poses**. ECON also supports batch reconstruction from **multi-person** photos.
<br/>
<br/>

## News :triangular_flag_on_post:
- [2022/03/05] <a href="">arXiv</a> and <a href="#demo">demo</a> are available.

## TODO
- [ ] Blender add-on for FBX export
- [ ] Full RGB texture generation

<br>

<!-- TABLE OF CONTENTS -->
<details open="open" style='padding: 10px; border-radius:5px 30px 30px 5px; border-style: solid; border-width: 1px;'>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#instructions">Instructions</a>
    </li>
    <li>
      <a href="#demo">Demo</a>
    </li>
    <li>
      <a href="#tricks">Tricks</a>
    </li>
    <li>
      <a href="#citation">Citation</a>
    </li>
  </ol>
</details>

<br/>

## Instructions

- See [docs/installation.md](docs/installation.md) to install all the required packages and setup the models


## Demo

```bash
# For image-based reconstruction
python -m apps.infer -cfg ./configs/econ.yaml -in_dir ./examples -out_dir ./results

# For video rendering
python -m apps.multi_render -n {filename}
```

## Tricks
### Some adjustable parameters in *config/econ.yaml*
- `use_ifnet`
  - True: use IF-Nets+ for mesh completion ( $\text{ECON}_\text{IF}$ - Better quality)
  - False: use SMPL-X for mesh completion ( $\text{ECON}_\text{EX}$ - Faster speed)
- `use_smpl`
  - [ ]: don't use either hands or face parts from SMPL-X
  - ["hand"]: only use the **visible** hands from SMPL-X
  - ["hand", "face"]: use both **visible** hands and face from SMPL-X
- `thickness` (default 2cm)
  - could be increased accordingly in case **xx_full.obj** looks flat
- `hps_type`
  - "pixie": more accurate for face and hands
  - "pymafx": more robust for challenging poses

<br/>

## More Qualitative Results

|![OOD Poses](assets/OOD-poses.jpg)|
| :----------------------: |
|_Challenging Poses_|
|![OOD Clothes](assets/OOD-outfits.jpg)|
|_Loose Clothes_|
|![SHHQ](assets/SHHQ.gif)|
|_ECON Results on [SHHQ Dataset](https://github.com/stylegan-human/StyleGAN-Human)_|
|![crowd](assets/crowd.gif)|
|_ECON Results on Multi-Person Image_|


<br/>
<br/>

## Citation

```bibtex
@inproceedings{xiu2022econ,
  title     = {{ECON}: {E}xplicit {C}lothed humans {O}btained from {N}ormals},
  author    = {Xiu, Yuliang and Yang, Jinlong and Cao, Xu and Tzionas, Dimitrios and Black, Michael J.},
  booktitle = arXiv,
  month     = {Dec},
  year      = {2022},
}
```
<br/>

## Acknowledgments

We thank [Lea Hering](https://is.mpg.de/person/lhering) and [Radek Daněček](https://is.mpg.de/person/rdanecek) for proof reading, [Yao Feng](https://ps.is.mpg.de/person/yfeng), [Haven Feng](https://is.mpg.de/person/hfeng), and [Weiyang Liu](https://wyliu.com/) for their feedback and discussions, [Tsvetelina Alexiadis](https://ps.is.mpg.de/person/talexiadis) for her help with the AMT perceptual study.

Here are some great resources we benefit from:

- [ICON](https://github.com/YuliangXiu/ICON) for Body Fitting
- [MonoPortDataset](https://github.com/Project-Splinter/MonoPortDataset) for Data Processing
- [rembg](https://github.com/danielgatis/rembg) for Human Segmentation
- [smplx](https://github.com/vchoutas/smplx), [PyMAF-X](https://www.liuyebin.com/pymaf-x/), [PIXIE](https://github.com/YadiraF/PIXIE) for Human Pose & Shape Estimation
- [CAPE](https://github.com/qianlim/CAPE) and [THuman](https://github.com/ZhengZerong/DeepHuman/tree/master/THUmanDataset) for Dataset
- [PyTorch3D](https://github.com/facebookresearch/pytorch3d) for Differential Rendering

Some images used in the qualitative examples come from [pinterest.com](https://www.pinterest.com/).

This project has received funding from the European Union’s Horizon 2020 research and innovation programme under the Marie Skłodowska-Curie grant agreement No.860768 ([CLIPE Project](https://www.clipe-itn.eu)).

--------------

<br>

## License

This code and model are available for non-commercial scientific research purposes as defined in the [LICENSE](LICENSE) file. By downloading and using the code and model you agree to the terms in the [LICENSE](LICENSE).

## Disclosure

MJB has received research gift funds from Adobe, Intel, Nvidia, Meta/Facebook, and Amazon.  MJB has financial interests in Amazon, Datagen Technologies, and Meshcapade GmbH.

## Contact

For technical questions, please contact yuliang.xiu@tue.mpg.de

For commercial licensing, please contact ps-licensing@tue.mpg.de and black@tue.mpg.de
