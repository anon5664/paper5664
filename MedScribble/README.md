
# MedScribble

We collected a dataset (`MedScribble`) of manual scribbles from three annotators for seven biomedical image segmentation tasks. The dataset contains a total of 31 2D image-segmentation pairs with 3 sets of scribble annotations for each image-segmentation pair. For each segmentation task (i.e., dataset/label combination) the annotators were shown 5 training examples with the ground truth segmentation per task and instructed to draw positive scribbles on the region of interest and negative scribbles on the background for 3-5 new images. Annotators drew the scribbles in a Gradio web app. Annotators 1 and 2 used an iPad with stylus and Annotator 3 used a laptop trackpad to draw scribbles. 

See [tutorial.ipynb](https://github.com/anon5664/paper5664/blob/main/MedScribble/tutorial.ipynb) for a preview of the dataset.

We selected 7 segmentation tasks from 7 different public biomedical image segmentation datasets. See the list of data sources below for the sources of the images and ground truth segmentations. All images were padded sqaure before being resized to 256x256 and rescaled to [0,1]. For 3D datasets, we took either the middle slice (`midslice`) or slice with maximum label area (`maxslice`) as indicated by the folder name.

Each example folder contains 5 files:
```
    img.npy
    seg.npy
    scribble_1.npy
    scribble_2.npy
    scribble_3.npy
```
The scribble annotations (`scribble_X.npy`) for each annotator are stored as a 2x256x256 array where the 1st channel contains positive (label) scribbles and the second channel contains negative (background) scribbles.  

# Data Sources

Please cite the original data sources for the images and segmentations. 

For SpineWeb, you will need to follow the instructions on the [website](http://spineweb.digitalimaginggroup.ca/Index.php?n=Main.Datasets#Dataset_7.3A_Intervertebral_Disc_Localization_and_Segmentation.3A_3D_T2-weighted_Turbo_Spin_Echo_MR_image_Database) to retrieve Dataset 7. Then perform the following processing steps for `Subject04`, `Subject13`, and `Subject14`:

1. Resample the to 1mmx1mmx1mm spacing 
2. Pad with zeros to be square
3. Resize to 256x256x256
4. Clip values to [0.5, 99.5] percentiles and rescale be on [0,1]
5. Take the middle slice 

For the other datasets, we provide the relevant slices and segmentations. 

## ACDC

owner: University Hospital of Dijon

website: https://www.creatis.insa-lyon.fr/Challenge/acdc/databases.html

citation:
```
@article{ACDC,
  title={Deep learning techniques for automatic MRI cardiac multi-structures segmentation and diagnosis: is the problem solved?},
  author={Bernard, Olivier and Lalande, Alain and Zotti, Clement and Cervenansky, Frederick and Yang, Xin and Heng, Pheng-Ann and Cetin, Irem and Lekadir, Karim and Camara, Oscar and Ballester, Miguel Angel Gonzalez and others},
  journal={IEEE transactions on medical imaging},
  volume={37},
  number={11},
  pages={2514--2525},
  year={2018},
  publisher={ieee}
  doi={10.1109/TMI.2018.2837502}
}
```

## BTCV (Cervix)

website: https://www.synapse.org/#!Synapse:syn3193805/wiki/217790

license: [CC by 4.0](https://creativecommons.org/licenses/by/4.0/)

citation:
```
@inproceedings{BTCV,
  title={Miccai multi-atlas labeling beyond the cranial vault--workshop and challenge},
  author={Landman, Bennett and Xu, Zhoubing and Igelsias, J and Styner, Martin and Langerak, T and Klein, Arno},
  booktitle={Proc. MICCAI Multi-Atlas Labeling Beyond Cranial Vault Workshop Challenge},
  volume={5},
  pages={12},
  year={2015}
}
```

## HipXRay

website: https://data.mendeley.com/datasets/zm6bxzhmfz/1

license: [CC by 4.0](https://creativecommons.org/licenses/by/4.0/)

```
@article{HipXRay,
	title = {X-ray images of the hip joints},
	volume = {1},
	url = {https://data.mendeley.com/datasets/zm6bxzhmfz/1},
	doi = {10.17632/zm6bxzhmfz.1},
	language = {en},
	urldate = {2023-09-03},
	author = {Gut, Daniel},
	month = jul,
	year = {2021},
	note = {Publisher: Mendeley Data},
}
```

## PanDental

website: https://data.mendeley.com/datasets/hxt48yk462/2

license: [CC BY NC 3.0](https://creativecommons.org/licenses/by-nc/3.0/)

citation:
```
@article{PanDental,
  title={Automatic segmentation of mandible in panoramic x-ray},
  author={Abdi, Amir Hossein and Kasaei, Shohreh and Mehdizadeh, Mojdeh},
  journal={Journal of Medical Imaging},
  volume={2},
  number={4},
  pages={044003},
  year={2015},
  publisher={SPIE}
}
```

## SCD

website: https://www.cardiacatlas.org/sunnybrook-cardiac-data/

license: [CC0 1.0 DEED](https://creativecommons.org/publicdomain/zero/1.0/)

citation:
```
@article{SCD,
  title={Evaluation framework for algorithms segmenting short axis cardiac MRI},
  author={Radau, Perry and Lu, Yingli and Connelly, Kim and Paul, Gideon and Dick, AJWG and Wright, Graham},
  journal={The MIDAS Journal-Cardiac MR Left Ventricle Segmentation Challenge},
  volume={49},
  year={2009}
}

```

## SpineWeb (Dataset 7)

website: http://spineweb.digitalimaginggroup.ca/Index.php?n=Main.Datasets#Dataset_7.3A_Intervertebral_Disc_Localization_and_Segmentation.3A_3D_T2-weighted_Turbo_Spin_Echo_MR_image_Database

citation:
```
@article{SpineWeb,
  title={Evaluation and comparison of 3D intervertebral disc localization and segmentation methods for 3D T2 MR data: A grand challenge},
  author={Zheng, Guoyan and Chu, Chengwen and Belav{\`y}, Daniel L and Ibragimov, Bulat and Korez, Robert and Vrtovec, Toma{\v{z}} and Hutt, Hugo and Everson, Richard and Meakin, Judith and Andrade, Isabel L{\u{o}}pez and others},
  journal={Medical image analysis},
  volume={35},
  pages={327--344},
  year={2017},
  publisher={Elsevier}
}
```

## WBC

website: https://github.com/zxaoyou/segmentation_WBC

license: [GNU General Public License v3.0](https://github.com/zxaoyou/segmentation_WBC/blob/master/LICENSE)

citation:
```
@article{WBC,
  title={Fast and Robust Segmentation of White Blood Cell Images by Self-supervised Learning},
  author={Xin Zheng and Yong Wang and Guoyou Wang and Jianguo Liu},
  journal={Micron},
  volume={107},
  pages={55--71},
  year={2018},
  publisher={Elsevier}
  doi={https://doi.org/10.1016/j.micron.2018.01.010},
  url={https://www.sciencedirect.com/science/article/pii/S0968432817303037}
}
```
