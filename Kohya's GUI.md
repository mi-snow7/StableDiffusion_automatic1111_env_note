# Kohya's GUI
This is a note on how to train the LoRA model using Kohya's GUI.
  
## Prior knowledge
Regularization Images can help alleviate overfitting.
  
Total steps = (`number of images` * `number of repeats` + `regularized image` * `number of repeats`) * `number of epochs` / `batch size`  
**If you do not use `regularized image`, `number of repeats` should set `1`**
  
In general, the `total steps` should be around 2000 to avoid overfitting.  
However, in my experience I have been able to get good results with the following settings.  
(It took me 40 min to complete LoRA training)  
`number of images` = 130, `number of repeats` = 1, `number of epochs` = 30-50, `regularized image` = NONE  


## SET-UP Kohya's GUI
### 1. T.B.D.


### 2. T.B.D.


## Lora params

### Source model
**Recommend**  
- [AnyLoRA](https://civitai.com/models/23900/anylora-checkpoint)
  - For anime style LoRA
- [SD1.5 base model](https://huggingface.co/runwayml/stable-diffusion-v1-5/tree/main)
  - For realistic style LoRA


### Folders, Folder structure
T.B.D.

### Parameters


Basic tab
  
- Optimizer
  - `AdamW`

- Learning rate
  - `0.00005`

- Network Rank (Dimension)
  - `32-128`

- Network Alpha
  - `32-128`
  
  
Advanced tab  
  
- Keep n tokens
  - set `1 or higher` if `Shuffle caption` is enabled.

- Clip skip
  - `2`


