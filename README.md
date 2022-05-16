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
