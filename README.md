# The Textual Inversion Library

Some anons were requesting a space they could host a textual inversion library, sepearate from the one maintained by Hugging Face, so here it is. Feel free to use the wiki to post any models that you've worked up.

# A MORON'S GUIDE TO TEXTUAL INVERSION

This is the new hotness in the world of AI generated imagery. Textual inversion allows you to train data sets of specific styles or things, which will then be tied to a specific word. It does this without affecting how the model file works as a whole, allowing you to inject keyword shortcuts. If that doesn't excite you, let me simply by saying - this lets you tie a keyword to specific people, things, places, or art styles in Stable Diffusion that you otherwise would be unable to directly reference. It's a game changer.

I was going to integrate this into my [main setup guide](https://rentry.org/zfawb) for Stable Diffusion, but it has enough moving parts that I think it's worth going into on it's own, namely in the fact that a new folder needs to be created in the root directory of Voldy's. With that being said, if you haven't already set Stable Diffusion up, you'll want to do that before consulting this guide.

## Prepare Voldy's to receive the horrors.

**Step 1:** In file explorer, navigate to your root stable diffusion directory (mine is `C:\stable-diffusion-voldy`). Create a new folder in this location called `embeddings` (this may be created by default now, but it wasn't when I made this guide, so if it's there, obviously ignore this).

**Step 2:** To make sure this works, go to the [Stable Diffusion concepts library](https://huggingface.co/sd-concepts-library) and pick a model that tickles your fancy and `git clone` that model into your newly created embeddings folder (I will explain how next).

**Step 3:** Open command prompt from your embeddings folder (mine is at `C:\stable-diffusion-voldy\embeddings`). To do so, make sure you're within your `embeddings` folder in file explorer and click on the navigation bar (which should say something along the lines of This PC > OS Disk (C:) > stable-diffusion-voldy > embeddings). Type cmd on this bar and hit enter. Command prompt should open in the proper directory.

**Step 4:** I'm going to clone [this model](https://huggingface.co/sd-concepts-library/line-art), which as the name implies allows you to consistency produce a line art style. To do this, I'm going to type `git clone https://huggingface.co/sd-concepts-library/line-art` and hit `enter`. That's it. The same concept applies to any model you want to clone, simply type `git clone` followed by the url.

**Step 5:** Enter the directory for the model you just downloaded. Open `token-identifier.txt` and copy the contents, ignoring the < > (you need to enter them when you put the token into your prompt, but the file name is irrelevant to that).

**Step 6:** Right click on `learned_embeds.bin`, click `rename`, paste what you copied out of `token-identifier.txt`, and click `enter`.

**Step 7:** Move this newly renamed `.bin` file to the `embeddings` directory. Feel free to delete the directory you cloned for the model once you have moved the `.bin` file out of it.

**Step 8:** Launch Voldy's and make sure your newly added model works. Pay attention to the name of the `.bin`, that's going to be the keyword that prompts Stable Diffusion to use it. In my case, I added `<line-art>` to my prompt of a frog, and it gave me this. Do the same methodology for any model that you want to add.

![Line Art Frog](https://i.imgur.com/kU8Ae2Y.png)

## But I want to make my own...

**Step 1:** Once you've figured out what you want to integrate, pick 3-5 photos of your selection, and crop them down into square images.

**Step 2:** Upload your photos to a publicly accessible database. I used [Imgur for mine](https://imgur.com/), which allows for hidden photos with a publicly accessible link, if relative privacy is of a concern to you. You need to provide square images, preferably sized to 512x512.

**Step 3:** Go to the [textual inversion colab](https://colab.research.google.com/github/huggingface/notebooks/blob/main/diffusers/sd_textual_inversion_training.ipynb#scrollTo=Yl3r7A_3ASxm) and follow the step by step instructions to run the model training, clicking the play button to the left at each new portion. For your image files, make sure whatever you're inputting is the direct link ending in `.jpg`, `.png`, or something of that like. If you don't believe you have a direct link, right click on the image and click `copy image address`. When you follow the link to generate your token code (you should already have a Hugging Face account if you downloaded the model files for Voldy's), generate a write code.

**Step 4:** Once the training has fully run, click the folder on the left side of the screen. Click `sd-concept-output`, click the three dots to the right of `learned_embeds.bin`, click download. Once the file has downloaded, rename it to whatever you provided as your placeholder token.

**Step 5:** Move this newly renamed `.bin` file to the `embeddings` directory.

**Step 6:** Launch Voldy's and make sure your newly added model works.

!!! note Database of Models
	I'm going to include links to any models that I generate going forward. If you have any you'd like you contribute, send them my way.
