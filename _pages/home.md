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

#### [Spencer Bialek](mailto:sbialek@uvic.ca)<sup>1,2</sup>, Emmanuel Bertin<a href="https://orcid.org/0000-0002-3602-3664"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/></sup></a> <sup>2,3</sup>, Sébastien Fabbro<a href="https://orcid.org/0000-0003-2239-7988"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/> </sup></a><sup>1,4</sup>, Hervé Bouy<a href="https://orcid.org/0000-0002-7084-487X"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/></sup></a> <sup>5,6</sup>, Jean-Pierre Rivet<a href="https://orcid.org/0000-0002-0289-5851"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/></sup></a> <sup>7</sup>, Olivier Lai<a href="https://orcid.org/0000-0001-5656-7346"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/></sup></a> <sup>7</sup>, Jean-Charles Cuillandre<a href="https://orcid.org/0000-0002-3263-8645"><sup> <img src="https://orcid.org/assets/vectors/orcid.logo.icon.svg" class="orcid" alt="ORCID iD icon"/></sup></a> <sup>3</sup>

<p style="font-size: 0.8em; margin-top: 2em;">
<sup>1</sup>Department of Physics and Astronomy, University of Victoria, Victoria, BC, V8W 3P2, Canada<br/>
<sup>2</sup>Canada–France–Hawaii Telescope, Kamuela, HI 96743, USA<br/>
<sup>3</sup>AIM, CEA, CNRS, Université Paris-Saclay, Université Paris Cité, F-91191 Gif-sur-Yvette, France<br/>
<sup>4</sup>National Research Council Herzberg Astronomy and Astrophysics, Victoria, BC, Canada<br/>
<sup>5</sup>Laboratoire d’Astrophysique de Bordeaux, CNRS and Université de Bordeaux, Allée Geoffroy St. Hilaire, 33165 Pessac, France<br/>
<sup>6</sup>Institut Universitaire de France<br/>
<sup>7</sup>Université Côte d’Azur, Observatoire de la Côte d’Azur, CNRS, Laboratoire J.–L. Lagrange, F-06304 Nice Cedex 4, France<br/>
</p>

<video autoplay="true" loop width="100%">
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
Short-exposure astronomical images reveal the starlight to be composed of speckles with randomly varying shapes and positions around a central point.
As a result, long exposures taken from ground instruments lead to the degradation of images and the overall effect can be framed as a blurring operation.
With small telescopes (aperture ≈ 3 − 4 times the [Fried parameter](https://en.wikipedia.org/wiki/Fried_parameter)), the tilt component of the wavefront distortions outweighs the sum of all other contributions, and point sources feature a dominant speckle which can be used to track and compensate for random image motions on the focal plane.

<!-- Include an M92 video from the assets folder -->
<video autoplay="true" loop width="100%">
  <source src="{{ site.baseurl }}/assets/video/tycho.mp4" type="video/mp4">
</video>

<img src="{{ site.baseurl }}/assets/img/tycho_average.gif" width="100%" style="max-width:none !important;"/>

### The method




