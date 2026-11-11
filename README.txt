An entropy-based distribution-free approach for profile monitoring

Code accompanying the paper:

    An entropy-based distribution-free approach for profile monitoring
    P.O. Obanya, R.L.J. Coetzer and S. Liebenberg
    Focus Area for Pure and Applied Analytics, North-West University, South Africa
    National Institute for Theoretical and Computational Sciences (NITheCS), South Africa
    [Journal, volume, pages, year, DOI - to be added on publication]


OVERVIEW

This repository contains the Python code (Jupyter notebooks) used to generate the simulation results in the paper. The paper introduces permutation entropy (PE) as a non-parametric, distribution-free statistic for profile monitoring. PE quantifies the ordinal (rank-order) structure of a profile, and is therefore sensitive to deviations that change the temporal ordering of observations, even when the mean or median of the profile is unchanged.

The monitoring procedure is as follows:

Phase 1 (establishing control limits)
    1. Fit a cubic B-spline to the in-control (IC) data.
    2. Apply non-parametric residual bootstrapping: resample the residuals with replacement, add them to the fitted values, and refit the spline (B = 200 replicates).
    3. Calculate the normalised PE, H, of each bootstrapped profile.
    4. Set the lower and upper control limits (LCL and UCL) as the 100(alpha/2)-th and 100(1 - alpha/2)-th empirical percentiles of the bootstrapped H values.

Phase 2 (monitoring)
    1. Smooth each new profile using the same settings as in Phase 1 and calculate its H value.
    2. Classify the profile as out-of-control (OOC) if H <= LCL or H >= UCL.


CONTENTS

Section 3.1 - Sensitivity of PE to heteroscedastic and Gaussian processes (IC data set and OOC Data Sets 1-3)
    Spline_Simulations.ipynb
    PE.ipynb
    Control_Charts.ipynb
    Histograms.ipynb
    README_Splines_Simulations.txt

Section 3.2 - Detection of non-location-based pattern shifts (valve stiction), compared with location-based statistics
    Stiction.ipynb
    README_Stiction.txt

Section 3.3 - Detection of pure vertical mean shifts, illustrating the limitation of PE
    Vertical_Mean_Shifts.ipynb
    README_VMS.txt

Numerical trace - a small step-by-step example of the pipeline
    Numerical_Trace.ipynb
    README_Numerical_Trace.txt

Each README file explains the corresponding notebooks, their parameters and the order in which they should be run.

The case study in the paper (ash lock temperature profiles from a commercial coal gasifier) uses confidential industrial data, which cannot be shared. That code is therefore not included.


REQUIREMENTS

Python 3 with the following packages:

    pip install numpy pandas scipy matplotlib patsy statsmodels fbm


USAGE

Section 3.1: Run Spline_Simulations.ipynb, then PE.ipynb (once for each data set; see README_Splines_Simulations.txt), and then Control_Charts.ipynb and Histograms.ipynb.

Sections 3.2 and 3.3: Run Stiction.ipynb and Vertical_Mean_Shifts.ipynb. The two cells in each notebook can be run independently, and the figures are saved to the folders Stiction_Plots and Vertical_Shift_Plots, respectively.

All simulations use fixed random seeds, so the results in the paper can be reproduced.


CITATION

If you use this code, please cite the paper:

    Obanya, P.O., Coetzer, R.L.J. and Liebenberg, S. An entropy-based distribution-free approach for profile monitoring. [Journal, volume, pages, year, DOI - to be added on publication]


