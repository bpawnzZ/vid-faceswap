## vid-faceswap (Updated Fork)

**⚠️ IMPORTANT: This is an updated fork of the original vid-faceswap extension that fixes compatibility issues with SD WebUI 1.10.1+**

This extension is for AUTOMATIC1111's [Stable Diffusion web UI](https://github.com/AUTOMATIC1111/stable-diffusion-webui).
It adds a tab dedicated to faceswapping of videos.

### 🚀 What's Fixed in This Fork

This version fixes the following issues that occur in the original extension with SD WebUI 1.10.1+:

1. **Fixed missing `create_sampler_and_steps_selection` import** - Replaced with manual UI creation
2. **Fixed missing `create_seed_inputs` import** - Replaced with manual seed input controls
3. **Fixed `moviepy.editor` import error** - Updated to use correct `moviepy` import path
4. **Updated for SD WebUI 1.10.1+ compatibility** - Works with the latest stable-diffusion-webui versions

### 📦 Installation

**From this fork (recommended for SD WebUI 1.10.1+):**
1. Open "Extensions" tab in SD WebUI
2. Open "Install from URL" tab
3. Enter: `https://github.com/bpawnzZ/vid-faceswap.git`
4. Press "Install" button
5. Restart Web UI

**From original (may not work with SD WebUI 1.10.1+):**
Use the original URL: `https://github.com/dchatel/vid-faceswap`

<img width="960" alt="" src="interface.png">

Example of swap from Anya Taylor-Joy to Scarlett Johansson, using denoising strength 0.2 and controlnet depth and canny (click to see it on youtube):

[![Anya Talor-Joy to Scarlett Johansson](https://img.youtube.com/vi/TipAErBhazg/hqdefault.jpg)](https://youtu.be/TipAErBhazg)

### 🛠️ Additional Installation Steps

5. **(optional) Install rife-ncnn-vulkan-python** for frame interpolation
6. Restart Web UI.

#### What is rife-ncnn-vulk-python and how to install it ?

RIFE stands for Real-Time Intermediate Flow Estimation. This will allows you to turn a video with a low fps to a video with high fps. 

vid-faceswap uses it to save stable-diffusion image generations, which are costly, and then interpolate the missing frames. This also leads to better videos with less temporal incoherence issues.

### Linux Installation:
```bash
# Standard installation (may work for most users)
pip install rife-ncnn-vulkan-python

# If you encounter CMake policy errors, use:
CMAKE_POLICY_VERSION_MINIMUM=3.31 /path/to/your/python -m pip install rife-ncnn-vulkan-python

# Example with SD WebUI conda environment:
CMAKE_POLICY_VERSION_MINIMUM=3.31 /home/insomnia/miniconda/envs/sd-webui/bin/python -m pip install rife-ncnn-vulkan-python
```

### Windows Installation:
On windows, pip will likely give you an error, as it will not be able to compile rife. So, instead you can [download the last version of RIFE](https://github.com/media2x/rife-ncnn-vulkan-python/releases). Don't forget to click "show all assets" if windows versions do not show up. Extract the whl file contained in the zip and run the command: ```pip install path-to-extracted-whl-file```

**Note:** Replace `/path/to/your/python` with your actual Python executable path (e.g., from your conda/virtual environment).

### Usage tips

- Maximum FPS will limit the number of frames that will be processed by stable diffusion. For example, if you have a 30 fps video and you set maximum fps to 10, it will only process 1/3 of the frames, saving as much computational time, energy, etc...
- Target FPS uses RIFE to bring the fps of the output video to that number of fps. For example, if you have a 30 fps video, and you've set maximum fps to 10, but also set target fps to 60, you'll end up with a 60 fps video for 1/6 of the computational cost.
- It's generally a good idea to set a low maximum fps and high target fps. This helps reduce temporal incoherence.
- A relatively low denoising strength is basically needed if you want to avoid as much temporal incoherence as possible. But you can go as high as you want, especially if you use controlnet. Feel free to experiment.

### Supported file formats

- Anything supported by ffmpeg (mp4, mkv, webm, gif, etc.)
- Animated webp

---

### 🔧 Technical Details

**Changes made in this fork:**
- **Line 15 in `scripts/vid_faceswap.py`**: Changed import from `modules.ui` to `modules.ui_common` for `create_refresh_button`
- **Lines 189-209 in `scripts/vid_faceswap.py`**: Replaced `create_sampler_and_steps_selection` and `create_seed_inputs` with manual UI creation
- **Line 5 in `scripts/video.py`**: Fixed `moviepy.editor` import to use `moviepy` directly

**Compatibility:** Tested with SD WebUI 1.10.1

**Original Repository:** https://github.com/dchatel/vid-faceswap

**Maintained by:** [bpawnzZ](https://github.com/bpawnzZ)