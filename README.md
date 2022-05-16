# DeepNextFace (Towards High Fidelity Monocular Face Reconstruction using Self-supervised Learning and Ray Tracing) -- ICCV 2021 --
DeepNextFace is a 3D face reconstruction library from a single monocular RGB image via deep convolutional neural networks and differentiable ray tracing. It achieves fast, robust and stable 3D face reconstruction. From a single RGB image, DeepNextFace estimates face geometry, spatially-varying skin reflectance (diffuse and specular albedos), scene light and head pose. The library uses the differentiable rendering layer of [NextFace](https://github.com/abdallahdib/NextFace/). This repository is a reproduction of our [ICCV 2021 paper](https://openaccess.thecvf.com/content/ICCV2021/papers/Dib_Towards_High_Fidelity_Monocular_Face_Reconstruction_With_Rich_Reflectance_Using_ICCV_2021_paper.pdf)
<p align="center"><img src="resources/teaser1.gif" style="float: left; width: 60%; margin-right: 1%; margin-bottom: 0.5em;"></p>
<p align="center"><img src="resources/teaser4.gif" style="float: left; width: 60%; margin-right: 1%; margin-bottom: 0.5em;"></p>

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
DeepNextFace is a reproduction of [our early work](https://openaccess.thecvf.com/content/ICCV2021/papers/Dib_Towards_High_Fidelity_Monocular_Face_Reconstruction_With_Rich_Reflectance_Using_ICCV_2021_paper.pdf)>  with some slight differences (see below). 
The network architecture is composed mainly of two stages. First, a resnet encoder takes as input an RGB image and project it into a latent code, a fully connected layer takes as input the latent code and predicts the 3DMM parameters (shape identity, expression), head pose (rotation translation), camera (focal) and scene light (with spherical harmonics). The second stage is composed of two decoders, trained to reconstruct a delta diffuse and specular maps from the latent code. These detlta maps are added on top of the statistical albedo maps (obtained from the first stage) to captrue medium-frequency albedo details outside the span of the statistical prior space. This allow to capture more details in the final reflectance maps (such as beards and makeup). Please note that there is some slight difference in the network trained here and the one in our paper.
