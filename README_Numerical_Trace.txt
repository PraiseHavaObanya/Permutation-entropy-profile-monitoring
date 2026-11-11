Purpose
Numerical_Trace.ipynb serves as a minimalist, reproducible test toolkit. It has 2 cells:
Numerical/Pipeline Trace: Performs a step-by-step trace of a 10-point synthetic dataset.
Transformation Roadmap: A visualization module that prints a structural map of how your data evolves from raw inputs to final scalar control limits.

Pipeline Trace (Cell 1)
The script performs a step-by-step trace of the data: 
Input Generation: Creates a small, noisy sine wave.
B-Spline Fitting: Executes the B-spline basis expansion and OLS regression.
Residuals: Demonstrates how residuals, which are required for valid nonparametric bootstrapping, are obtained.
Bootstrap Resampling: Displays the resulting bootstrap matrix for manual inspection.
PE Calculation: Computes permutation entropy values on the synthetic bootstrap results.
Control Limit Estimation: Derives the 2.5th and 97.5th percentiles as the lower and upper control limits (alpha = 0.05).

Technical Parameters & Concepts: 
Embedding Dimension (d): Determines the length of the subsequence to analyze. It sets the resolution of the ordinal patterns.
Time Delay (t): Defines the temporal spacing between elements in the embedded vector. t = 1 captures short-term, local transitions, while t > 1 skips consecutive values. The rule of thumb N >= 5d! ensures sufficient data to populate the d! possible permutations. The effective length of the signal is reduced by the delay, where the number of available embedded vectors is N - (d-1)t.



Transformation Roadmap (Cell 2)
This cell prints a tabular overview of the data progression:
Steps: Maps the progression from Data Collection through to the calculation of Control Limits.
Input/Output: Clearly defines the expected format (e.g., vectors, matrices, scalars) at each stage of the B-spline and entropy pipeline.

The first cell will print the numerical results of each step, and the second cell will generate the transformation roadmap table.

Note: This trace is a simplified illustration of the pipeline. For brevity, the spline is not refitted to each bootstrap sample, and the series length (n = 10) is below the N >= 5d! rule used in the manuscript. The full procedure is implemented in the main simulation scripts.