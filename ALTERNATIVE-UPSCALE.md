# A Moron's Guide to Alternative Upscaling

Voldy's has made significant improvements to memory utilization that, when tied with the `--medvram` and `--opt-split-attention` launch parameters allow outputs at much larger resolutions than were previously possible. Having achieved subpar results using a combination of ESRGAN upscalers and SD upscale, I decided to run a test, the results of which I believe achieve a much higher quality image, specifically in regard to photorealism. I've laid out the results of that test below, as well as information on how this method can be use.

This method requires a moderate amount of VRAM. With 10GB, I was able to take a 512x768 image up to 1024x1536. You may have better or worse luck depending on your card and the amount of VRAM that you have available. Experiment with it. Don't just give up if your first chosen size results in a VRAM error.

## The Method

This method will yield consistently cohesive, high quality, results. As with any upscale through Voldy's, this will alter details of the original output. This can be more or less pronounced depending on your denoising strength (higher will change more, lower will change less). As a result, as I'll showcase below, the seed can be just as important here as it would be in the initial output.

**Step 1:** Take an image output that you like and send it to the `img2img` tab. Alternatively, if it's an image you previously output, load it into the `PNG Info` tab (you'll need some of the parameters for the upscale).

**Step 2:** Load the same prompt, prompt negatives, and sampling method as your original output into the `img2img` tab, along with the image. The following are my preferences based on the testing I conducted, which is featured below. Yours may vary depending on how you interpret that same data set, and the amount of changes you're interested in seeing.

- Set the CFG scale to 15
- Set the Denoising strength to 0.3
- Set the sampling steps to 250

**Step 3:** Set the height and width to some upsized derivative of your original output ([this chart should help you](https://i.imgur.com/IsUgWk3.png), but if you can't match it exactly, get close and swap from `Just resize` to `Crop and resize`). In my case, after some trial and error of hitting VRAM limits on higher aspect ratios, I sized my output to 1024x1536, up from the original size of 512x768. I'd also recommend using facial restoration if that's applicable to your subject image.

**Step 4:** Press `Generate` and wait patiently for your results. For the purposes of objective testing, I ran all of the test images using the same seed as the original output. I also generated several images on random seeds using the above parameters, some of which can be seen in the chart below as a reference to the degree of variation that you may encounter. Keep that in mind as you're outputting and don't be afraid to run multiple versions until you're truly satisfied with the results.

## Inconsistency between the original output and the upscale

As a result of the way Stable Diffusion handles seeds, the same seed on a `text2img` output at 512x512 will be entirely different from its output at 512x768. The same holds true for `img2img`. Because of the change to a larger width/height, there is currently no way to ensure a flawless duplication with this method. Your best bet is to run batches at lower steps and find the one that most closely fits your desired output, then rerun it at high steps. This appear to be the unavoidable tradeoff for the visibly increased fine detail this method provides.

IMAGES TO BE READDED SOON

Original Seed | Random Seed 1 | Random Seed 2 | Random Seed 3
:----: | :----: | :----: | :----:
![Original seed]() | ![Random seed 1]() | ![Random seed 2]() | ![Random seed 3]()

## Test Results

I found that the sampler doesn't make much (if any) difference to the output image, which is why the instructions say to use the same sampler as the original output, and why I didn't include that variant in the testing below.

Aside from the X/Y plot variations, these upscales were all set to run on identical seeds at 100 steps, CFG 15, and a denoising strength of 0.5. I've included the results here as a reference, as well as comparisons between various upscaling methods. I wouldn't recommend going lower than 50 steps. While I didn't include examples here, runs performed at both 20 and 30 steps resulted in significant losses in quality.

- Full size versions of the seed comparison images above can be viewed [in this gallery]().
- Full size versions of the upscaling comparison images below can be viewed [in this gallery]().
- Full size versions of the CFG/Denoising comparison images below can be viewed [in this gallery]().
- Full size versions of the CFG/Steps compassion images below can be viewed [in this gallery]().
- Full size versions of the Steps/Denoising compassion images below can be viewed [in this gallery]().

The parameters I selected for the X/Y plots were the result of some limited testing I conducted beforehand. Feel free to try some other variations once you get up and running, though I will note that a denoising strength of 0.7 resulted in my example image having a head grow out of her stomach. If I conduct further testing, I will add those results here and update this guide accordingly.

Original | This method | SD upscaling | Gigapixel AI
:----: | :----: | :----: | :----:
![Original]() | ![CFG 15 @ 0.6]() | ![Lollypop and SD Upscaling]() | ![Gigapixel AI]()

![CFG/Denoising]()

![CFG/Steps]()

![CFG/Steps]()
