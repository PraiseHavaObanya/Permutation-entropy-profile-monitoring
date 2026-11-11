Detection of Pure Vertical Mean Shifts: A Limitation of PE


This README file covers the script, Vertical_Mean_Shifts.ipynb, which relates to Section 3.3 providing a diagnostic framework for detecting and monitoring faults that change the location, but not the ordinal patterns, of a profile using B-splines, $L_1$ quantile splines, and Normalized Permutation Entropy (NPE).

Note: NPE denotes the normalised permutation entropy, which is denoted by H in the manuscript.


The script contains 2 core modules: 
Cell 1: Location Monitoring: Focuses on location-based monitoring, implementing Phase 1 and Phase 2 control charts (Pandolfo, Wei) to quantify the shift in process location caused by the pure vertical mean shift.
Cell 2: Complexity Analysis: Employs Permutation Entropy (PE) to quantify structural changes in the signal. 

Methodology
Pure Vertical Mean Shift Modeling & Simulation: Adds a constant offset of 1.5 to the IC data, which translates all observations vertically without altering the relative ordering of adjacent points.
Robust Curve Fitting: Contrasts standard Ordinary Least Squares (OLS) B-splines with L_1 Quantile Splines using statsmodels and patsy.
Location-Based Monitoring (Pandolfo & Wei): Quantifies the shift in process location caused by the pure vertical mean shift, using depth-based metrics and robust/standardised deviation measures based on the Median Absolute Deviation (MAD).
Phase 1/Phase 2 Monitoring & Bootstrapping: Uses nonparametric residual bootstrapping to establish stable In-Control (IC) baselines and empirical control limits, subsequently evaluating Out-of-Control (OOC) vulnerability.
Complexity Analysis (NPE): Maps sub-sequences of length d and time-delay t into ordinal patterns to quantify the predictability and disorder of the response variable. Because the vertical shift leaves the ordinal patterns unchanged, PE is not expected to detect it; this illustrates the limitation of PE discussed in the manuscript.

Note that the roles of the spline-fitting and PE parameters are explained in README_Splines_Simulations.txt


Prerequisites
To run these scripts, ensure you have the required Python libraries installed:
pip install numpy pandas matplotlib patsy statsmodels

Execution Workflow
Both cells can be run independently, i.e. they do not depend on each other.

Running the script yields a folder Vertical_Shift_Plots that contains all relevant visuals.