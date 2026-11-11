This README file covers 4 scripts namely:

Spline_Simulations.ipynb: A Jupyter Notebook containing all simulation sets (IC, OOC 1, OOC 2, OOC 3). Each simulation is self-contained within an independent cell.
PE.ipynb: A single-cell Jupyter Notebook for performing Permutation Entropy (PE) complexity analysis, based on ordinal patterns.
Control_Charts.ipynb: A single-cell Jupyter notebook for monitoring of H values over time.
Histograms.ipynb: A single-cell Jupyter notebook for comparative distribution analysis between IC and OOC complexity metrics.

Individual Python Scripts (.py): You can copy the contents of any notebook cell into a standalone .py file to execute it locally.

These 4 scripts are related to Section 3.1 (Sensitivity of PE to Heteroscedastic and Gaussian Processes). Note that the scripts should be run in order of appearance.

Algorithm: Bootstrap-Based Permutation Entropy Control Chart

INPUT:
    In-control data D_IC  = {(x_i,y_i)} for i = 1, ..., n
    Number of bootstrap replicates B
    Significance level α
    Smoothing procedure S(·)
    Permutation entropy function PE(·)

OUTPUT:
    Lower control limit (LCL)
    Upper control limit (UCL)

PHASE I: ESTABLISHMENT OF CONTROL LIMITS

1.  Fit the smoothing function (f̂) ̂(x) = S(D_IC) to the in-control data.

2.  Obtain the fitted values:
        ŷ_i=f ̂  (x_i),i = 1,...,n.

3.  Calculate the residuals:
        e_i  = y_i  - ŷ_i,i = 1,...,n.

4.  For b = 1,...,B:

        a. Resample the residuals {e_i} with replacement to obtain
           bootstrap residuals {e_i^* (b)}.

        b. Generate a bootstrap data set:
               y_i^* (b) = ŷ_i  + e_i^* (b), for i = 1,...,n.

        c. Fit the smoothing function to the bootstrap data set to obtain:
                f ̂_b^* (x) = S(x_i,y_i^* (b)).

        d. Calculate the permutation entropy of the estimated
           bootstrap profile:
               H^* (b) = PE(f ̂_b^* (x)).

5.  Construct the bootstrap distribution:
        H^*  = {H^* (1),H^* (2),...,H^* (B)}.

6.  Determine the two-sided control limits:
        LCL = Q_(α/2) (H^*)
        UCL = Q_(1-α/2) (H^*).

PHASE II: MONITORING OF NEW PROFILES

For each new profile D_new  :

1.  Apply the same smoothing procedure used in Phase I to obtain
    the estimated profile:
        f ̂_new (x) = S(D_new).

2.  Calculate the permutation entropy:
        H_new  = PE(f ̂_new (x)).

3.  If: H_new  ≤ LCL  or  H_new  ≥ UCL,
    then classify the profile as Out-of-Control (OOC).
    Otherwise, classify the profile as In-Control (IC).

Methodology
Simulation & Bootstrapping (Spline_Simulations.ipynb): Nonparametric Residual Bootstrapping is used to quantify uncertainty in spline regression. The pipeline follows these steps:
Data Generation: Creation of synthetic data with varying characteristics (sine waves, linear transitions, fractional Brownian motion, and heteroscedastic noise). In OOC Data Set 2, the fBm segment is scaled and shifted to ensure continuity at x = 9.6, and a small linear drift, 0.05(x - 9.6), is added.
B-Spline Fitting: Uses patsy to generate basis functions and numpy to solve the Ordinary Least Squares (OLS) regression.
Resampling: Generates 200 bootstrap replicates by resampling model residuals, without assuming a specific error distribution.

2. Complexity Analysis (PE.ipynb): Quantifies the degree of order or disorder in the bootstrapped spline fits using permutation entropy.
Mechanism: It maps sub-sequences of length d and time-delay t into ordinal patterns.
Normalization: The output (H) is normalized between 0 (perfectly predictable/monotonic) and 1 (completely unpredictable), providing a complexity signature that can be used to distinguish between profiles. This normalised permutation entropy is denoted by H in the manuscript.

3. Monitoring & Control Charts (Control_Charts.ipynb): This monitors process stability over time:
Threshold Setting: Uses quantiles of IC data to establish Lower (LCL) and Upper (UCL) control limits.
Deviation Detection: Plots H-values from OOC simulations against these limits to identify statistically significant deviations.

4. Distributional Complexity (Histograms.ipynb): This assesses the statistical distance between process states. The use of Kernel Density Estimation (KDE) results in the overlay of KDE curves onto histograms to visualize the probability density of H-values.


Technical Parameters & Concepts
Spline_Simulations.ipynb
Degrees of Freedom (df_r_equivalent): Dictates spline complexity. A higher df increases variance (following the noise), while a lower df increases bias (resulting in a smoother curve).
Knot Placement: Determined using quantiles of the input data (np.percentile) to optimize flexibility where data density is highest.
Hurst Parameter (hurst_param, denoted by r in the manuscript): Governs the "memory" of the fBm in OOC Data Set 2. r < 0.5 results in anti-persistent (mean-reverting) behaviour, while r > 0.5 results in persistent, long-range dependence. In this study, r = 0.1.
PE.ipynb
PE parameters (d, t): Defines the pattern window. The embedding dimension d determines the length of the subsequence to analyze. It sets the resolution of the ordinal patterns. Time delay t defines the temporal spacing between elements in the embedded vector. t = 1 captures short-term, local transitions in the signal (high-frequency detail), while t > 1 allows the algorithm to skip over consecutive values to identify broader, long-range structural trends. If t is too large, you risk missing the fine-grained structural changes. Remember that the rule of thumb N >= 5d! ensures that you have enough data points to populate the d! possible permutations reliably. While d primarily constrains the total possible patterns, t dictates the effective length of the signal being analyzed, as the number of available embedded vectors is N - (d-1)t.

Prerequisites
To run these scripts, you will need the following Python libraries:
pip install numpy pandas matplotlib patsy scipy fbm

How to Use
Generate Data: Execute Spline_Simulations.ipynb to create your Spline_Simulations_*.csv output files.
Calculate Complexity: Execute PE.ipynb. This script will process the CSV files and generate complexity outputs.
Visualize: Execute Control_Charts.ipynb for time-series monitoring and Histograms.ipynb for distribution comparisons.

Note the following regarding PE.ipynb:

1. the input files are the output files from Spline_Simulations.ipynb, namely Spline_Simulations.csv, Spline_Simulations_OOC_New_1.csv, Spline_Simulations_OOC_New_2.csv, Spline_Simulations_OOC_New_3.csv, for the IC Data Set, OOC Data Set 1, OOC Data Set 2 and OOC Data Set 3, respectively.

2. the specific data set for which H is to be calculated is defined by the variable df, e.g df = pd.read_csv('Spline_Simulations.csv')

3. the output file names for the PE.ipynb, for the respective input files, should be defined under the variable filename as follows:
filename = f"IC_H_values_Spline_Simulations_d{d}_t{t}.csv" for the IC Data Set
filename = f"OOC_H_values_Spline_Simulations_New_1_d{d}_t{t}.csv" for OOC Data Set 1
filename = f"OOC_H_values_Spline_Simulations_New_2_d{d}_t{t}.csv" for OOC Data Set 2
filename = f"OOC_H_values_Spline_Simulations_New_3_d{d}_t{t}.csv" for OOC Data Set 3

Endeavour to input the corresponding df and filename variables before execution.

Following the execution of Spline_Simulations.ipynb and PE.ipynb, the visualization scripts (Control_Charts.ipynb and Histograms.ipynb) can be executed.