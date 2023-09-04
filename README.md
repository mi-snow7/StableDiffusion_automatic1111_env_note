# My StableDiffusion automatic1111 v1.6.0 environment and notes
## SET-UP automatic1111
### 1. Download StableDiffusion WebUI(automatic1111)
```
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
```


### 2. Install python v3.10

require 3.10 for xformers  
https://www.python.org/downloads/


### 3. Modify webui-user.bat
- Add arguments `--medvram --opt-split-attention --xformers --no-half` in `COMMANDLINE_ARGS`  
- Add path to python v3.10 `C:\Users\USERNAMEHERE\AppData\Local\Programs\Python\Python310\python.exe`

```
@echo off

set PYTHON="C:\Users\USERNAMEHERE\AppData\Local\Programs\Python\Python310\python.exe"
set GIT=
set VENV_DIR=
set COMMANDLINE_ARGS=--medvram --opt-split-attention --xformers --no-half

call webui.bat

```


### 4. Run(double click) webui-user.bat

### 5. Install automatic1111 extensions
Install these extensions from Extensions->Available tab.
**Mandatory**
- https://github.com/LEv145/--sd-webui-ar-plus
  - aspect ratio selector
- https://github.com/butaixianran/Stable-Diffusion-Webui-Civitai-Helper
- ~~https://github.com/KohakuBlueleaf/a1111-sd-webui-lycoris.git~~
  - No longer needed for webui >= 1.5.0
- https://github.com/Bing-su/adetailer
  - after detailer
- https://github.com/Mikubill/sd-webui-controlnet.git
  - ControlNet models: https://huggingface.co/webui/ControlNet-modules-safetensors/tree/main
- https://github.com/pkuliyi2015/multidiffusion-upscaler-for-automatic1111.git
  - Tiled Diffusion & VAE
- https://github.com/hako-mikan/sd-webui-lora-block-weight.git
  - [weights settings](#weights-settings)
  - [LoRA Block Weight](#Lora-block-weight)
- https://github.com/hnmr293/sd-webui-llul
  - Local Latent upscaLer
- https://github.com/toshiaki1729/stable-diffusion-webui-dataset-tag-editor
  - needs to tagging to train images
- https://github.com/a2569875/stable-diffusion-webui-composable-lora.git
  - Install from Extension index URL.
  - Use this extension with latent couple instead of RegionalPrompter.
    -  RegionalPrompter happened some critical error in my env.
- https://github.com/ashen-sensored/stable-diffusion-webui-two-shot
  - Latent Couple extension
- https://github.com/hako-mikan/sd-webui-supermerger
  - LoRA merge tool: SuperMerger

**Optional**  
- https://github.com/Coyote-A/ultimate-upscale-for-automatic1111.git
- https://github.com/nonnonstop/sd-webui-3d-open-pose-editor.git

  
### 6. Install VAE
Add files into `\stable-diffusion-webui\models/VAE`
- kl-f8-anime2.ckpt
  - https://huggingface.co/hakurei/waifu-diffusion-v1-4/tree/main/vae
- Counterfeit-V2.5.vae.pt
  - https://huggingface.co/gsdf/Counterfeit-V2.5/tree/main
- vae-ft-mse-840000-ema-pruned.safetensors
  - https://huggingface.co/stabilityai/sd-vae-ft-mse-original/tree/main
- orangemix.vae.pt
  - https://huggingface.co/WarriorMama777/OrangeMixs/tree/main/VAEs

### 7. Change automatic1111 settings
- User interface
  - Quicksettings list (setting entries that appear at the top of page rather than in settings tab) (requires restart)
    - Add `sd_model_checkpoint`, `sd_vae`, `CLIP_stop_at_last_layers`
    - **Set Clip skip to 2 after UI reloaded**

### 8. Download checkpoints, LoRA, LyCORIS
Add checkpoint models into `\stable-diffusion-webui\models\Stable-diffusion`  
Add LoRA and LyCORIS models into `\stable-diffusion-webui\models\Lora`  
https://civitai.com/

### 9. Install Textual Inversion
Add files into `\stable-diffusion-webui\embeddings`
- [badhandv4](https://civitai.com/models/16993)
- [EasyNegative](https://civitai.com/models/7808)
- [negative_hand Negative Embedding](https://civitai.com/models/56519)


## TIPS, Another tools
### TOOLS
- [Kohya's GUI](https://github.com/bmaltais/kohya_ss)
  - SET-UP (T.B.D.)
- https://github.com/Sanster/lama-cleaner
  - Lama cleaner

### ControlNet tile_resample upscaling params
Don't forget **Disable ADetailer**
- Common settings
  - Sampling method: Euler a, DPM++ 2M Karras, DDIM, etc
  - Sampling steps: Same as source image or 32-64 or higher
  - Upscaler: SwinIR_4x, R-ESRGAN 4x+, R-ESRGAN 4x+ Anime6B
  - Hires.fix : Enabled
  - Hires step: 0
  - Denoising strength: 0.3-0.5
- T2I
  - Set source image in Single Image tab
  - Enable Pixel Perfect (optional)
  - Enable Allow Preview
  - ControlType: Tile
    - Preprocessor: tile_resample
    - Model: control_v11f1e_sd15_tile
  - Down Sampling Rate: 1~3 (each individual case)
  - Control Mode: Default
  - Resize Mode: Default
  - Modify prompt (optional)
    - Change Lora weight from 0.7 to 0.4
    - Change Lora block weight
    - Change facial, hair colors, background and ...etc prompts
- I2I
  - Resize mode: Resize and fill
  - Denoising strength: 0.3-0.5
  - **ControlNet Preprocessor: none**
### LoRA block weights format on a1111-v1.5.0
```<lora:flat2:-0.3:lbw=1,1,1,1,1,0,0,0,1,1,1,1,1,1,1,0,0>```

## XX. settings, params
#### weights settings
```
F:0,0,0,0,0,0,0,0,1,1,1,0,0,0,0,0,0
NF:1,1,1,1,1,1,1,1,0,0,0,1,1,1,1,1,1

CHARA:1,1,1,1,1,0,0,0,1,1,1,1,1,1,1,0,0
BG:1,1,1,1,1,1,0.2,1,0.2,0,0,0.8,1,1,1,0,0

NONE:0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
ALL:1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1
INS:1,1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0
IND:1,0,0,0,1,1,1,0,0,0,0,0,0,0,0,0,0
INALL:1,1,1,1,1,1,1,0,0,0,0,0,0,0,0,0,0
MIDD:1,0,0,0,1,1,1,1,1,1,1,1,0,0,0,0,0
OUTD:1,0,0,0,0,0,0,0,1,1,1,1,0,0,0,0,0
OUTS:1,0,0,0,0,0,0,0,0,0,0,0,1,1,1,1,1
OUTALL:1,0,0,0,0,0,0,0,1,1,1,1,1,1,1,1,1
ALL0.5:0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.5

LC-Face:0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1,0,1,1,1,0,0,1
LC-NCNF:1,1,1,1,1,1,1,1,1,1,1,1,1,1,0,1,1,0,0,0,1,1,1,1,0,0
LC-NF:1,1,1,1,1,1,1,1,1,1,1,1,1,1,0,1,1,0,0,0,1,1,1,1,1,1
LC-NC:1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,0,0
LC-NPNBASE:0,1,1,1,1,1,1,1,0,0,0,0,0,0,1,1,1,1,1,1,1,1,1,1,0,0
LC-NP:1,1,1,1,1,1,1,1,0,0,0,0,0,0,1,1,1,1,1,1,1,1,1,1,0,0
LC-NIN:1,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1,1,1,1,1,1,1,1,1,1,1
LC-CT:0,0,0,0,0,0,0,0,0,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1
```
#### Lora block weight
```
F,NF,CHARA,BG,NONE,ALL,INS,IND,INALL,MIDD,OUTD,OUTS,OUTALL,ALL0.5,LC-Face,LC-NCNF,LC-NF,LC-NC,LC-NPNBASE,LC-NP,LC-NIN,LC-CT
```
