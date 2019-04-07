---
title: "Calibrating Spectra with OzDES_calibSpec"
excerpt: "OzDES_calibSpec is the publically available code I have developed to perform spectrophotometric calibration of the OzDES data. <br/><img src='/images/calibBAsmall.png '>"
collection: blog
---

OzDES_calibSpec is a publically available code which can be found at https://github.com/jhoormann/OzDES_calibSpec. This methodlogy was first presented in the paper [CIV Black Hole Mass Measurements with the Australian Dark Energy Survey (OZDES)](https://arxiv.org/abs/1902.04206) by Hoormann et al 2019.

<img src=”/images/4panelcalib.png”>
<figcaption>
Figure 1 from Hoormann et al 2019.  The top panel shows an example of an uncalibrated spectrum.  The second shows the DES transmission functions used to compute the magnitudes in each band from the OzDES spectrum.  The third panel shows the scale factors in each band needed to bring the OzDES magnitude into alignment with the DES magnitude.  The black line is the best fit to the scale factors which acts as the scaling function.  The bottom panel is the calibrated spectrum, found by multiplying the uncalibrated spectrum (top panel) by the scaling function (third panel).
</figcaption>

<img src=”/images/calibBA.png”>
<figcaption>
The left panel shows the uncalibrated spectrum for every observation of the F-star, FSC0225m0444.  The right panel shows the calibrate spectra for the same source.  As is seen in these figures the calibration procedures compensate for the observationally induced differences in the spectra.
</figcaption>

<img src=”/images/fstarcalib.png”>
<figcaption>
The top panel shows the calibrated spectra for FSC0225m0444, the same as in the right panel of the above figure.  The second panel shows the root mean spectrum of the data in the top panel, which shows the variation between each observation.  The bottom panel shows the percent variation.  On the whole the variation is less than 5% with larger variations at low wavelengths due to noise in the detectors and a bump at 5700 Angstroms which is where the two arms of the spectrograph are spliced together to create the spectrum.  
</figcaption>

