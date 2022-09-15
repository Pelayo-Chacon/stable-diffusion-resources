# A MORON'S GUIDE TO STABLE DIFFUSION

The following is a guide to Stable Diffusion, with specific information as to how Voldy’s UI works. If you're using a different version of Stable Diffusion, I'd recommend following [this guide to switch over to Voldy's](https://github.com/Pelayo-Chacon/stable-diffusion-resources/blob/main/README.md). With that being said, a lot of the information contained within should still be helpful regardless of the distribution you're using. This is all based on my personal experience and the information I’ve been able to gather through it. If there’s anything I didn’t talk about that you’re curious to look into, [Voldy’s hosts a feature showcase](https://github.com/AUTOMATIC1111/stable-diffusion-webui-feature-showcase).

NEW FEATURES HAVE BEEN ADDED SINCE THIS GUIDE WAS DRAFTED, EXPLANATIONS WILL BE ADDED AS SOON AS POSSIBLE.

To change the default values of the UI, such as to allow for higher steps or larger batch sizes, you'll want to edit `ui-config.json`, which will appear in your root directory after launching Voldy's for the first time.

## txt2img
The `txt2img` tab is the standard version of Stable Diffusion you’re probably at least somewhat familiar with. It functions by taking a textual prompt and outputting a render. I’m going to go line by line through how each parameter functions (to the best of my knowledge).

**Prompt Line:** Prompts can be anything from long statements to short snippets tied together with commas. Stable Diffusion responds differently based on if you separate those statements or snippets with a comma, line, or period.
- Anything written earlier in the prompt is weighted more heavily, so moving the placement of snippets can make a big difference on the output.
- Putting `[brackets]` around a specific word or phrase will result in it appearing less in the prompt. The more `[[[brackets]]]` around the phrase, the heavier this will be weighted.
- The same can be said of `(parentheses)`, however with the opposite effect. The more `(((parentheses)))` around a word or phrase, the more likely it will appear or be prominent.
- There is a new called `Negative prompt` which allows you to tell Stable Diffusion to avoid certain elements. So far, I've used the keywords `mutations` or `deformed` to successfully avoid the borked arms the AI normally produces.
- Putting exclamation marks can have a weighted effect on words as well, though I personally haven’t messed around with this much.
- My opinion is that a perfected prompt will produce fairly consistent results through output batches. If you’re getting what you want some of the time, but not consistently, keep tweaking, it’ll be worth it.

**Roll:** This function will output a random artist at the end of your prompt. Artists will heavily influence the style of the output, so this feature can be interesting. The available pool of artists can be set from the `Settings` tab, which will be discussed in more detail below.

**Generate:** Self explanatory

**Sampling Steps:** This is how many steps the ai will take in producing the final output. Do not be fooled, more steps does not necessarily mean better quality. Each sampling method has its own sweet spot, as does each prompt. Experimentation is important, though I’ll go into this more below.

**Sampling Method:** These make all the difference in the world to your output. I’m going to list some of my favorites, as well as what I believe the sampling step “sweet spot” of each one is. The methods I don’t list aren’t necessarily bad, I just haven’t seen a reason to use them over the ones I like.
 - `Euler a` is my favorite sampling method.
	- It can produce great results in as little as 15 steps, with the variation between each subsequent step producing wildly different results.
	- I tend to stick on 20 when I’m prompt crafting, and more it around once I’ve perfected my prompt.
	- It can be output at higher steps, but I tend to move to `DPM2 a` if I’m going to do that.
 - `DDIM` is great for prompt crafting at the early stages.
	- It can output amazing results in as little as 8 steps and at the very least will give you a general idea of what your prompt will look like.
	- With that being said, I don’t tend to use this at higher steps or for finalized renders.
- `DPM2 a` will put out amazing results at **HIGH** steps.
	- It takes a lot longer to render and I generally won’t run it at anything less than 80 steps, but the results on a perfected prompt can be remarkable.
- `LMS` is considered to be the standard workhorse. 
	- It’ll put out consistent results at 50 steps.
	- I don’t see a reason to use this over others, but it’s what I started on, so I figured it was worth giving a mention to.

**Restore Faces:** This is a facial fixer. Keeping it off results in some borked looking features most of the time. This may have been fixed, but when CodeFormer was first integrated into Voldy's, you had to go to the `Settings` tab and manually chose a restoration model.

**Tiling:** I haven’t messed with this, so I honestly don’t know. I believe it creates repetitive patterns on larger outputs, but I can’t confirm or deny that. If you use this, let me know and I’ll add information to the guide.

**Batch Count:** How many images will be created in a row. The batch count limit can be raised by editing the `ui-config.json` located in your directory at `stable-diffusion\stable-diffusion-webui`. Batch size is ultimately determined by your VRAM, and rendering at larger width/height can result in batches crashing. I’ve run into this issue running large sized renders on a 3080, so use that as a benchmark.

**Batch Size:** I have no idea what this is meant to do. It overloads by VRAM every time I try to change it. If you figure it out, let me know.

**CFG Scale:** This determines how closely Stable Diffusion will follow your prompt. Lower values give more control to the AI, higher values give more to your prompt. I find the sweet spot to be between 7 and 11, and I personally use 8 when developing prompts.

**Height/width:** Fairly self explanatory. I’d recommend keeping at least one of them at 512 when adjusting the proportions since that’s the size the model was trained at. When rendering anything anthropomorphic, there’s a chance it will duplicate their head at taller or wider ratios. This can be fixed through prompting, but some will inevitably pop through.
> The standard `.bat` launcher I included in the [setup](https://github.com/Pelayo-Chacon/stable-diffusion-resources/blob/main/README.md) allows for larger rendering. This is best saved for landscapes and structures. Generally, there’s no real reason to do this since the results oftentimes look borked and all images can be upscaled later using ESRGAN anyway, but experiment around.

**Seed:** Each individual render outputs a seed which will allow you to duplicate that specific render on any distribution of Stable Diffusion running the 1.4 models. I’d recommend enabling the option to create a text file next to every image with generation parameters in `Settings`, which will include the seed information for that image, and allow you to easily reference your favorite seeds.
- You can tweak all of the settings, including the prompt, on a seed you like to finetune your overall settings for a specific prompt/idea.
- Unless you want to use a specific seed, set to -1, otherwise it will output the same image over and over.
- There is a new `extra` setting that I haven't messed with yet which I believe allows you to output seed variations on a batch. I will update with more information once I've had a chance to mess with this.

**Script:** I haven’t messed with this, but I know the x/y plot allows you to view the impact of variations to your prompt settings. If you use this, let me know so I can include more information about it.

**The buttons under the output:**
- `Save` will save a copy of the image, but this is largely irrelevant since it will already be in your output folder.
	- Voldy’s can be run on multiple devices on your local network, which is why the option exists.
	- If you choose to allow others to render on your network, remember it will all output to YOUR PC and use YOUR GPU power.
- `Send to img2img` will send the output currently in focus to the `img2img` tab.
- `Send to inpaint` will send the output currently in focus to the inpaint portion of the `img2img` tab.
- `Send to extras` will send the output currently in focus to the output `Extras` tab.
- `Interrupt` will interrupt the current render/batch.
- `Save prompt as style` allows you to save a prompt as an easily selectable output. A box to select will appear to the left of `Roll` after you save your first style, allowing you to make a selection. Prompts can be deleted by accessing `styles.csv` in the root directory and deleting the row they're in. This can be helpful if you find a combination that generations really good images and want to repeatedly use it with varied subjects.

## img2img

The `img2img` tab is where Stable Diffusion, and Voldy’s in particular, gets interesting. I won’t discuss anything that I already delved into on the `txt2img` tab. This function allows you to input any image (including a previous output) and have Stable Diffusion create variations of it. This can include placing an image in with no prompt, though I haven’t messed around with this personally. If a prompt is included, Stable Diffusion will take the image and make adjustments based around your prompt. This can be controlled through settings detailed below.

- **Drag Back Result:** If you really like a result, you can click `x` to remove the current input image, and drag that result directly from the output window into the input window in it's place to run further variations.

- **Redraw whole image:** will render an output based on the image, your prompt, and any other settings below.

- `Inpaint a part of image` will render only the selected part of the image based on the image, your prompt, and any other settings below.
	- I haven’t messed with this yet, but I’ve seen it used to fix issues with images.
	- The prompt can be changed to be something as simple as changing hair or eye color.
	- Since I haven’t messed with this, I’m unfamiliar with the mask settings, so if you use this, let me know so I can update the guide accordingly.

- **Loopback:** will render based on the most recent output from the “img2img” tab. 
	- This is really useless in my opinion since the color/quality begins to degrade after a while.
	- If you want to use `img2img` to fix or make variants of a specific output, I’d recommend loading that image directly through the `Redraw whole image` function and loading any improved results along the way in the same manner.

- **SD Upscale:** I haven’t used this to it's fullest potential yet, but I've seen it used very effectively to add detail into upscaled images.

- **Denoising strength:** This determines how much Stable Diffusion is going to keep the input image intact. The lower the strength, the less it will change.

- **Script:** `Img2img` includes what is called the `Poor man’s outpainting`. It functions similarly to the function you may have seen on DALLE-2, where existing images can be expanded outward.
	- I haven’t had any luck with results on this. If you figure out how to use it, let me know, because I’ve seen it work wonders.

## Other Tabs

The `Extras` tab is mostly useful for upscaling using any ESRGAN modules you loaded in. It’s pretty straightforward to use. You can double up upscalers if you so please. I personally recommend [Remacri](https://u.pcloud.link/publink/show?code=kZgSLsXZ0M1fT3kFGfRXg2tNtoUgbSI4kcSy) for landscapes and structures, and [Lollypop](https://drive.google.com/u/1/uc?id=10h8YXKKOQ61ANnwLjjHqXJdn4SbBuUku&export=download) for anything that has anthropomorphic figures. If you want to try out different models, you can find them [here](https://upscale.wiki/wiki/Model_Database). Anything that ends with `.pth` can be loaded by Voldy’s, but I haven’t tested any others.

The `PNG Info` tab allows you to load any images you've generated in and see information about them, including the prompt, steps, sampler, CFG scale, seed, and in the case of `img2img`, the denoising strength. This is invaluable.

The `Settings` tab is pretty essential. You can set your output directories here, which I’d personally recommend doing. I’d also recommend enabling the following option, which will create subfolders for each new prompt you try.

- [x]  When writing images/grids, create a directory with name derived from the prompt

If it's not automatically selected, you should also select CodeFormer as your face restoration model. I personally set my weight to 0.5. As with the above, and anytime you make setting on the `Settings` tab, make sure you hit `Apply Settings` at the top of the page. GFPGAN is okay, but tends to make everyone look like a KPOP star. The only other portion of the `Settings` tab worth noting is the selection boxed for random artist categories. Only those checked will appear when the `Roll` button is selected. Also, make sure you hit `Apply Settings` at the top of the page after you make any changes to the `Settings` tab, or you’ll lose those changes.
