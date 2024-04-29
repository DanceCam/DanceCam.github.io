---
layout: home
permalink: /

profile:
   align: left
   image: dancecam_logo.png
   more_info: 

news: false # includes a list of news items
selected_papers: false # includes a list of papers marked as "selected={true}"
social: false # includes social icons at the bottom of the page
---

<h1 style="text-align: center;">Atmospheric turbulence mitigation in wide-field astronomical images with short-exposure video streams</h1>

#### [Spencer Bialek](mailto:sbialek@uvic.ca)<a href="https://orcid.org/0009-0007-4388-2508"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/></sup></a> <sup>1,2</sup>, Emmanuel Bertin<a href="https://orcid.org/0000-0002-3602-3664"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/></sup></a> <sup>2,3</sup>, Sébastien Fabbro<a href="https://orcid.org/0000-0003-2239-7988"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/> </sup></a><sup>1,4</sup>, Hervé Bouy<a href="https://orcid.org/0000-0002-7084-487X"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/></sup></a> <sup>5,6</sup>, Jean-Pierre Rivet<a href="https://orcid.org/0000-0002-0289-5851"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/></sup></a> <sup>7</sup>, Olivier Lai<a href="https://orcid.org/0000-0001-5656-7346"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/></sup></a> <sup>7</sup>, Jean-Charles Cuillandre<a href="https://orcid.org/0000-0002-3263-8645"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/></sup></a> <sup>3</sup>

<p style="font-size: 0.8em; margin-top: 2em;">
<sup>1</sup>Department of Physics and Astronomy, University of Victoria, Victoria, BC, V8W 3P2, Canada<br/>
<sup>2</sup>Canada–France–Hawaii Telescope, Kamuela, HI 96743, USA<br/>
<sup>3</sup>AIM, CEA, CNRS, Université Paris-Saclay, Université Paris Cité, F-91191 Gif-sur-Yvette, France<br/>
<sup>4</sup>National Research Council Herzberg Astronomy and Astrophysics, Victoria, BC, Canada<br/>
<sup>5</sup>Laboratoire d’Astrophysique de Bordeaux, CNRS and Université de Bordeaux, Allée Geoffroy St. Hilaire, 33165 Pessac, France<br/>
<sup>6</sup>Institut Universitaire de France<br/>
<sup>7</sup>Université Côte d’Azur, Observatoire de la Côte d’Azur, CNRS, Laboratoire J.–L. Lagrange, F-06304 Nice Cedex 4, France<br/>
</p>

<video autoplay controls loop width="100%">
  <source src="{{ site.baseurl }}/assets/video/test_M92.mp4" type="video/mp4">
</video>


<div style="margin-left: auto; margin-right:auto; margin-top: 2em; max-width: 800px">
<h3 style="text-align: center;">Abstract</h3>
<p style="font-style: italic; text-align: justify;">We introduce a novel technique to mitigate the adverse effects of atmospheric turbulence on
astronomical imaging. Utilizing a video-to-image neural network trained on simulated data,
our method processes a sliding sequence of short-exposure (∼0.2s) stellar field images to
reconstruct an image devoid of both turbulence and noise. We demonstrate the method with
simulated and observed stellar fields, and show that the brief exposure sequence allows the
network to accurately associate speckles to their originating stars and effectively disentangle
light from adjacent sources across a range of seeing conditions, all while preserving flux
to a lower signal-to-noise ratio than an average stack. This approach results in a marked
improvement in angular resolution without compromising the astrometric stability of the final
image.</p>
</div>

### The problem

Atmospheric turbulence causes the wavefront of incoming light to be dynamically distorted.
As a result, long exposures taken from ground instruments lead to the degradation of images and the overall effect can be framed as a blurring operation.
With small telescopes (aperture ≈ 3 − 4 times the [Fried parameter](https://en.wikipedia.org/wiki/Fried_parameter)), the tilt component of the wavefront distortions outweighs the sum of all other contributions, and the effect of turbulence is prominently random image motions on the focal plane.

<video autoplay controls loop width="100%" style="margin-bottom: 0rem;margin-top: 2rem;">
  <source src="{{ site.baseurl }}/assets/video/tycho.mp4" type="video/mp4">
</video>
<div class="caption">
    Example of a video sequence at 20 frames per second, showing the dynamical effects of atmospheric turbulence on astronomical observations carried out from the ground on a small telescope (14"). The Moon crater close the center is Tycho. The pixel scale is 0.29".
</div>
<img src="{{ site.baseurl }}/assets/img/tycho_average.gif" width="100%" style="margin-bottom: -0.7rem; max-width:none !important;"/>
<div class="caption">
    3 second average of the video above, showing the blurring effect of long exposures.
</div>

As the video above shows, fast imaging provides much sharper images than long exposures, but the high-resolution information is scrambled by turbulence.
To compensate the effects of atmospheric turbulence over wide fields, one could imagine correcting those apparent motions by adjusting a “rubber” focal plane model ([Kaiser et al. 2000](https://ui.adsabs.harvard.edu/abs/2000PASP..112..768K/abstract)), which consists of a distorted virtual pixel grid.

For deep sky observations, which are our primary goal, the deformations of this virtual grid would have to be continuously controlled by a number of guide stars over its surface.
However this process is complex to set up in practice, e.g., changing conditions require dynamic adaptation of the statistical model, and the number of individual stars suitable for guiding is often insufficient.
Instead, we propose to leverage the power of Deep Learning to directly reconstruct virtual exposures from video sequences.

### The method

The cornerstone of our proposed method is the application of the Residual U-Net, a variant of the traditional U-Net architecture
known for its proficiency in semantic segmentation and image reconstruction tasks.
A set of simulated short-exposure video streams of stellar fields – with turbulence and noise – along with their corresponding ground truth frames – with no turbulence or noise – is used to train the model.
Instead of a single output, the model additionally has outputs from each stage in the decoder which are compared to downsampled versions of the ground truth using a weighted mean-squared error (MSE) loss function.
Once trained, either a simulated or real video stream can be used as input and only a single (not downsampled) inferred image is retrieved.

<img class="repo-img-light" src="{{ site.baseurl }}/assets/img/dancecam_unet.png" width="100%" style="margin-bottom: -0.7rem; ;margin-top: 2rem; max-width:none !important;"/>
<img class="repo-img-dark" src="{{ site.baseurl }}/assets/img/dancecam_unet-dark.png" width="100%" style="margin-bottom: -0.7rem; ;margin-top: 2rem; max-width:none !important;"/>
<div class="caption">
    The DanceCam Residual U-Net architecture.
</div>


