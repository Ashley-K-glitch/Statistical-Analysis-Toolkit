Wakala Plus – Daily Deposit Statistics Toolkit

1. Project Overview

Wakala Plus operates M-Pesa agent outlets across Nairobi, Thika, Machakos and Nakuru. 

The team needs a reliable way to monitor daily deposit amounts across its agent . Unusual deposit patterns may indicate potential fraud, operational challenges or errors in data recording.

2. Project instructions

Calculate mean, median and mode

Implement mean, median and mode with plain Python — no statistics module, no NumPy. mode returns a list because data can have several modes or none worth reporting; document how you treat 'every value appears once'.


Calculate variance and standard deviation

Implement variance(values, sample) and std_dev(values, sample) supporting both sample (n − 1) and population (n) formulas. Explain in your README which one suits this dataset and why.


Handle invalid and missing values

Implement load_column(path, column) returning the valid floats and a list of rejected (row_number, raw_value) pairs. Do not guess at values that cannot be trusted; every rejection must appear in the report with a reason.


Detect outliers using IQR

Implement quartiles(values) and iqr_outliers(values, k) returning the IQR, both fences and the outlying values. Quartile methods differ — choose one, name it, and make sure your NumPy comparison uses the same one.


Build a StatisticsAnalyzer class

Implement StatisticsAnalyzer with a from_csv class method, a summary() dict, a without_outliers() method returning a new analyzer, and report(). Methods must not recalculate the sorted data on every call.


Compare your results with NumPy

Implement compare_with_numpy(analyzer) — the only place numpy is imported — and report MATCH or MISMATCH per statistic using a tolerance, not ==. Any mismatch must be explained (e.g. ddof, quartile method).


Generate a statistical summary report

Print and save output/stats_report.txt following the expected layout, showing statistics for all data and with outliers removed side by side. Add three sentences for the risk team on what the outliers might mean.


Write unit tests

Fill in test_stats_toolkit.py with at least eight passing tests using unittest or pytest, covering empty input, even/odd lengths, ties in mode, sample vs population variance, outlier detection and rejected values. Use small hand-checkable inputs, not the dataset.


3. Statistical Functions

The statistical calculations were implemented using plain Python.

4. Mean

The mean represents the average daily deposit amount.

It is calculated by adding all deposit values and dividing the total by the number of observations.

Formula:

Mean = Sum of all values / Number of values

In this project, the mean provides an overview of the average deposit activity across the analysed records.

5. Median

The median represents the middle value when all observations are arranged in ascending order.

For an odd number of observations, the middle value is selected.

For an even number of observations, the two middle values are added and divided by two.

The median is useful because it is less affected by unusually high or low deposit values than the mean.

6. Mode

The mode identifies the most frequently occurring deposit amount.

A dictionary is used to count the frequency of each value.

The implementation supports:

A single mode.

Multiple modes when values share the highest frequency.

An empty list when no value occurs more than once.

7. Variance

Variance measures how widely deposit values are spread around their mean.

Two types are supported:

Population variance

Used when the dataset represents the entire population being analysed.

The sum of squared differences from the mean is divided by the total number of observations, n.

Sample variance

Used when the dataset represents a sample of a larger population.

The sum of squared differences is divided by n - 1.

The function accepts a sample parameter to determine which calculation to perform.

8. Standard Deviation

Standard deviation measures the spread of observations around the mean.

It is calculated by taking the square root of the variance.

Unlike variance, standard deviation is expressed in the original unit of measurement.

For this project, that means Kenyan shillings (KES).

Both sample and population standard deviation are supported.

9. Outlier Detection Using IQR

The Interquartile Range (IQR) method is used to identify unusually high or low deposit amounts.

The IQR measures the spread of the middle 50% of the observations.

Quartiles

The calculation uses three quartiles:

Q1: First quartile, representing the 25th percentile.

Q2: Second quartile, representing the median.

Q3: Third quartile, representing the 75th percentile.

The project uses the median-of-halves method to calculate Q1 and Q3.

For an odd number of observations, the overall median is excluded when dividing the sorted data into the lower and upper halves.

IQR calculation

IQR = Q3 - Q1

Outlier boundaries

The standard multiplier of 1.5 is used by default.

Lower Fence = Q1 - (1.5 × IQR)

Upper Fence = Q3 + (1.5 × IQR)

Any value below the lower fence or above the upper fence is flagged as an outlier.

The iqr_outliers() function returns:

IQR.

Lower fence.

Upper fence.

List of detected outliers.

The multiplier can also be adjusted using the k parameter.

10. Interpretation

For Wakala Plus:

Unusually high deposits may require investigation for suspicious transactions or legitimate high-volume activity.

Unusually low deposits may indicate float shortages, operational disruptions or incomplete records.

Extreme values may also result from data-entry errors.

An outlier is not automatically evidence of fraud. It is a signal that further investigation may be necessary.