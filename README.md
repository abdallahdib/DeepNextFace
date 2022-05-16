# DeepNextFace (Towards High Fidelity Monocular Face Reconstruction using Self-supervised Learning and Ray Tracing) -- ICCV 2021 --
DeepNextFace is a 3D face reconstruction library from a single monocular RGB image via deep convolutional neural networks and differentiable ray tracing. It achieves fast, robust and stable 3D face reconstruction. From a single RGB image, DeepNextFace estimates face geometry, spatially-varying skin reflectance (diffuse and specular albedos), scene light and head pose. The library uses the differentiable rendering layer of [NextFace](https://github.com/abdallahdib/NextFace/). This repository is a reproduction of our [ICCV 2021 paper](https://openaccess.thecvf.com/content/ICCV2021/papers/Dib_Towards_High_Fidelity_Monocular_Face_Reconstruction_With_Rich_Reflectance_Using_ICCV_2021_paper.pdf)
<p align="center"><img src="resources/teaser1.gif" style="float: left; width: 60%; margin-right: 1%; margin-bottom: 0.5em;"></p>
<p align="center"><img src="resources/teaser4.gif" style="float: left; width: 60%; margin-right: 1%; margin-bottom: 0.5em;"></p>

# Features: 
* The network is trained in a fully self-supervised manner on unlabeled images.  
* Estimates face geometry 
* Estimates medium-details face reflectance (diffuse and specular) based on simplified cook-torrance BRDF 
* robust against extreme head poses and expressions
* robust against challenging lighting conditions and shadows. 
* Estimates scene light with spherical harmonics
* Estimates head pose and orientation
* Runs on both cpu and cuda-enabled gpu
* 
# Installation
* Clone the repository 
* Execute the commands in 'INSTALL' file. these commands create a new conda environment called deepNextFace and install required packages. An 'environment.yml' is also provided. The library is tested with torch 1.3.1, torchvision 0.4.2 and cuda toolkit 10.1, but it should also work with recent pytorch versions.   
* Activate the environment: conda activate deepNextFace
* Download basel face model 2009 from [here](https://faces.dmi.unibas.ch/bfm/index.php?nav=1-2&id=downloads), just fill the form and you will receive an instant direct download link into your inbox. Downloaded  **01_MorphableModel.mat** file and put it inside **./morphableModel2009** directory


# How to use
## Reconstruction from multiple images (batch reconstruction)
* Put your images in the same folder and run the following command for reconstruction: 
  * **python recontruct.py --input *path-to-your-folder-that-contains-all-ur-images* --output *output-path-where-to-save-results***

# How it works
DeepNextFace is a reproduction of [our early work](https://openaccess.thecvf.com/content/ICCV2021/papers/Dib_Towards_High_Fidelity_Monocular_Face_Reconstruction_With_Rich_Reflectance_Using_ICCV_2021_paper.pdf) with some slight differences (see below). 
The network architecture is composed mainly of two stages. First, a resnet encoder takes as input an RGB image and project it into a latent code, a fully connected layer takes as input the latent code and predicts the 3DMM parameters (shape identity, expression), head pose (rotation translation), camera (focal) and scene light (with spherical harmonics). The second stage is composed of two decoders, trained to reconstruct a delta diffuse and specular maps from the latent code. These detlta maps are added on top of the statistical albedo maps (obtained from the first stage) to captrue medium-frequency albedo details outside the span of the statistical prior space. This allow to capture more details in the final reflectance maps (such as beards and makeup). Please note that there is some slight difference in the network trained here and the one in our paper. For instance, The network used in DeepNextFace uses less epoches than in the paper which leads to some slight differences with the paper.

# Limitations 
* By design, DeepNextFace can only capture medium-frequency albedo details, and high frequency albedo details will not be captured. This is because the texture decoders operates on a compact representation of the input image (the latent code of the resnet)  our recent [work](https://arxiv.org/abs/2203.07732) captures more albedo details.
* DeepNextFace cannot capture fine geometry details (wrinkles, pores...). s. our recent [work](https://arxiv.org/abs/2203.07732) captures fine scale geometric details.
* Texture resolution is limited to 256x256, due to gpu memory limitation. Training on large texture dimension is possible but require more gpus.
* separating albedo color from light color is an ill-posed problem and some albedo skin tone can get baked in the estimated light. This is discussed in the paper.
 More details on these limitations can be found in the paper.
 
 # License
DeepNextFace is available for free, under GPL license, to use for research and educational purposes only. Any commercial usage if not allowed as the code source of DeepNextFace was released in the objective to help pushing the state-of-the art of monocular face reconstruction via self-supervised learning.  Please check LICENSE file. 


# Acknowledgements
 DeepNextFace relies on [NextFace](https://github.com/abdallahdib/NextFace/edit/main/README.md) for handling the rendering and morphable model part . [redner](https://github.com/BachiLi/redner/) is used for ray tracing, albedo model from [here](https://github.com/waps101/AlbedoMM/). Expression model is based on [FaceWareHouse3D dataset](http://kunzhou.net/zjugaps/facewarehouse/) similar to the one used by [Garrido et al., 2016](http://vcai.mpi-inf.mpg.de/projects/PersonalizedFaceRig/)

# contact 
mail: deeb.abdallah @at gmail

twitter: abdallah_dib

# Citation 
If you use DeepNextFace and find it useful in your work, these works are relevant for you:

```

@inproceedings{dib2021towards,
  title={Towards High Fidelity Monocular Face Reconstruction with Rich Reflectance using Self-supervised Learning and Ray Tracing},
  author={Dib, Abdallah and Thebault, Cedric and Ahn, Junghyun and Gosselin, Philippe-Henri and Theobalt, Christian and Chevallier, Louis},
  booktitle={Proceedings of the IEEE/CVF International Conference on Computer Vision},
  pages={12819--12829},
  year={2021}
}

@article{dib2022s2f2,
  title={S2F2: Self-Supervised High Fidelity Face Reconstruction from Monocular Image},
  author={Dib, Abdallah and Ahn, Junghyun and Thebault, Cedric and Gosselin, Philippe-Henri and Chevallier, Louis},
  journal={arXiv preprint arXiv:2203.07732},
  year={2022}
}

@inproceedings{dib2021practical,
  title={Practical face reconstruction via differentiable ray tracing},
  author={Dib, Abdallah and Bharaj, Gaurav and Ahn, Junghyun and Th{\'e}bault, C{\'e}dric and Gosselin, Philippe and Romeo, Marco and Chevallier, Louis},
  booktitle={Computer Graphics Forum},
  volume={40},
  number={2},
  pages={153--164},
  year={2021},
  organization={Wiley Online Library}
}

