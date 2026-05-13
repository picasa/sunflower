# An ecophysiological model for the sunflower crop.

`sunflower` is a sunflower crop simulator that predicts plant and crop variables as a function of time and environmental data. The default simulation function implements equations from the SUNFLO model ([Casadebaig2011](https://doi.org/10.1016/j.agrformet.2010.09.012)).
A set of helper functions provides a way to set default simulation conditions, change management or cultivar-related parameters, and summarise time series outputs as standard crop features (stage duration, resource use, and productivity). The [{sunflower}](https://forge.inrae.fr/sunflo/sunflower) R package source code is versionned on the INRAE gitlab instance. 

## Installation

To install this package, start R (>= 4.1) and run:

```
# install.packages("remotes") 
remotes::install_git("https://forge.inrae.fr/sunflo/sunflower.git")
```

## Documentation

The simulation process is described on the [get started]([articles/sunflower.html](https://sunflo.pages-forge.inrae.fr/sunflower/articles/sunflower.html)) page. The model conceptual basis and parameterization are available on the [documentation]([articles/_0_sunflo_documentation.html](https://sunflo.pages-forge.inrae.fr/sunflower/articles/_0_sunflo_documentation.html)) page

## Model overview

SUNFLO is a process-based model for the sunflower crop that was developed to simulate grain yield and oil concentration as a function of time ($t$), environment ($E$, which includes soil, climate, and management practices), and genetic diversity ($G$) ([Casadebaig2011](https://doi.org/10.1016/j.agrformet.2010.09.012), [Lecoeur2011](https://doi.org/10.1071/FP09189))

## Model architecture

This model is based on a conceptual framework initially proposed by Monteith ([1977](https://doi.org/10.2307/2402584)) and now shared by a large family of crop models ([Jones2016](https://doi.org/10.1016/j.agsy.2016.05.014)).
In this framework, the daily crop dry biomass ($DM_t$) is calculated as a difference equation ^[$DM_t = DM_{t-1} + PAR \times RIE \times RUE$] as a function of incident photosynthetically active radiation ($PAR$, $MJ.m^{-2}$), light interception efficiency ($RIE$), and radiation use efficiency ($RUE$, $g.MJ^{-1}$).
The light interception efficiency is based on Beer-Lambert's law^[$RIE = 1-exp^{-k~LAI}$] as a function of leaf area index ($LAI$) and light extinction coefficient ($k$). The radiation use efficiency concept ([Monteith1994](https://doi.org/10.1016/0168-1923(94)90037-X)) is used to represent photosynthesis at the crop scale.

Broad-scale processes of this framework—the dynamics of $LAI=f(t, G, E)$, photosynthesis ($RUE=f(t, G, E)$), and biomass allocation to grains were split into finer processes (e.g., leaf expansion and senescence, response functions to environmental stresses) to reveal genotypic specificity and to allow the emergence of genotype-by-environment interactions. Globally, the SUNFLO crop model has about 50 equations and 24 parameters (14 plant-related traits and 10 environment-related).
