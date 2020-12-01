# XClumpy
## Introduction
XClumpy [(Tanimoto et al. 2019)](https://ui.adsabs.harvard.edu/abs/2019ApJ...877...95T/abstract) is an X-ray spectral model from the clumpy torus in an Active Galactic Nucleus, utilizing the Monte Carlo simulation for Astrophysics and Cosmology framework (MONACO: [Odaka et al. 2011](https://ui.adsabs.harvard.edu/abs/2011ApJ...740..103O/abstract)).


## Torus Geometry
The adopted geometry of the torus is the same as that in [Nenkova et al. (2008)](https://ui.adsabs.harvard.edu/abs/2008ApJ...685..160N/abstract), who assume a power-law distribution of clumps in the radial direction and a normal distribution in the elevation direction. This enables us to directly compare the results obtained from the infrared and X-ray bands. If you would like to need more information, please see [Tanimoto et al. (2019)](https://ui.adsabs.harvard.edu/abs/2019ApJ...877...95T/abstract).

<p align="center">
<img src="https://user-images.githubusercontent.com/20199124/100601931-96766180-3346-11eb-9f25-2f96b4a8671c.jpg">
</p>


## Usage
We prepared an xcm file of the XClumpy model (xclumpy.xcm). Our spectral model is represented in XSPEC the following:  
`const1*phabs*(zphabs*cabs*zcutoffpl+const2*zcutoffpl+atable{xclumpy_v01_RC.fits}+atable{xclumpy_v01_RL.fits})`  

This model consists of five components:  
1. `const1*phabs`  
  The const1 term is a cross-normalization constant to adjust small differences in the absolute flux calibration among different instruments. The phabs term represents the Galactic absorption.  

2. `zphabs*cabs*zcutoffpl`  
  This component represents the transmitted continuum through the torus. The zphabs and cabs terms represent the photoelectric absorption and Compton scattering by the torus, respectively. The hydrogen column density along the line of sight is determined according to Equation (1). The zcutoffpl term is the instrinsic continuum modeled by a power-law with an exponential cutoff. We fix this at a typical value (E<sub>cut</sub> = 370 keV).  

3. `const2*zcutoffpl`  
  This component represents the scattered component. The const term is the scattering fraction. We link the photon index, the cutoff energy, and the normalization to those of the intrinsic continuum.

4. `atable{xclumpy_v01_RC.fits}`  
  This component represents the reflection continuum from the clumpy torus based on the XClumpy model. This XClumpy model has six parameters: (1) hydrogen column density along the equatorial plane, (2) torus angular width, (3) inclination angle, (4) photon index, (5) cutoff energy, and (6) normalization (See Parameters). We link the photon index, the cutoff energy, and the normalization to those of the intrinsic continuum. We determine the line-of-sight hydrogen column density the following equation:

<p align="center">
<img src="https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cbegin%7Bequation%7D%0AN_%7B%5Cmathrm%7BH%7D%7D%5E%7B%5Cmathrm%7BLOS%7D%7D+%3D+N_%7B%5Cmathrm%7BH%7D%7D%5E%7B%5Cmathrm%7BEqu%7D%7D+%5Cexp%5Cleft%28%7B-%5Cfrac%7B%28i-%5Cpi%2F2%29%5E2%7D%7B%5Csigma%5E2%7D%7D%5Cright%29%0A%5Cend%7Bequation%7D%0A" alt="\begin{equation} N_{\mathrm{H}}^{\mathrm{LOS}} = N_{\mathrm{H}}^{\mathrm{Equ}} \exp\left({-\frac{(i-\pi/2)^2}{\sigma^2}}\right)\end{equation}">
</p>

5. `atable{xclumpy_v01_RL.fits}`  
  This component represents fluorescence lines from the clumpy torus based on the XClumpy model. We link the photon index, the cutoff energy, and the normalization to those of the reflection continuum.


## Parameters
The XClumpy model has six parameters.

| Parameter | Explanation                                        | Range                           | Units           | 
| :-------: | :------------------------------------------------: | :-----------------------------: | :-------------: | 
| nh        | hydrogen column density along the equatorial plane | 10<sup>23</sup>-10<sup>25</sup> | cm<sup>-2</sup> | 
| sigma     | torus angular width                                | 10-90                           | degree          | 
| incl      | inclination angle                                  | 20-87                           | degree          | 
| gamma     | photon index                                       | 1.5-2.5                         | ...             | 
| cutoff    | cutoff energy                                      | 370                             | keV             | 
| norm      | normalization                                      | ...                             | ...             | 


## Example
We show the dependence of the reflection continuum on the hydrogen column density along the equatorial plane as an example. Red line: log N<sub>H</sub>/cm<sup>-2</sup> = 23.5. Orange line: log N<sub>H</sub>/cm<sup>-2</sup> = 24.0. Blue line: log N<sub>H</sub>/cm<sup>-2</sup> = 24.5. Here we adopt sigma = 30 degree, i = 60 degree, gamma = 2.0, cutoff = 370 keV, and norm = 1.

<p align="center">
<img src="https://user-images.githubusercontent.com/20199124/100716198-b451ce00-33fb-11eb-9e6a-72e370c3ae0c.jpg">
</p>


## Acknowledgement
Numerical computations were carried out on Cray XC50 at Center for Computational Astrophysics, National Astronomical Observatory of Japan.
