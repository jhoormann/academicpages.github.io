---
title: "Calibrating Spectra with OzDES_calibSpec"
excerpt: "OzDES_calibSpec is the publically available code I have developed to perform spectrophotometric calibration of the OzDES data. <br/><img src='/images/calibBAsmall.png '>"
collection: blog
---

OzDES_calibSpec is a publically available code which can be found at https://github.com/jhoormann/OzDES_calibSpec. This methodlogy was first presented in the paper [CIV Black Hole Mass Measurements with the Australian Dark Energy Survey (OZDES)](https://arxiv.org/abs/1902.04206) by Hoormann et al 2019.

Reverberation mapping (RM) works by measuring variations in the size of emission lines in order to measure the response from the clouds (go to [this blog]( https://jhoormann.github.io/blog/blog-1/) to learn more about how RM works).  In the video below you can see how this works.  This video show the C IV emission line as observed by OzDES for the active galaxy DES J0033-42 as it changes over time.  You can see that emission line changes in size which translates to a change in flux in the light curve shown in the panel on the top 
right.  

<br/><img src='/images/LCVariation.gif'>
The change in line strength corresponds to flares which occur right around the black hole.  However, there are other factors which could cause variations to appear which have nothing to do with underlying physics of black holes.  
<br/>
A number of things could happen to effect the shape of the spectrum we observe.  Something as simple as a wispy cloud floating above the telescope while we are observing could block some of the light and make the source appear dimmer.    Also, because of the orbit of the earth, even though we are looking at the same patch of the universe over and over again, the fields we target will appear in different parts of the sky based on the time of year we observe them.  If we observe something just above the horizon the light will have to travel through more atmosphere than if we observe it when it directly overhead.  This can also cause changes in what we observe.  Another effect is due to the experimental set-up.  OzDES uses a system called 2dF which allows you to place optical fibers exactly where you expect the source you want to observe to be.  Ideally the optical fiber is positioned at the center of the galaxy in order to collect all the light that it emits.  This is shown in the left panel of the image below.  However, it is possible for the fiber to be offset (right) meaning that we will be unable to collect light from parts of the galaxy.

<img src='/images/misplacedfiber.png'>
<figcaption>
A cartoon example of what is meant by the optical fiber being offset.
</figcaption>

One of the primary projects I have led is to determine how best to account for all of these variations so that we can perform high quality calibration of our spectra.  The way I do this is using a procedure called spectrophotometric calibration.  This means that we use high quality calibrated photometry (in our case using the near simultaneous DES observations) to calibrate our spectra.  How this works is illustrated in the figure below.   In the top panel is an example of an uncalibrated spectrum that we have observed with OzDES.   In order to compare a spectrum to photometry you need to convert your spectrum into magnitudes.  Because we will be comparing our calculated OzDES magnitudes to the data observed by DES we use their transmission functions (second panel).  The transmission functions tell us, for each band DES observes (we care about the g, r, i bands because that is what overlaps with our OzDES spectrum) what percentage of the light at a given wavelength will be observed by DES.   I can then compare the calculated OzDES magnitudes with the magnitudes observed at the same time by DES and calculate the scale factor needed to bring the two values into agreement.  The third panel shows these scale factors.  The error bars on these values are so small in large part due to the fact that the DES photometry we are using is so precise (sub percent accuracy).  As you can see the scale factors are not constant.  Therefore, I fit a 2D polynomial to the scale factors to create a scaling function which I multiply by the original spectrum to calibrate it.  The uncertainty in this scaling function is estimated using Gaussian processes and is then added in quadrature with the uncertainties due to the observations themselves.  

<img src='/images/4panelcalib.png'>
<figcaption>
Figure 1 from Hoormann et al 2019.  The top panel shows an example of an uncalibrated spectrum (arbitrary units).  The second shows the DES transmission functions used to compute the magnitudes in each band from the OzDES spectrum.  The third panel shows the scale factors (10 <sup>-16</sup> ergs/s/cm<sup>2</sup>/Angstrom/count) in each band needed to bring the OzDES magnitude into alignment with the DES magnitude.  The black line is the best fit to the scale factors which acts as the scaling function.  The bottom panel is the calibrated spectrum (10 <sup>-16</sup> ergs/s/cm<sup>2</sup>/Angstrom), found by multiplying the uncalibrated spectrum (top panel) by the scaling function (third panel). For those unfamiliar, 10 Angstroms = 1 nanometer.
</figcaption>

The fact that the scale factors are not constant for each band is likely due to a combination of all of the effects that were mentioned above.  Even between observations of the same source the scaling function can change significantly.  That is why having near simultaneous photometric observations are so important, at least if you are calibrating a variable source such as the active galaxies observed for the RM program. 

In order to test how well this calibration procedure works I made use of the fact that every time OzDES observes it targets what are called F-stars.  These F-stars are non-varying stars with a well understood spectral shape which makes them ideal targets for calibration purposes.  In the figure below are all of the observations through OzDES Year 4 for the F-star FSC0225m0444.  In the left panel you can see the original, uncalibrated spectra.  Despite the fact that this star should have a constant spectral shape you can see that data does vary, particularly at lower wavelengths.  However, after calibration (right panel) you can see that all the observations do indeed yield similar spectra.

<img src='/images/calibBA.png'>
<figcaption>
The left panel shows the uncalibrated spectrum (arbitrary units) for every observation of the F-star, FSC0225m0444.  The right panel shows the calibrate spectra (10 <sup>-16</sup> ergs/s/cm<sup>2</sup>/Angstrom) for the same source.  As is seen in these figures the calibration procedures compensate for the observationally induced differences in the spectra.
</figcaption>

In order to quantify how well this procedures works I took the calibrated F-star spectrum and calculated the root mean squared (RMS) spectrum.  The calibrate F-star spectrum is shown again in the top panel of the next figure and the RMS spectrum is shown in the middle panel.  The RMS spectrum isolates the variation in the input data.  I can then calculate the fractional variation for this source.  This is shown as the percent variation in the bottom panel of the plot below.  

<img src='/images/fstarcalib.png'>
<figcaption>
The top panel shows the calibrated spectra for FSC0225m0444, the same as in the right panel of the above figure (units of  10<sup>-16</sup> ergs/s/cm<sup>2</sup>/Angstrom).  The second panel shows the root mean spectrum of the data in the top panel, which shows the variation between each observation.  The bottom panel shows the percent variation.  On the whole the variation is less than 5% with larger variations at low wavelengths due to noise in the detectors and a bump at 5700 Angstroms which is where the two arms of the spectrograph are spliced together to create the spectrum.  
</figcaption>

The percent variation is generally less than 5%.  The variation is larger at lower wavelengths where the observations themselves are nosier.  There is also an increase in variation around 5700 Angstroms.  This is because the spectrograph OzDES uses (AAOmega) breaks up the data into two arms, the red (high wavelength) and blue (low wavelength) arms.  The break between the arms occurs at 5700 Angstroms.  In order to get a single spectrum the data from the two arms are spliced together.  While the procedures to do this have gotten better and better over the years there is still some added uncertainty where the splicing happens.  The fact that on the whole the uncertainty is less than 5% though is fantastic! This puts us at the threshold of the noise levels of the detectors themselves!

While this code, OzDES_calibSpec, was designed with the OzDES Reverberation Program in mind it can be applied to any spectrum with corresponding photometry data.
