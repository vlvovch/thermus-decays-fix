# THERMUS decays fix
[THERMUS](https://doi.org/10.1016/j.cpc.2008.08.001) package is a popular program for thermal model applications in heavy-ion collisions. In the publicly-available implementations of the various THERMUS versions, the decay contributions to final yields of particles which are marked as unstable are not calculated. This can have unfortunate implications if the yields of unstable particles [such as e.g. K<sup>*</sup>, &varphi;, or &Lambda;(1520)] are compared between THERMUS and experiment, since they may be notably underestimated in the THERMUS calculation. (There is no such issue in THERMUS with the yields of particles which are marked as stable.)

The described behavior is not well documented and seems to be rather unnatural.
This issue can in principle be avoided by using multiple particle sets in THERMUS.
Such a solution however looks to be rather tedious and prone to introducing mistakes.
This repository contains modified THERMUS source files, which add calculation of decay contributions to final yields of unstable particles.
When the final yields of unstable particles are accessed in the modified THERMUS, the output values contain both primordial yields and decay contributions from the higher-lying states.

### Usage

This repository contains fixes for three different THERMUS versions (links to codes are accessible as of Nov 6, 2018):

- [THERMUS-2.3](http://www.phy.uct.ac.za/sites/default/files/image_tool/images/281/people/wheaton/thermus/THERMUSV2-3.tar.gz), the fix is located in the folder `fix-thermus-2.3` of this repository
- [THERMUS-3.0](http://www.phy.uct.ac.za/sites/default/files/image_tool/images/281/people/wheaton/thermus/THERMUSV3-0.tar.gz), the fix is located in the folder `fix-thermus-3.0` of this repository
- The official [GitHub version of THERMUS](https://github.com/thermus-project/THERMUS),  the fix is located in the folder `fix-thermus-github` of this repository

To apply the fix just copy the contents of the relevant folder of this repository into the root THERMUS directory, replacing the files there. Then (re)build THERMUS.

### Illustration

The [prediction.C](https://github.com/thermus-project/THERMUS/blob/master/test/prediction.C) macro from the THERMUS-github repository calculates various particle yields and yield ratios at T = 156 MeV and &mu;<sub>B</sub> = 0.1 MeV.

The resulting yields and yield ratio calculated using default and corrected version of THERMUS are listed in [prediction-nofix.txt](prediction-nofix.txt) and [prediction-fix.txt](prediction-fix.txt) files, respectively.
A clear difference is observed for the yields where unstable particles are involved.

One particularly good example is the &Lambda;(1520)/&Lambda; ratio. The default THERMUS implementation yields
```bash
 3124 	 3122 	 Lambda(1520)/Lambda PREDICTION 	 0.061313
```
which appears to agree with the THERMUS value shown in [arXiv:1805.04361v1](http://arxiv.org/pdf/1805.04361v1.pdf) (Fig. 4).

The corrected THERMUS yields instead
```bash
 3124 	 3122 	 Lambda(1520)/Lambda PREDICTION 	 0.080032
```
This value is about 30% higher than the uncorrected one.

*Copyright (C) 2018  Volodymyr Vovchenko*
