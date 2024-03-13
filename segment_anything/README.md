# Segment Anything

Code from: https://github.com/facebookresearch/segment-anything

## Modifications

* `./modeling/mask_decoder.py`: fixed error with batch size > 1
* `./build_sam.py`: set device when loading weights to avoid errors in cpu-only environments

## Citation

```
@inproceedings{SAM,
      title={Segment Anything}, 
      author={Alexander Kirillov and Eric Mintun and Nikhila Ravi and Hanzi Mao and Chloe Rolland and Laura Gustafson and Tete Xiao and Spencer Whitehead and Alexander C. Berg and Wan-Yen Lo and Piotr Dollár and Ross Girshick},
      booktitle = {ICCV},
      year={2023},
}
```