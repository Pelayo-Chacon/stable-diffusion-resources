# A Moron's Collection of Stable Diffusion Resources

I put these resouces together to assist friends of mine in setting up Voldy's Stable Diffusion GUI. Hopefully sharing them here assists a few others in both setting up and understanding this exciting, and rapidly developing, technology. If there's anything not touched on here that you're interested in learning about, let me know and I'll attempt a guide to the best of my ability. Similarly, if there is any knowledge that you're interested in sharing, send it my way and I'll be happy to integrate it into this resource center.

# List of Guides:
- [Guide to Using Voldy's Stable Diffusion GUI](https://github.com/Pelayo-Chacon/stable-diffusion-resources/blob/main/USER-GUIDE.md)
- [Guide to Textual Inversion](https://github.com/Pelayo-Chacon/stable-diffusion-resources/blob/main/TEXTUAL-INVERSION.md)
- [Guide to Alternative Upscaling](https://github.com/Pelayo-Chacon/stable-diffusion-resources/blob/main/ALTERNATIVE-UPSCALE.md)
- [Prompt Crafting and Other Resources](https://github.com/Pelayo-Chacon/stable-diffusion-resources/blob/main/RESOURCES.md)

# A Moron's Guide to Setup Voly's Stable Diffusion GUI

So you want to take the dive into Stable Diffusion and the wide world of AI generated art, but you don’t know where to start. This is a guide to set up what I believe to be the best UI based distribution currently available. It’s frequently updated with features from various distributions and it’s free of the Patreon begging, Discord integrating, and potential malware bull shit that plagues many mainstream distributions. Going forward, I’m going to refer to this version as Voldemort’s, or Voldy’s for short. You can [inspect the code for Voldy’s here](https://github.com/AUTOMATIC1111/stable-diffusion-webui). Stable Diffusion only works well with a modern NVidia graphics card. If you’re running AMD or an old card, you’re probably shit out of luck.

## Download and install the following before you begin the setup process:
- [Python](https://www.python.org/downloads/release/python-3106/) - During installation, you'll see a note asking if you’d like to add Python to your PCs PATH. You do.
- [Git]([https://github.com/AUTOMATIC1111/stable-diffusion-webui](https://git-scm.com/download/win)

## Primary Setup

**Step 1:** Download the model checkpoint (currently 1.4) from [huggingface](https://huggingface.co/CompVis/stable-diffusion-v-1-4-original). You have to accept the license by registering for huggingface, which can be done by clicking a button that says `Access repository` and creating an account. There are two model checkpoint weights you can download, I’d personally recommend using `sd-v1-4-full-ema.ckpt`. It’s double the size so the download will take a bit, but it can lead to better results. It's apparently a bit of a memory hog though, so if you're running into memory issues, you may want to use `sd-v1-4.ckpt` instead.

**Step 2:** Once the download is complete, rename your chosen `.ckpt` file to `model.ckpt`.

**Step 3:** Download [GPFGAN](https://github.com/TencentARC/GFPGAN/releases/download/v1.3.0/GFPGANv1.3.pth), which fixes the borked faces Stable Diffusion produces most of the time. CodeFormer now comes standard with Voldy's, which does the same thing and produces better results for the most part, but this is still nice to experiment around with.

**Step 4:** Download ESRGAN models for upscaling final results. 
- [Remacri](https://drive.google.com/file/d/14pUxWLlOnzjZKOCsNguyNHchU6_581fc) is good for landscapes and structures.
- [Lollypop](https://drive.google.com/u/1/uc?id=10h8YXKKOQ61ANnwLjjHqXJdn4SbBuUku&export=download) is better for upscaling anything that has anthropomorphic figures.
- If you want to try out different models, you can find them [here](https://upscale.wiki/wiki/Model_Database). Anything that ends with `.pth` can be loaded by Voldy’s.

**Step 5:** In file explorer, create (or choose) a root directory (location on your PC where Voldy's will be stored) to download the files to. In my case, I cloned the files directly to my `C:\` drive, leading to a root directory location of: `C:\`

**Step 6:** Open command prompt in this directory. To open command prompt, press the `Windows key`, type `cmd`, and hit `Enter`. In the window that opens, enter the following command (you can copy and paste this and all following commands):

`cd C:\`

Alternatively, you can open command prompt to this directory through file explorer. To do so, make sure file explorer is in your newly created (or selected) directory and click on the navigation bar (which should say something along the lines of `This PC > OS Disk (C:)`). Clear anything on this bar, then type `cmd` and hit enter. Command prompt should open in the proper directory folder.

**Step 7:** To confirm you're in the right spot, enter the following command, which should send back your directory location. In my case it sent: `C:\”.

`echo %cd`

**Step 8:** Enter the following command, which will create a folder with the necessary files.

`git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui`

**Step 9:** In file explorer, navigate to the newly created `stable-diffusion-webui` directory (to confirm you're in the right place, look for a file called `webui.bat`). Move the `model.ckpt` and `GFPGANv1.3.pth` files you downloaded earlier into this directory.

**Step 10:**  In the same directory, right click on `webui-user.bat`, click `edit` and replace its contents with the following, saving your changes.

```
@echo off

set PYTHON=
set GIT=
set VENV_DIR=
set COMMANDLINE_ARGS=--medvram --opt-split-attention

git pull
start http://127.0.0.1:7860/

call webui.bat
```

**Step 11:** Navigate to `ESRGAN`. Move the `.pth` ESRGAN files you downloaded earlier, such as Remacri or Lollipop, into this folder.

**Step 12:** Navigate back to your root directory and double click `webui-user.bat` to launch. It will download some files the first time, so be patient. Once Voldy’s is fully launched, it should return a URL of `http://127.0.0.1:7860/` within the command prompt window. The launcher should have already navigated you there (you may need to refresh the page), but if accidentally closed it out and need to relaunch, go to that URL to view the UI and begin to render. To exit Voldy’s, close the command prompt window.

**Optional:** To launch from your desktop, copy the launcher `webui-use.bat` , then go to your desktop, right click, and click `paste shortcut`. You can now launch Voldy’s from your desktop.

## Setting Output Location

Once you launch Voldy’s, I would recommend setting your output folders (unless you’d prefer they output within your root directory). I was going to go hands off for this portion, but I'm feeling benevolent so I created a `.bat` to make this easier.

**Step 1:** Download the file below, and move it to wherever you want your images to output to. Run it, and it will create the appropriate sub-folders. You can delete the `.bat` after this is complete.

 - [Hand holding directory assignment .bat for friends](https://file.io/9WCbCrKdYHJV) - LINK DEAD, I WILL UPDATE SOON

**Step 2:** Go to the `Settings` tab of the UI and assign your new file locations accordingly. Once you’ve assigned the locations, make sure to hit `Apply Settings` at the top of the page.

I’d also recommend enabling the following option, which will create subfolders for each new prompt you try. There are other options available that I go through in my [guide on how to use Voldy’s](https://rentry.org/affxl).

- [x]  When writing images/grids, create a directory with name derived from the prompt

If it's not automatically selected, you should also select CodeFormer as your face restoration model. I personally set my weight to 0.5. As with the above, and anytime you make setting on the `Settings` tab, make sure you hit `Apply Settings` at the top of the page.

## Accessing Locally or Online
In all cases, the augments below are meant to replace `set COMMANDLINE_ARGS=` within `webui-user.bat`. The example lines will be shown using the recommend launch parameters from **Step 10** of the primary setup.

**To run online:** `set COMMANDLINE_ARGS=--medvram --opt-split-attention --share`
- You will see an xxx.app.gradio URL, which can be used to access from your preferred device.
- To assign a specific port, use the following command, replacing xxxx with your specified port.
	- `set COMMANDLINE_ARGS=--medvram --opt-split-attention --share --port xxxx`
	- Remember that all ports below 1024 need root/admin rights, for this reason it is advised to use a port above 1024.
- You may set up authentication for said gradio shared instance with the following command line, replacing user and pw with your selections:
	- `set COMMANDLINE_ARGS=--medvram --opt-split-attention --share --gradio-auth username:password`
	- Optionally, you can provide multiple sets of usernames and passwords separated by commas (user1:pw1, user2:pw2).

**To run locally:** `set COMMANDLINE_ARGS=--medvram --opt-split-attention --listen`
- This will allow computers on the same local network as your device to access the UI by going to the URL `http://127.0.0.1:7860/`.
- To assign a specific port, use the following command, replacing xxxx with your specified port.
	- `set COMMANDLINE_ARGS=--medvram --opt-split-attention --listen --port xxxx`
	- Remember that all ports below 1024 need root/admin rights, for this reason it is advised to use a port above 1024.

## Alternate Models
Two teams recently released models that were trained on anime images. If this interests you, you can download the [waifu-diffusion model here](https://thisanimedoesnotexist.ai/downloads/wd-v1-2-full-ema.ckpt), and the [trinart model here](https://huggingface.co/naclbit/trinart_stable_diffusion_v2/resolve/main/trinart2_step60000.ckpt). I haven't tested either yet, but I've seen some interesting results, so let me know your experience. To easily switch between either of these and the main model, follow the steps below.

**Step 1:** In file explorer, your root directory at `stable-diffusion-webui`. This is the directory containing `webui-user.bat`.

**Step 2:** Move the `wd-v1-2-full-emma.ckpt` or `trinart2_step60000.ckpt` you downloaded into this folder, without renaming.

**Step 4:** Copy `webui-user.bat` and rename the copy to `webui-user-waifu` or `webui-user-trinart` respectively.

**Step 5:** Right click on the copy to edit within notepad and replace its contents with the following, saving your changes.

**For `webui-user-waifu.bat`:**

```
@echo off

set PYTHON=
set GIT=
set VENV_DIR=
set COMMANDLINE_ARGS=--ckpt wd-v1-2-full-emma.ckpt --medvram --opt-split-attention

git pull
start http://127.0.0.1:7860/

call webui.bat
```

- Pruning `wd-v1-2-full-emma.ckpt` to reduce VRAM usage and loading time
	- The Waifu diffusion model is normally 7GB due to redundant training data, but it can be reduced to 3.6GB without any loss of quality
	- Download [`prune.py`](https://github.com/harubaru/waifu-diffusion/blob/main/scripts/prune.py)
	- Right click on `prune.py`, click `edit`, and modify as follows:
		- Change the last line of `prune.py` to the location of  `wd-v1-2-full-emma.ckpt` on your PC.
	- Open command prompt in this directory, following these steps if you're unsure of how to do so:
		- Make sure file explorer is in the location of `prune.py` on your system
		-  Click on the navigation bar (which should say something along the lines of `This PC > OS Disk (C:) > YOUR LOCATION`).
		- Clear anything on this bar, then type `cmd` and hit enter. Command prompt should open in the proper directory folder.
	- Enter the following command:

		`python prune.py`

	- You will now have a pruned `.ckpt`.

**For `webui-user-trinart.bat`:**

```
@echo off

set PYTHON=
set GIT=
set VENV_DIR=
set COMMANDLINE_ARGS=--ckpt trinart2_step60000.ckpt --medvram --opt-split-attention
git pull
start http://127.0.0.1:7860/

call webui.bat
```

**Optional:** To launch from your desktop, copy the launcher `webui-use.bat` , then go to your desktop, right click, and click `paste shortcut`. You can now launch Voldy’s from your desktop.
