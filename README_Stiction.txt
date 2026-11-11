Detection of Non-Location-Based Pattern Shifts Using PE (Stiction)


This README file covers the script, Stiction.ipynb, which relates to Section 3.2 providing a diagnostic framework for detecting and monitoring mechanical stiction (stick-slip) faults in control systems using B-splines, $L_1$ quantile splines, and Normalized Permutation Entropy (NPE).

Note: NPE denotes the normalised permutation entropy, which is denoted by H in the manuscript.


The script contains 2 core modules: 
Cell 1: Location Monitoring: Focuses on location-based monitoring, implementing Phase 1 and Phase 2 control charts (Pandolfo, Wei) to assess whether the mechanical deadband shifts the process location.
Cell 2: Complexity Analysis: Employs Permutation Entropy (PE) to quantify structural changes in the signal. 

Methodology
Stiction Modeling & Simulation: Simulates non-linear deadband behavior where the process output remains flat until the input signal exceeds the threshold.
Robust Curve Fitting: Contrasts standard Ordinary Least Squares (OLS) B-splines with L_1 Quantile Splines using statsmodels and patsy.
Location-Based Monitoring (Pandolfo & Wei): Assesses whether stiction shifts the process location, using depth-based metrics and robust/standardised deviation measures based on the Median Absolute Deviation (MAD). As shown in the manuscript, stiction alters the ordinal structure of the profile without significantly shifting its mean or median.
Phase 1/Phase 2 Monitoring & Bootstrapping: Uses nonparametric residual bootstrapping to establish stable In-Control (IC) baselines and empirical control limits, subsequently evaluating Out-of-Control (OOC) vulnerability.
Complexity Analysis (NPE): Maps sub-sequences of length d and time-delay t into ordinal patterns to quantify the predictability and disorder of the response variable.

Note that the roles of the spline-fitting and PE parameters are explained in README_Splines_Simulations.txt


Prerequisites
To run these scripts, ensure you have the required Python libraries installed:
pip install numpy pandas matplotlib patsy statsmodels

Execution Workflow
Both cells can be run independently, i.e. they do not depend on each other.

Running the script yields a folder Stiction_Plots that contains all relevant visuals.