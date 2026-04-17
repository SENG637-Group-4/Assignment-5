**SENG 637- Dependability and Reliability of Software Systems**

**Lab. Report \#5 – Software Reliability Assessment**

| Group 4       |  
|-----------------|
| Zohara Kamal |  
| Thanoshan Vijayanandan |  
| Minh Le |  
| Shuvam Agarwala |  

# Introduction
In this assignment, we explore the use of Reliability Growth Testing and Reliability Demonstration Chart to assess the reliability of a software system. Then we will compare these techniques to see what they are like and how they are different from one another.

# Assessment Using Reliability Growth Testing 
For Reliability Growth Testing, we used C-SFRAT as it's the recommended tool in the assignment. We had no trobule in downloading, installing and set up the tool for the analysis. Since C-SFRAT worked for us, we haven't tried other suggested alternative tools like SweET and SFRAT.

### Result of model comparison and range analysis (an explanation of which part of data is good for proceeding with the analysis)
To select top two models, first, we ran all the models for the given failure data with every covariate combination possible. In the process, we obtained the relevant comparison data ([CSV](./artifacts/c-sfrat/model_results_tab_3.csv)). Then, we sorted the Akaike Information Criterion (AIC) and Bayesian Information Criteria (BIC) columns from the lowest values. The reason for this is that, the lower the AIC and BIC score, the better the model ([Choosing the Best Model: A Friendly Guide to AIC and BIC](https://medium.com/@jshaik2452/choosing-the-best-model-a-friendly-guide-to-aic-and-bic-af220b33255f)).

With this process, we determined that the DW3 model, with covariate F is the best model, with AIC of 122.19925720563498 and BIC of 127.93520602357556. Next is the GM model with covariate F with AIC of 125.3234449148569 and BIC of 129.62540652831234.

![Best model](./artifacts/c-sfrat/best-model.png)

### Plots for failure rate and reliability of the SUT for the test data provided
Time to Failure Plot:
![Time to Failure Plot](./artifacts/c-sfrat/time-to-failure-plot.png)

Intensity Plot:
![Intensity Plot](./artifacts/c-sfrat/intensity-plot.png)

### Result of Range Analysis

From the provided plots, the failure behavior of the system changes across different intervals.

In the early intervals, the cumulative failure curve generally increases in a gradual way, and the failure intensity remains mostly moderate, although there are still some fluctuations. Both DW3 and GM models follow the actual data reasonably well in this region, indicating that the overall trend is predictable, even if the behavior is not perfectly smooth.

Around intervals 20 to 23, there is a more noticeable increase in cumulative failures. The failure intensity plot also shows clear spikes in this region, suggesting bursts of failures and greater variability. After this point, the data remains somewhat irregular, but the models continue to track the general trend fairly well.

A subset of 21 out of 31 intervals, or about 70% of the dataset, is used to train the models, with the remaining intervals used for prediction. This choice appears reasonable because the predicted DW3 and GM curves still follow the later cumulative failure trend closely, even though they smooth over some of the sharper changes in the raw data.

Therefore, the earlier portion of the data is more stable and more suitable for trend analysis, while the later intervals capture more volatile system behavior that is important for evaluating model performance and prediction accuracy.

### Failure Rate and Reliability of the SUT

From the cumulative failure plot, the total number of failures at interval 31 is approximately 92. Therefore, the average failure rate is:

Failure Rate = 92 / 31 = 2.96 failures per interval

The failure intensity plot shows that the failure rate is not constant over time. In the early intervals, the failure intensity is generally moderate, but it still fluctuates. Around intervals 20 to 23, there are clear spikes where the failure rate increases sharply, reaching roughly 7 to 10 failures per interval. After this point, the failure rate remains variable.

This indicates that the system exhibits non-uniform and bursty failure behavior.

### Model Performance

At interval 31:
- Raw Data: Failure Rate = 2.96, MTTF = 0.337  
- DW3 Prediction: Failure Rate = 2.94, MTTF = 0.341  
- GM Prediction: Failure Rate = 2.90, MTTF = 0.344  

Using interval 21 for the DW3 and GM models to predict the final 10 intervals, the predicted failure rate and MTTF are very close to the original failure data.

The predicted values are close to the actual values, which indicates that both models provide a good overall fit to the cumulative failure trend.

However, the failure intensity plot shows that both models smooth out the sharper spikes in the real data. This suggests that while the models capture the general trend well, they may underestimate sudden bursts of failures and short-term variability.

### Decision Making Based on Target Failure Rate

Assume that the acceptable target failure rate for the system is 4 failures per interval.

The average failure rate of the system is approximately 2.96 failures per interval, which is below the target threshold. Based on this average, the system can be considered acceptable.

However, the failure intensity plot shows that there are several intervals where the failure rate exceeds the target value, with spikes reaching roughly 7 to 10 failures per interval, especially around intervals 20 to 23. This indicates that the system experiences periods of high instability.

Therefore, relying solely on the average failure rate can be misleading. While the system is acceptable on average, its actual behavior shows intermittent violations of the target threshold.

In conclusion, the system can be considered acceptable overall, but not consistently reliable. The presence of significant failure spikes suggests that continuous monitoring and potential improvements are necessary to ensure stable and predictable performance.

### Advantages and disadvantages of reliability growth analysis
| Aspect                 | Advantages                                                                         | Disadvantages                                                                 |
| ---------------------- | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Reliability estimation | Helps estimate current reliability and forecast future reliability from test data. | Predictions can be inaccurate if the data is incomplete or noisy.             |
| Fault discovery        | Finds defects systematically so they can be fixed during development.              | Later defects are often harder and more expensive to uncover.                 |
| Project control        | Lets teams track reliability progress and adjust plans early.                      | Can slow development because it adds extra test-fix-retest cycles.            |
| Model use              | Supports comparing different growth models to pick a suitable one.                 | Results depend heavily on choosing the right model.                           |
| Real-world readiness   | Improves product quality before release.                                           | Test conditions may not match real operating conditions, limiting usefulness. |

# Assessment Using Reliability Demonstration Chart 

The RDC-11 Excel worksheet was used to generate the Reliability Demonstration Chart (RDC) as required. However, the default configuration of the tool supports only 16 failures, whereas the provided dataset contains 92 failures. Therefore, the worksheet configuration was modified to accommodate the full dataset.

The default risk parameters provided in the RDC tool:

| Parameter                | Value |
| ------------------------ | ----- |
| Discrimination Ratio (γ) | 2     |
| Developer's Risk (α)     | 0.1   |
| User's Risk (β)          | 0.1   |

<img width="471" height="198" alt="image" src="https://github.com/user-attachments/assets/beddb081-2e4a-4266-bc55-759fd5658e78" />


The original dataset was given in terms of failure counts per time interval, rather than exact times between failures, which are required for RDC analysis. To address this, the data was transformed by assuming that failures are uniformly distributed within each time interval.

For example:

At T = 1, there are 2 failures → assumed at times 0.5 and 1.0

At T = 2, there are 11 failures → evenly distributed between 1 and 2

| T   | FC  |
| --- | --- |
| 1   | 2   |
| 2   | 11  |

This produces the required time between failures and cumulative time.

Converted Data Example

| Cumulative Failure Count | Time between failures | Cumulative Time |
| ------------------------ | --------------------- | --------------- |
| 1                        | 0.5                   | 0.5             |
| 2                        | 0.5                   | 1               |

This transformation was applied consistently across the entire dataset to generate all 92 failure points required for RDC plotting.

In summary, the dataset required preprocessing before it could be used in the RDC tool. The key steps included:
- Modifying the RDC-11 worksheet to support 92 failures
- Retaining the default risk parameters (γ, α, β)
- Converting interval-based failure data into time-between-failures format using a uniform distribution assumption

This prepared dataset was then used to plot the RDC and assess whether the system meets the required MTTF target.

RDC dataset can be found:

- [md file](RDC_part_2_data.md)

- [csv file](RDC_part_2_data.csv)

The full RDC sheet that we used for part 2 can be found [here](RDC_sheet_part_2.xlsm).

## RDC Graphs

### First RDC graph (minimum MTTF)
The minimum MTTF for the system to be considered acceptable. This minimum was determined by changing the FIO until a minimum was found; where the SUT barely enters the accept region. 
- Maximum Acceptable Number of Failures = 1200
- FIO = 1200 failures/31 intervals = 38.70
- MTTF = 1/38.70 = 0.026

<img width="675" height="146" alt="image" src="https://github.com/user-attachments/assets/1e77dddb-aa0c-4114-b6d3-779956080e2d" />

<img width="781" height="705" alt="image" src="https://github.com/user-attachments/assets/86bca538-fed7-4da1-b7da-ba3ffb455779" />


### Second RDC graph (double the minimum MTTF)
The third plot is double the minimum MTTF. In this case, the SUT goes into the continue testing region and a bit in reject region.
- Maximum Acceptable Number of Failures = 600
- FIO = 600 failures/31 intervals = 19.35
- MTTF = 1/19.35 = 0.052

When the MTTF is doubled, the requirement becomes much stricter. This means the system is expected to fail less often. The allowed failure rate becomes smaller. The accept region becomes smaller. Because of this, the failure data gets very close to the reject region. This shows that the system cannot meet this high MTTF requirement. So, this MTTF is too high for the system.

<img width="683" height="154" alt="image" src="https://github.com/user-attachments/assets/38148b8e-2d3d-4c8a-a861-1ba27f8b0338" />

<img width="775" height="709" alt="image" src="https://github.com/user-attachments/assets/18ac66d0-601b-46ba-b5a5-9ce8ca12cd7e" />


### Third RDC graph (half the minimum MTTF)
The fourth plot is half the minimum MTTF. In this case, the SUT goes into the accept region.
- Maximum Acceptable Number of Failures = 2400
- FIO = 2400 failures/31 intervals = 77.42
- MTTF = 1/77.42 = 0.013

When the MTTF is cut in half, the requirement becomes easier. This means the system is allowed to fail more often. The allowed failure rate becomes larger. The accept region becomes bigger. Because of this, the failure data clearly falls in the accept region. This shows that the system meets this lower MTTF requirement. So, this MTTF is easy to satisfy, maybe too easy.

<img width="679" height="148" alt="image" src="https://github.com/user-attachments/assets/f08a31b6-de6a-4cce-a882-23611d2ac52f" />

<img width="782" height="701" alt="image" src="https://github.com/user-attachments/assets/13dea72b-1a24-47ba-a99b-2ce8f06f68cc" />


### Fourth RDC graph (maximum acceptable number of failures = number of failures)
The SUT almost goes into the reject region.
- Maximum Acceptable Number of Failures = 92
- FIO = 92 failures/31 intervals = 2.97
- MTTF = 1/2.97 = 0.337

<img width="681" height="147" alt="image" src="https://github.com/user-attachments/assets/19581a23-6a70-420d-806f-b20c03b964d6" />

<img width="781" height="704" alt="image" src="https://github.com/user-attachments/assets/ebfa0a29-ef9c-4de4-96da-df3f012db16b" />

### Advantages and disadvantages of RDC
| Aspect                | Advantages                                                        | Disadvantages                                                 |
| --------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Simplicity            | Easy to understand and communicate results                        | May oversimplify complex reliability behavior and ignore underlying failure patterns                 |
| Decision-making       | Clear accept, reject and continue regions support fast decisions   | Highly dependent on predefined thresholds and risk levels     |
| Efficiency            | Low time and cost, minimal computation required                   | Trades off depth and precision for speed                      |
| Visualization         | Graphical format makes trends and outcomes easy to interpret      | Can be misleading with limited or noisy data                  |
| Parameter sensitivity | Flexible through parameters (maximum acceptable number of failures and MTTF) to match requirements | Incorrect parameter choice (like MTTFmin) invalidates results |
| Quantitative accuracy | Provides general reliability indication                           | Cannot compute exact reliability or availability values       |
| Data dependency       | Works with relatively small datasets (default setting is 16, in this assignment is 92)                             | Strongly affected by data quality, sample size, and representativeness of failures             |

# Comparison of Results

# Discussion on Similarity and Differences of the Two Techniques
### Similarities between Reliability Growth Testing (RGT) and Reliability Demonstration Chart (RDC)

- Both approaches are employed to estimate and analyze system reliability.
- Each method depends on predefined reliability metrics such as failure rate or Mean Time To Failure (MTTF).
- Both require observed failure data as input for analysis.

### Differences between RGT and RDC

- Reliability Growth Testing (RGT) focuses on predicting future reliability trends using historical failure data, whereas Reliability Demonstration Chart (RDC) is used to assess whether the system meets specified reliability targets based on observed data.

- RGT applies statistical or mathematical failure growth models to generate reliability forecasts, while RDC utilizes predefined risk profiles to evaluate system reliability compliance.

- RGT primarily provides predictive insights based on the chosen model and available data, whereas RDC supports decision-making by determining whether the System Under Test (SUT) satisfies acceptable reliability criteria.

# How the team work/effort was divided and managed
| Team member                     | Section                                                                 |
|--------------------------|-------------------------------------------------------------------------|
| Zohara Kamal            | Difficulties and challenges, and comments and feedback |
| Thanoshan Vijayanandan             | Part 1: Reliability Growth Testing, Part 2: Reliability Demonstration Chart   |
| Minh Le      | Part 1: Reliability Growth Testing, Part 2: Reliability Demonstration Chart |
| Shuvam Agarwala | Part 2: Reliability Demonstration Chart                      |

# Difficulties encountered, challenges overcome, and lessons learned
- The failure dataset was not directly compatible with the Reliability Demonstration Chart (RDC) format. Specifically, the data was provided as failures per interval, whereas RDC requires time-between-failures data.

- To address this mismatch, a transformation was applied by assuming failures were uniformly distributed within each interval to derive time-between-failures. However, this assumption is unrealistic in practice, which may introduce inaccuracies in the results.

- Additionally, no explicit target values for MTTF/FIO or a defined risk profile were provided for the RDC analysis. A default risk profile was therefore assumed, but alternative profiles could significantly impact the evaluation outcomes. As a result, it is not possible to conclusively determine whether the System Under Test (SUT) meets acceptability criteria.

- The provided RDC dataset was inconsistent with the given failure data of the SUT. Consequently, substantial modifications to the RDC spreadsheet were required to accommodate the necessary number of data points.

- The RDC chart did not correctly visualize the accept, continue, and reject regions. Furthermore, adjustments to the risk profile did not reflect on the graph, necessitating manual modifications to the underlying Excel sheet.

- The C-SFRAT tool functioned correctly in a Windows environment; however, compatibility issues and execution errors were encountered when attempting to run it on macOS.

# Comments/feedback on the lab itself

- The Reliability Demonstration Chart should have allowed input of all the failure data. It was very difficult to get it to properly graph the data.

- There was very little documentation on the failure dataset.

- The lab provided practical exposure to reliability engineering concepts such as Reliability Growth Testing (RGT) and Reliability Demonstration Charts (RDC), helping bridge theory and application.

- It encouraged critical thinking by requiring us to handle imperfect data and make reasonable assumptions during analysis.

- The use of real-world-like failure datasets made the exercise more realistic and relevant to industry scenarios.

- The lab introduced useful tools (e.g., C-SFRAT), giving hands-on experience with software used in reliability analysis.

- It highlighted the challenges involved in data preprocessing and format conversion, which are important skills in software engineering and data analysis.

- The comparison between RGT and RDC helped in understanding the strengths and limitations of different reliability assessment techniques.

- It emphasized the importance of model assumptions and their impact on the validity of results.
