**SENG 637- Dependability and Reliability of Software Systems**

**Lab. Report \#5 – Software Reliability Assessment**

| Group 4       |   |
|-----------------|---|
| Zohara Kamal |   |
| Thanoshan Vijayanandan |   |
| Minh Le |   |
| Shuvam Agarwala |   |

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

s

### A discussion on decision making given a target failure rate
s

### A discussion on the advantages and disadvantages of reliability growth analysis
| Aspect                 | Advantages                                                                         | Disadvantages                                                                 |
| ---------------------- | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Reliability estimation | Helps estimate current reliability and forecast future reliability from test data. | Predictions can be inaccurate if the data is incomplete or noisy.             |
| Fault discovery        | Finds defects systematically so they can be fixed during development.              | Later defects are often harder and more expensive to uncover.                 |
| Project control        | Lets teams track reliability progress and adjust plans early.                      | Can slow development because it adds extra test-fix-retest cycles.            |
| Model use              | Supports comparing different growth models to pick a suitable one.                 | Results depend heavily on choosing the right model.                           |
| Real-world readiness   | Improves product quality before release.                                           | Test conditions may not match real operating conditions, limiting usefulness. |

# Assessment Using Reliability Demonstration Chart 

# 

# Comparison of Results

# Discussion on Similarity and Differences of the Two Techniques

# How the team work/effort was divided and managed

# 

# Difficulties encountered, challenges overcome, and lessons learned

# Comments/feedback on the lab itself
