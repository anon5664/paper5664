# Paper ID 5664

Supplemental material for anonymous paper submission #5664: "ScribblePrompt: Fast and Flexible Interactive Segmentation for any Biomedical Image"

## Contents

This repository contains
* [**GIFs**](#gifs) showing additional example segmentations
* The [**MedScribble Dataset**](#medscribble-dataset) of manual scribble annotations
* [**Scribble Simulation Code**](#scribble-simulation-code)
* [**Inference Code**](#inference-code)

Other supplemental materials
* **Interactive online demo**: https://huggingface.co/spaces/anon5664/ScribblePrompt
* **Demo video**: https://www.youtube.com/watch?v=N5AA8JndQTk

## GIFs

These GIFs show example predictions from ScribblePrompt-UNet on test examples from evaluation dataset unseen during training.

![](https://github.com/anon5664/paper5664/blob/main/gifs/total_segmentator.gif)
![](https://github.com/anon5664/paper5664/blob/main/gifs/wbc.gif)
![](https://github.com/anon5664/paper5664/blob/main/gifs/drive.gif)
![](https://github.com/anon5664/paper5664/blob/main/gifs/buid.gif)
![](https://github.com/anon5664/paper5664/blob/main/gifs/hipxray.gif)
![](https://github.com/anon5664/paper5664/blob/main/gifs/acdc.gif)

## MedScribble Dataset

We provide a description of the MedScribble dataset in [`MedScribble/README.md`](https://github.com/anon5664/paper5664/blob/main/MedScribble/README.md) and show a preview of the dataset in [`MedScribble/tutorial.ipynb`](https://github.com/anon5664/paper5664/blob/main/MedScribble/tutorial.ipynb)

## Scribble Simulation Code

We provide scribble simulation code in [`scribbleprompt/scribbles.py`](https://github.com/anon5664/paper5664/blob/main/scribbleprompt/scribbles.py). To generate scribbles, run

```
From scribbleprompt.scribbles import ContourScribble, CenterlineScribble, LineScribble
scribble_gen = LineScribble()
scribble_gen(mask, n_scribbles=1)
```
where mask is a torch.Tensor with size (b,1,H,W) or (1,H,W) with values in [0,1].

## Inference Code  

We provide checkpoints for two versions of ScribblePrompt:

* **ScribblePrompt-UNet** with an efficient fully-convolutional architecture  

* **ScribblePrompt-SAM** based on the [Segment Anything Model](https://github.com/facebookresearch/segment-anything)

Both models have been trained with iterative **scribbles, click, and bounding box interactions** on a diverse collection of 65 medical imaging datasets with both real and synthetic labels. 

To instantiate [ScribblePrompt-UNet](https://github.com/anon5664/paper5664/blob/main/scribbleprompt/unet.py) and make a prediction:
```
from scribbleprompt import ScribblePromptUNet

sp_unet = ScribblePromptUNet()

mask = sp_unet.predict(
    image,        # (B, 1, H, W) 
    point_coords, # (B, n, 2)
    point_labels, # (B, n)
    scribbles,    # (B, 2, H, W)
    box,          # (B, n, 4)
    mask_input,   # (B, 1, H, W)
) # -> (B, 1, H, W) 
```

To instantiate [ScribblePrompt-SAM](https://github.com/anon5664/paper5664/blob/main/scribbleprompt/sam.py) and make a prediction:
```
from scribbleprompt import ScribblePromptSAM

sp_sam = ScribblePromptSAM()

mask, img_features, low_res_logits = sp_sam.predict(
    image,        # (B, 1, H, W) 
    point_coords, # (B, n, 2)
    point_labels, # (B, n)
    scribbles,    # (B, 2, H, W)
    box,          # (B, n, 4)
    mask_input,   # (B, 1, 256, 256)
) # -> (B, 1, H, W), (B, 16, 256, 256), (B, 1, 256, 256)

```
`image` should have spatial dimensions $(H,W) = (128,128)$ and pixel values min-max normalized to the $[0,1]$ range. 

For ScribblePrompt-UNet, `mask_input` should be the logits from the previous prediction. For ScribblePrompt-SAM, `mask_input` should be `low_res_logits` from the previous prediction. 

## Acknowledgements

Code for ScribblePrompt SAM builds on [Segment Anything](https://github.com/facebookresearch/segment-anything) 
