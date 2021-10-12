# XClumpy
## Introduction
XClumpy [(Tanimoto et al. 2019)](https://ui.adsabs.harvard.edu/abs/2019ApJ...877...95T/abstract) is an X-ray spectral model from the clumpy torus in an Active Galactic Nucleus, utilizing the Monte Carlo simulation for Astrophysics and Cosmology framework (MONACO: [Odaka et al. 2011](https://ui.adsabs.harvard.edu/abs/2011ApJ...740..103O/abstract)).


## Torus Geometry
The adopted geometry of the torus is the same as that in [Nenkova et al. (2008)](https://ui.adsabs.harvard.edu/abs/2008ApJ...685..160N/abstract), who assume a power-law distribution of clumps in the radial direction and a normal distribution in the elevation direction. This enables us to directly compare the results obtained from the infrared and X-ray bands. See [Tanimoto et al. (2019)](https://ui.adsabs.harvard.edu/abs/2019ApJ...877...95T/abstract) for more details.

<p align="center">
<img src="https://user-images.githubusercontent.com/20199124/100601931-96766180-3346-11eb-9f25-2f96b4a8671c.jpg">
</p>


## Usage
We prepared an xcm file of the XClumpy model (xclumpy.xcm). Our spectral model is represented as follows in XSPEC terminology:  
`const*phabs*(zphabs*cabs*zcutoffpl+atable{xclumpy_v01_RC.fits}+atable{xclumpy_v01_RL.fits})`  

This model consists of four components:  
1. `const*phabs`  
   The const term is a cross-normalization constant to adjust small differences in the absolute flux calibration among different instruments. The phabs term represents the Galactic absorption.  

2. `cabs*zphabs*zcutoffpl`  
   This component represents the transmitted continuum through the torus. The zphabs and cabs terms represent the photoelectric absorption and Compton scattering by the torus, respectively. The hydrogen column density along the line of sight is determined according to Equation (1). The zcutoffpl term is the intrinsic continuum modeled by a power-law with an exponential cutoff. We fix this at a typical value (E<sub>cut</sub> = 370 keV: [Ricci et al. 2018](https://ui.adsabs.harvard.edu/abs/2018MNRAS.480.1819R/abstract)).  

3. `atable{xclumpy_v01_RC.fits}`  
   This component represents the reflection continuum from the clumpy torus based on the XClumpy model. This XClumpy model has six parameters: (1) hydrogen column density along the equatorial plane, (2) torus angular width, (3) inclination angle, (4) photon index, (5) cutoff energy, and (6) normalization (See Parameters). The photon index, cutoff energy, and normalization must be linked to those of the intrinsic continuum. We determine the line-of-sight hydrogen column density the following equation:

<p align="center">
<img src="https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cbegin%7Bequation%7D%0AN_%7B%5Cmathrm%7BH%7D%7D%5E%7B%5Cmathrm%7BLOS%7D%7D+%3D+N_%7B%5Cmathrm%7BH%7D%7D%5E%7B%5Cmathrm%7BEqu%7D%7D+%5Cexp%5Cleft%28%7B-%5Cfrac%7B%28i-%5Cpi%2F2%29%5E2%7D%7B%5Csigma%5E2%7D%7D%5Cright%29%0A%5Cend%7Bequation%7D%0A" alt="\begin{equation} N_{\mathrm{H}}^{\mathrm{LOS}} = N_{\mathrm{H}}^{\mathrm{Equ}} \exp\left({-\frac{(i-\pi/2)^2}{\sigma^2}}\right)\end{equation}">
</p>

4. `atable{xclumpy_v01_RL.fits}`  
   This component represents fluorescence lines from the clumpy torus based on the XClumpy model. The hydrogen column density along the equatorial plane, torus angular width, inclination angle, photon index, cutoff energy, and normalization must be linked to those of the reflection continuum.


## Parameters
The XClumpy model has six parameters.

| Parameter | Explanation                                        | Range                           | Units                                                             | 
| :-------: | :------------------------------------------------: | :-----------------------------: | :-------------:                                                   | 
| nh        | hydrogen column density along the equatorial plane | 10<sup>23</sup>-10<sup>25</sup> | cm<sup>-2</sup>                                                   | 
| sigma     | torus angular width                                | 10-90                           | degree                                                           | 
| incl      | inclination angle                                  | 20-87                           | degree                                                           | 
| gamma     | photon index                                       | 1.0-3.0                         | ...                                                               | 
| cutoff    | cutoff energy                                      | 370                             | keV                                                               | 
| norm      | normalization                                      | ...                             | photons s<sup>-1</sup> cm<sup>-2</sup> keV<sup>-1</sup> at 1 keV | 


## Example
We show the dependence of the reflection continuum on the hydrogen column density along the equatorial plane as an example. Red line is log N<sub>H</sub>/cm<sup>-2</sup> = 23.5, orange line is log N<sub>H</sub>/cm<sup>-2</sup> = 24.0, and blue line is log N<sub>H</sub>/cm<sup>-2</sup> = 24.5. Here we adopt sigma = 30 degree, i = 60 degree, gamma = 2.0, cutoff = 370 keV, and norm = 1.0.

<p align="center">
<img src="https://user-images.githubusercontent.com/20199124/100716198-b451ce00-33fb-11eb-9e6a-72e370c3ae0c.jpg">
</p>


## Publications
1. [XCLUMPY: X-Ray Spectral Model from Clumpy Torus and Its Application to the Circinus Galaxy](https://ui.adsabs.harvard.edu/abs/2019ApJ...877...95T/abstract)  
   Atsushi Tanimoto, Yoshihiro Ueda, Hirokazu Odaka, Toshihiro Kawaguchi, Yasushi Fukazawa, & Taiki Kawamuro  
   The Astrophysical Journal, Volume 877, Issue 2, article id. 95, 16 pp. (2019).

2. [Application of Clumpy Torus Model to Broadband X-Ray Spectra of Two Seyfert 1 Galaxies: IC 4329A and NGC 7469](https://ui.adsabs.harvard.edu/abs/2019ApJ...875..115O/abstract)  
   Shoji Ogawa, Yoshihiro Ueda, Satoshi Yamada, Atsushi Tanimoto, & Toshihiro Kawaguchi  
   The Astrophysical Journal, Volume 875, Issue 2, article id. 115, 10 pp. (2019).

3. [Torus Constraints in ANEPD-CXO245: A Compton-thick AGN with Double-peaked Narrow Lines](https://ui.adsabs.harvard.edu/abs/2019ApJ...884L..10M/abstract)  
   Takamitsu Miyaji et al.  
   The Astrophysical Journal Letters, Volume 884, Issue 1, article id. L10, 6 pp. (2019).

4. [NuSTAR Discovery of a Compton-thick, Dust-obscured Galaxy: WISE J0825+3002](https://ui.adsabs.harvard.edu/abs/2020ApJ...888....8T/abstract)  
   Yoshiki Toba et al.  
   The Astrophysical Journal, Volume 888, Issue 1, article id. 8, 8 pp. (2020).

5. [Application of an X-Ray Clumpy Torus Model (XCLUMPY) to 10 Obscured Active Galactic Nuclei Observed with Suzaku and NuSTAR](https://ui.adsabs.harvard.edu/abs/2020ApJ...897....2T/abstract)  
   Atsushi Tanimoto, Yoshihiro Ueda, Hirokazu Odaka, Shoji Ogawa, Satoshi Yamada, Toshihiro Kawaguchi, & Kohei Ichikawa  
   The Astrophysical Journal, Volume 897, Issue 1, id.2, 13 pp. (2020).

6. [Nature of Compton-thick Active Galactic Nuclei in "Nonmerging" Luminous Infrared Galaxies UGC 2608 and NGC 5135 Revealed with Broadband X-Ray Spectroscopy](https://ui.adsabs.harvard.edu/abs/2020ApJ...897..107Y/abstract)  
   Satoshi Yamada, Yoshihiro Ueda, Atsushi Tanimoto, Saeko Oda, Masatoshi Imanishi, Yoshiki Toba, & Ricci Claudio  
   The Astrophysical Journal, Volume 897, Issue 1, id.107, (2020).

7. [Systematic Study of AGN Clumpy Tori with Broadband X-Ray Spectroscopy: Updated Unified Picture of AGN Structure](https://ui.adsabs.harvard.edu/abs/2021ApJ...906...84O/abstract)  
   Shoji Ogawa, Yoshihiro Ueda, Atsushi Tanimoto, & Satoshi Yamada  
   The Astrophysical Journal, Volume 906, Issue 2, id.84, (2021).

8. [X-Ray Constraint on the Location of the AGN Torus in the Circinus Galaxy](https://ui.adsabs.harvard.edu/abs/2021ApJ...913...17U/abstract)  
   Ryosuke Uematsu, Yoshihiro Ueda, Atsushi Tanimoto, Taiki Kawamuro, Kenta Setoguchi, Shoji Ogawa, Satoshi Yamada, & Hirokazu Odaka  
   The Astrophysical Journal, Volume 913, Issue 1, id.17, (2021)


## Citation
If you have used the XClumpy model in a scientific publication, please cite [Tanimoto et al. (2019)](https://ui.adsabs.harvard.edu/abs/2019ApJ...877...95T/abstract).


## Acknowledgement
Numerical computations were carried out on Cray XC50 at Center for Computational Astrophysics, National Astronomical Observatory of Japan.
