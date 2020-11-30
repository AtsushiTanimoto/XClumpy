<script async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS_CHTML"></script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
  tex2jax: {
  inlineMath: [["\\(","\\)"] ],
  displayMath: [ ['$$','$$'], ["\\[","\\]"] ]
  }
  });
</script>


# XClumpy
XClumpy [(Tanimoto et al. 2019)](https://ui.adsabs.harvard.edu/abs/2019ApJ...877...95T/abstract) is an X-ray spectral model from the clumpy torus in an Active Galactic Nucleus, utilizing the Monte Carlo simulation for Astrophysics and Cosmology framework [(Odaka et al. 2011)](https://ui.adsabs.harvard.edu/abs/2011ApJ...740..103O/abstract).


## Torus Geometry
The adopted geometry of the torus is the same as that in [Nenkova et al. (2008)](https://ui.adsabs.harvard.edu/abs/2008ApJ...685..160N/abstract), who assume a power-law distribution of clumps in the radial direction and a normal distribution in the elevation direction. This enables us to directly compare the results obtained from the infrared and X-ray bands.


## Parameters
The XClumpy model has eight independent parameters that define the torus properties:\\
1. Rinner: Inner radius of the torus
2. Outer radius of the torus
3. Radius of the clump
4. 
