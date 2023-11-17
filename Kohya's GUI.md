# Kohya's GUI
This is a note on how to train the LoRA model using Kohya's GUI.
  
[LoRA training params official wiki](https://github.com/bmaltais/kohya_ss/wiki/LoRA-training-parameters#explaining-lora-learning-settings-using-kohya_ss-for-stable-diffusion-understanding-by-everyone)
  
## Prior knowledge
Regularization Images can help alleviate overfitting.
  
Total steps = (`number of images` * `number of repeats` + `regularized image` * `number of repeats`) * `number of epochs` / `batch size`  
**If you do not use `regularized image`, `number of repeats` should set `1`**
  
In general, the `total steps` should be around 2000-3000 to avoid overfitting.  


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
  
Or you can select any models (LoRA may be created that depends on its model.)


### Folders, Folder structure
T.B.D.

### Parameters


Basic tab
  
- Optimizer
  - `DAdaptAdam`, `AdamW`

- Learning rate
  - `0.0001` - `0.00005` (1e-4 - 5e-5)
    - If optimizer is set to `DAdaptAdam` this value should be `1`.

- Network Rank (Dimension) ([❓](https://github.com/bmaltais/kohya_ss/wiki/LoRA-training-parameters#network-rank-dimension))
  - `16-128`
>The larger the number of neurons , the more learning information can be stored, but the possibility of learning unnecessary information other than the learning target increases, and the LoRA file size also increases.
>Generally, it is often set to a maximum of about 128, but there are reports that 32 is sufficient.
>When making LoRA on a trial basis, it may be better to start from around 2 to 8.

- Network Alpha ([❓](https://github.com/bmaltais/kohya_ss/wiki/LoRA-training-parameters#network-alpha))
  - `8-128`
    - This value depends on NetworkRank.
>*Network Alpha value must not exceed Network Rank value. It is possible to specify a higher number, but there is a high probability that it will result in an unintended LoRA.
>Also, when setting the Network Alpha, you should consider the effect on the learning rate.
>For example, with an Alpha of 16 and a Rank of 32, the strength of the weight used is 16/32 = 0.5, meaning that the learning rate is only half as powerful as the Learning Rate setting.

- Max resolution
  - `512,512` or `768,768`
  - For LoRA XL
    - `1024,1024`
>Specify the maximum resolution of training images in the order of "width, height". If the training images exceed the resolution specified here, they will be scaled down to this resolution.
  
  
Advanced tab  
  
- Keep n tokens
  - set `1 or higher` if `Shuffle caption` is enabled.

- Clip skip
  - `2`


