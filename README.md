# XClumpy
## Introduction
XClumpy [(Tanimoto et al. 2019)](https://ui.adsabs.harvard.edu/abs/2019ApJ...877...95T/abstract) is an X-ray spectral model from the clumpy torus in an Active Galactic Nucleus, utilizing the Monte Carlo simulation for Astrophysics and Cosmology framework [(Odaka et al. 2011)](https://ui.adsabs.harvard.edu/abs/2011ApJ...740..103O/abstract).


## Torus Geometry
The adopted geometry of the torus is the same as that in [Nenkova et al. (2008)](https://ui.adsabs.harvard.edu/abs/2008ApJ...685..160N/abstract), who assume a power-law distribution of clumps in the radial direction and a normal distribution in the elevation direction. This enables us to directly compare the results obtained from the infrared and X-ray bands. If you would like to need more information, please see [(Tanimoto et al. 2019)](https://ui.adsabs.harvard.edu/abs/2019ApJ...877...95T/abstract).


## Usage
We prepared an xcm file of the XClumpy model. Our model is represented in XSPEC the following:  
  const1\*phabs\*(const2\*zphabs\*cabs\*zcutoffpl+const3\*zcutoffpl+atable{xclumpy_v01_RC.fits}+atable{xclumpy_v01_RL.fits})  

This model consists of six components:  
1. const1\*phabs.  
  The const1 term is a cross-normalization constant to adjust small differences in the absolute flux calibration among different instruments. The phabs term represents the Galactic absorption.  

2. const2\*zphabs\*cabs\*zcutoffpl.  
  This component represents the transmitted continuum through the torus. The const2 term is a constant to consider time variability. We limit the const2 value within a range of 0.10-10.0 to avoid unrealistic results. The zphabs and cabs terms represent the photoelectric absorption and Compton scattering by the torus, respectively. The hydrogen column density along the line of sight is determined according to Equation (1). The zcutoffpl is the instrinsic continuum modeled by a power-law with an exponential cutoff. We fix this at a typical value (E<sub>cut</sub> = 370 keV).  

3. const3\*zcutoffpl.  
  


## Parameters
This XClumpy model has seven free parameters:  

1. nH  
  Hydrogen column density along the equatorial plane (10<sup>23</sup>-10<sup>25</sup> cm<sup>-2</sup>).
2. sigma
3. incl
4. gamma
5. cutoff
6. z
7. norm
