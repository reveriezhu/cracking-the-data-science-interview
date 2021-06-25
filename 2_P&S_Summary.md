# Practical Statistics For Data Scientists

* [Exploratory Data Analysis](#exploratory-data-analysis)
* [Data and Sampling Distributions](#data-and-sampling-distributions)
* [Statistical Experiments and Significance Testing](#statistical-experiments-and-significance-testing)

## Exploratory Data Analysis

Here are the sections:

* [Elements of Structured Data](#elements-of-structured-data)
* [Rectangular Data](#rectangular-data)
* [Estimates of Location](#estimates-of-location)
* [Estimates of Variability](#estimates-of-variability)
* [Exploring the Data Distribution](#exploring-the-data-distribution)
* [Exploring Binary and Categorical Data](#exploring-binary-and-categorical-data)
* [Correlation](#correlation)
* [Exploring Two or More Variables](#exploring-two-or-more-variables)

### Elements of Structured Data

* Data is typically classified in software by type.
* Data types include continuous, discrete, categorical, and ordinal.
* Data typing in software acts as a signal to the software on how to process the data.

### Rectangular Data

* The basic data structure in data science is a rectangular matrix in which rows are records and columns are variables/features.
* Terminology can be confusing; there are a variety of synonyms arising from the different disciplines that contribute to data science (statistics, computer science, and information technology).

### Estimates of Location

* The basic metric for location is the mean, but it can be sensitive to extreme values (outliers).
* Other metrics (median, trimmed mean) are more robust.

### Estimates of Variability

* The variance and standard deviation are the most widespread and routinely reported statistics of variability.
* Both are sensitive to outliers.
* More robust metrics include mean and median absolute deviations from the mean and percentiles (quantiles).

### Exploring the Data Distribution

* A frequency histogram plots frequency counts on the y-axis and variable values on the x-axis; it gives a sense of the distribution of the data at a glance.
* A frequency table is a tabular version of the frequency counts found in a histogram.
* A boxplot - with the top and bottom of the box at the 75th and 25th percentiles, respectively - also gives a quick sense of the distribution of the data; it is often used in side-by-side displays to compare distributions.
* A density plot is a smoothed version of a histogram; it requires a function to estimate a plot based on the data (multiple estimates are possible, of course).

### Exploring Binary and Categorical Data

* Categorical data is typically summed up in proportions, and can be visualized in a bar chart.
* Categories might represent distinct things (apples and oranges, male and female), levels of a factor variable (low, medium, and high), or numeric data that has been binned.
* Expected value is the sum of values times their probability of occurrence, often used to sum up factor variable levels.

### Correlation

* The correlation coefficient measures the extent to which two variables are associated with one another.
* When high values of v1 go with high values of v2, v1 and v2 are positively associated.
* When high values of v1 are associated with low values of v2, v1 and v2 are negatively associated.
* The correlation coefficient is a standardized metric so that it always ranges from -1 to +1.
* A correlation coefficient of 0 indicates no correlation, but be aware that random arrangements of data will produce both positive and negative values for the correlation coefficient just by chance.

### Exploring Two or More Variables

* Hexagonal binning and contour plots are useful tools that permit graphical examination of 2 numeric variables at a time, without being overwhelmed by huge amounts of data.
* Contingency tables are the standard tool for looking at the counts of 2 categorical variables.
* Boxplots and violin plots allow you to plot a numeric variable against a categorical variable.

[back to top](#practical-statistics-for-data-scientists)

## Data and Sampling Distributions

A popular misconception holds that the era of big data means the end of a need for sampling. In fact, the proliferation of data of varying quality and relevance reinforces the need for sampling as a tool to work efficiently with a variety of data and to minimize bias. Even in a big data project, predictive models are typically developed and piloted with samples. Samples are also used in tests of various sorts (e.g., pricing, web treatments).

Figure below shows a schematic that underpins the concepts in this chapter. The lefthand side represents a population that, in statistics, is assumed to follow an underlying but *unknown* distribution. The only thing available is the *sample* data and its empirical distribution, shown on the righthand side. To get from the lefthand side to the righthand side, a *sampling* procedure is used (represented by an arrow). Traditional statistics focused very much on the lefthand side, using theory based on strong assumptions about the population. Modern statistics has moved to the righthand side, where such assumptions are not needed.

![Figure 2-1](psds_0201.png)

Here are the sections:

* [Random Sampling and Sample Bias](#random-sampling-and-sample-bias)
* [Selection Bias](#selection-bias)
* [Sampling Distribution of a Statistic](#sampling-distribution-of-a-statistic)
* [The Bootstrap](#the-bootstrap)
* [Confidence Intervals](#confidence-intervals)
* [Normal Distribution](#normal-distribution)
* [Long Tailed Distribution](#long-tailed-distribution)
* [Student t-Distribution](#student-t-distribution)
* [Binomial Distribution](#binomial-distribution)
* [Poisson and Related Distributions](#poisson-and-related-distributions)

### Random Sampling and Sample Bias

- Even in the era of big data, random sampling remains an important arrow in the data scientist's quiver.
  - *Random sampling* is a process in which each available member of the population being sampled has an equal chance of being chosen for the sample at each draw.
  - Sampling can be done *with replacement*, in which observations are put back in the population after each draw for possible future re-selection.
  - Or it can be done *without replacement*, in which case observations, once selected, are unavailable for future draws.
- Bias occurs when measurements or observations are systematically in error because they are not representative of the full population.
- Data quality is often more important than data quantity, and random sampling can reduce bias and facilitate quality improvement that would be prohibitively expensive.

[back to current section](#data-and-sampling-distributions)

### Selection Bias

- Specifying a hypothesis, then collecting data following randomization and random sampling principles, ensures against bias.
- All other forms of data analysis run the risk of bias resulting from the data collection/analysis process (repeated running of models in data mining, data snooping in research, and after-the-fact selection of interesting events).
- *Regression to the mean* refers to a phenomenon involving successive measurements on a given variable: extreme observations tend to be followed by more central ones. Attaching special focus and meaning to the extreme value can lead to a form of selection bias.

[back to current section](#data-and-sampling-distributions)

### Sampling Distribution of a Statistic

- The frequency distribution of a sample statistic tells us how that metric would turn out differently from sample to sample.
- This sampling distribution can be estimated via the bootstrap, or via formulas that rely on the central limit theorem.
  - **Central Limit Theorem** is the tendency of the sampling distribution to take on a normal shape as sample size rises.
  - It says that the means drawn from multiple samples will resemble the familiar bell-shaped normal curve, even if the source population is not normally distributed, provided that the sample size is large enough and the departure of the data from normality is not too great.
  - The central limit theorem allows normal-approximation formulas like the t-distribution to be used in calculating sampling distributions for inference — that is, confidence intervals and hypothesis tests.
- A key metric that sums up the variability of a sample statistic is its *standard error*.
  - The standard error can be estimated using a statistic based on the standard deviation s of the sample values, and the sample size n: `SE = s / \sqrt{n}`.
  - As the sample size increases, the standard error decreases.

[back to current section](#data-and-sampling-distributions)

### The Bootstrap

One easy and effective way to estimate the sampling distribution of a statistic, or of model parameters, is to draw additional samples, with replacement, from the sample itself and recalculate the statistic or model for each resample. This procedure is called the bootstrap, and it does not necessarily involve any assumptions about the data or the sample statistic being normally distributed.

Conceptually, you can imagine the bootstrap as replicating the original sample thousands or millions of times so that you have a hypothetical population that embodies all the knowledge from your original sample (it’s just larger). You can then draw samples from this hypothetical population for the purpose of estimating a sampling distribution. See figure below.

![Figure 2-7](psds_0207.png)

In practice, it is not necessary to actually replicate the sample a huge number of times. We simply replace each observation after each draw; that is, we sample with replacement. In this way we effectively create an infinite population in which the probability of an element being drawn remains unchanged from draw to draw.

The number of iterations of the bootstrap is set somewhat arbitrarily. The more iterations you do, the more accurate the estimate of the standard error, or the confidence interval. The result from this procedure is a bootstrap set of sample statistics or estimated model parameters, which you can then examine to see how variable they are.

The bootstrap can be used with multivariate data, where the rows are sampled as units (see Figure below). A model might then be run on the bootstrapped data, for example, to estimate the stability (variability) of model parameters, or to improve predictive power. With classification and regression trees (also called decision trees), running multiple trees on bootstrap samples and then averaging their predictions (or, with classification, taking a majority vote) generally performs better than using a single tree. This process is called bagging.

![Figure 2-8](psds_0208.png)

[back to current section](#data-and-sampling-distributions)

### Confidence Intervals

- **Confidence intervals** are the typical way to present estimates as an interval range.
- The more data you have, the less variable a sample estimate will be.
  - Confidence intervals always come with a coverage level, expressed as a (high) percentage, say 90% or 95%.
  - One way to think of a 90% confidence interval is as follows: it is the interval that encloses the central 90% of the bootstrap sampling distribution of a sample statistic.
  - The higher the level of confidence, the wider the interval. Also, the smaller the sample, the wider the interval (i.e., the more uncertainty). Both make sense: the more confident you want to be, and the less data you have, the wider you must make the confidence interval to be sufficiently assured of capturing the true value.
- The bootstrap is an effective way to construct confidence intervals.

[back to current section](#data-and-sampling-distributions)

### Normal Distribution

- The normal distribution was essential to the historical developments of statistics, as it permitted mathematical approximation of uncertainty and variability.
  - In a normal distribution, 68% of the data lies within one standard deviation of the mean, and 95% lies within two standard deviations.
  - While raw data is typically not normally distributed, errors often are, as are averages and totals in large samples.
  - To convert data to *z-scores*, you subtract the mean of the data and divide by the standard deviation; you can then compare the data to a normal distribution.

[back to current section](#data-and-sampling-distributions)

### Long Tailed Distribution

- While the normal distribution is often appropriate and useful with respect to the distribution of errors and sample statistics, it typically does not characterize the distribution of raw data.
- Sometimes, the distribution is highly skewed (asymmetric), such as with income data, or the distribution can be discrete, as with binomial data.
- Both symmetric and asymmetric distributions may have long tails. The tails of a distribution correspond to the extreme values (small and large). Long tails, and guarding against them, are widely recognized in practical work.

[back to current section](#data-and-sampling-distributions)

### Student t-Distribution

- The t-distribution is a normally shaped distribution, but a bit thicker and longer on the tails. It is used extensively in depicting distributions of sample statistics.
- Distributions of sample means are typically shaped like a t-distribution, and there is a family of t-distributions that differ depending on how large the sample is. The larger the sample, the more normally shaped the t-distribution becomes.
- The t-distribution has been used as a reference for the distribution of a sample mean, the difference between two sample means, regression parameters, and other statistics.

[back to current section](#data-and-sampling-distributions)

### Binomial Distribution

- Binomial outcomes are important to model, since they represent, among other things, fundamental decisions (buy or don't buy, click or don't click, survive or die, etc.)
- The binomial distribution is the frequency distribution of the number of successes (x) in a given number of trials (n) with specified probability (p) of success in each trial.
  -  There are 2 possible outcomes: one with probability p and the other with probability 1 - p.
  - Mean: `n * p`
  - Variance: `n * p(1 - p)`
- With large n, and provided p is not too close to 0 or 1, the binomial distribution can be approximated by the normal distribution.

[back to current section](#data-and-sampling-distributions)

### Poisson and Related Distributions

- For events that occur at a constant rate, the number of events per unit of time or space can be modeled as a Poisson distribution.
- In this scenario, you can also model the time or distance between one event and the next as an exponential distribution.
- A changing event rate over time (e.g., an increasing probability of device failure) can be modeled with the Weibull distribution.

[back to current section](#data-and-sampling-distributions)

[back to top](#practical-statistics-for-data-scientists)

## Statistical Experiments and Significance Testing

Design of experiments is a cornerstone of the practice of statistics, with applications in virtually all areas of research. The goal is to design an experiment in order to confirm or reject a hypothesis. Data scientists are faced with the need to conduct continual experiments, particularly regarding user interface and product marketing. This chapter reviews traditional experimental design and discusses some common challenges in data science. It also covers some oft-cited concepts in statistical inference and explains their meaning and relevance (or lack of relevance) to data science.

Whenever you see references to statistical significance, t-tests, or p-values, it is typically in the context of the classical statistical inference “pipeline” (see Figure below). This process starts with a hypothesis (“drug A is better than the existing standard drug,” “price A is more profitable than the existing price B”). An experiment (it might be an A/B test) is designed to test the hypothesis—designed in such a way that, hopefully, will deliver conclusive results. The data is collected and analyzed, and then a conclusion is drawn. The term *inference* reflects the intention to apply the experiment results, which involve a limited set of data, to a larger process or population.

![Figure 3-1](psds_03in01.png)

Here are the sections:

* [AB Testing](#ab-testing)
* [Hypothesis Test](#hypothesis-test)
* [Resampling](#resampling)
* [Statistical Significance and P-Values](#statistical-significance-and-p-values)
* [t-Tests](#t-tests)
* [Multiple Testing](#multiple-testing)
* [Degrees of Freedom](#degrees-of-freedom)
* [ANOVA](#ANOVA)
* [Chi-Square Test](#chi-square-test)
* [Multi-Arm Bandit Algorithm](#multi-arm-bandit-algorithm)
* [Power and Sample Size](#power-and-sample-size)

### AB Testing

- An A/B test is an experiment with two groups to establish which of two treatments, products, procedures, or the like is superior.
  - *Treatment group* is the group of subjects exposed to a specific treatment.
  - *Control group* is the group of subjects exposed to no (or standard) treatment.
- A proper A/B test has subjects that can be assigned to one treatment or another. Ideally, subjects are randomized to treatments.
  - You need to pay attention to the *test statistic* - the metric used to measure the effect of the treatment. Most common is a binary variable: click or no click, buy or don't buy, fraud or no fraud, and so on.
- Without a control group, there is no assurance that "other things are equal" and that any difference is really due to the treatment.

[back to current section](#statistical-experiments-and-significance-testing)

### Hypothesis Test

- A *null hypothesis* is a logical construct embodying the notion that nothing special has happened, and any effect you observe is due to random chance.
  - Our hope is that we can, in fact, prove the null hypothesis wrong, and show that the outcomes for groups A and B are more different than what chance might produce.
- The *hypothesis test* assumes that the null hypothesis is true, creates a "null model" (a probability model), and tests whether the effect you observe is a reasonable outcome of that model.

[back to current section](#statistical-experiments-and-significance-testing)

### Resampling

- A *resampling* in statistics means to repeatedly sample values from observed data, with a general goal of assessing random variability in a statistic. It can also be used to assess and improve the accuracy of some machine learning models (i.e., bagging).
- There are two main types of resampling procedures: the bootstrap and permutation tests. The bootstrap is used to assess the reliability of an estimate. Permutation tests are used to test hypotheses, typically involving two or more groups.
- In a permutation procedure, two or more samples are involved, typically the groups in an A/B or other hypothesis test. Permute means to change the order of a set of values. The first step in a permutation test of a hypothesis is to combine the results from groups A and B (and, if used, C, D, ...) together. This is the logical embodiment of the null hypothesis that the treatments to which the groups were exposed do not differ.
- We then test that hypothesis by randomly drawing groups from this combined set, and seeing how much they differ from one another.
- The permutation procedure is as follows:
  1. Combine the results from the different groups in a single data set.
  2. Shuffle the combined data, then randomly draw (without replacing) a resample of the same size as group A.
  3. From the remaining data, randomly draw (without replacing) a resample of the same size as group B.
  4. Do the same for groups C, D, and so on.
  5. Whatever statistic or estimate was calculated for the original samples (e.g., difference in group proportions), calculate it now for the resamples, and record. This constitutes one permutation iteration.
  6. Repeat the previous steps R times to yield a permutation distribution of the test statistic.
- Now go back to the observed difference between groups and compare it to the set of permuted differences.
  - If the observed difference lies well within the set of permuted differences, then we have not proven anything - the observed difference is within the range of what chance might produce.
  - However, the observed difference lies outside most of the permutation distribution, then we conclude that chance is not responsible. In technical terms, the difference is *statistically significant*.

[back to current section](#statistical-experiments-and-significance-testing)

### Statistical Significance and P-Values

- Significance tests are used to determine whether an observed effect is within the range of chance variation for a null hypothesis model.
- The *p-value* is the probability that results as extreme as the observed results might occur, given a null hypothesis model.
  -  We can estimate a p-value from our permutation test by taking the proportion of times that the permutation test produces a difference equal to or greater than the observed difference.
- The *alpha* value is the threshold of "unusualness" in a null hypothesis chance model. Typical alpha levels are 5% and 1%.
- In assessing statistical significance, two types of error are possible:
  - **Type 1 error**: Mistakenly concluding an effect is real (when it is due to chance).
  - **Type 2 error**: Mistakenly concluding an effect is due to chance (when it is real).
- For a data scientist, a p-value is a useful metric in situations where you want to know whether a model result that appears interesting and useful is within the range of normal chance variability.
  - For example, p-values are sometimes used as intermediate inputs in some statistical or machine learning models - a feature might be included in or excluded from a model depending on its p-value.

[back to current section](#statistical-experiments-and-significance-testing)

### t-Tests

- The **t-test** provides insight into whether the difference between the means of two groups is due to chance or is reliable.
- t-test can be used when evaluating the results of an A/B test: "Would the difference between the control group and the treatment group be the same in a new sample from the same population?"
- The results of a t-test are evaluated through the ratio of the difference between the groups and the difference within the groups.
  - This ratio is known as the *t-statistic*; the t-statistic has a corresponding *p-value*, which represents the probability that what is observed could be produced by random data.
  - The lower the p-value, the more confident we can be that the difference is not produced by chance and is indeed a reliable difference between the means of the two groups.
  - In research, a p-value of 0.05 or less is generally considered reliable (statistically significant), but in a more entrepreneurial setting you may decide that a higher p-value is acceptable.
  - P-values correspond to t-statistics based on the size of the samples: The larger the sample size (more degrees of freedom), the lower the p-value for the same t-statistic (ratio of differences).

[back to current section](#statistical-experiments-and-significance-testing)

### Multiple Testing

- The more variables you add, or the more models you run, the greater the probability that something will emerge as “significant” just by chance.
- Multiplicity in a research study or data mining project (multiple comparisons, many variables, many models, etc.) increases the risk of concluding that something is significant just by chance.
- The bottom line for data scientists on multiplicity is:
  - For predictive modeling, the risk of getting an illusory model whose apparent efficacy is largely a product of random chance is mitigated by cross-validation, and use of a holdout sample.
  - For other procedures without a labeled holdout set to check the model, you must rely on: (1) Awareness that the more you query and manipulate the data, the greater the role that chance might play; and (2) Resampling and simulation heuristics to provide random chance benchmarks against which observed results can be compared.

[back to current section](#statistical-experiments-and-significance-testing)

### Degrees of Freedom

- The number of degrees of freedom forms part of the calculation to standardize test statistics so they can be compared to reference distribution.
- The concept of degrees of freedom lies behind the factoring of categorical variables into n - 1 indicator or dummy variables when doing a regression (to avoid multicollinearity).
  - When you use a sample to estimate the variance for a population, you will end up with an estimate that is slightly biased downward if you use n in the denominator. If you use n – 1 in the denominator, the estimate will be free of that bias.

[back to current section](#statistical-experiments-and-significance-testing)

### ANOVA

- ANOVA is a statistical procedure for analyzing the results of an experiment with multiple groups.
- It is the extension of similar procedures for the A/B test, used to assess whether the overall variation among groups is within the range of chance variation.
- A useful outcome of an ANOVA is the identification of variance components associated with group treatments, interaction effects, and errors.
- The basics for it can be seen in the following resampling procedure (specified here for the A-B-C-D test of web page stickiness):
  1. Combine all the data together in a single box.
  2. Shuffle and draw out four resamples of five values each.
  3. Record the mean of each of the four groups.
  4. Record the variance among the four group means.
  5. Repeat steps 2-4 many times (say 1,000).
- What proportion of the time did the resampled variance exceed the observed variance? This is the p-value.
- There is a statistical test for ANOVA based on the *F-statistic*.
  - The F-statistic is based on the ratio of the variance across group means (i.e., the treatment effect) to the variance due to residual error.
  - The higher this ratio, the more statistically significant the result.

[back to current section](#statistical-experiments-and-significance-testing)

### Chi-Square Test

- There are two types of **Chi-Square Tests**:
  1. The *goodness of fit* test (does a coin tossed 20 times turn up 10 heads and 10 tails?)
  2. The *test of independence* (is there a relationship between gender and salary?)
- We have some outcomes, and a variable that we think might have an effect.
  - We look at *observed* values of the outcome, with and without our variable of interest.
  - We then *calculate* the expected values.
  - From that, we calculate the deviations from what we observed.
  - We scale the deviations based on the expected values, and adjust for number of sets of samples.
  - The *chi-square statistic* is one measure of that deviation (whatever we are observing, is it random or is it unlikely to be random?)
- Statisticians (using probability and combinatorics) have already calculated a look-up table, called the chi-squared table.
  - Given a certain observed deviation, that table tells us what is the probability that this deviation is due to chance.
  - If that probability is really tiny, then we say “Hey, that can’t be due to chance. There must be some sort of an effect.”
  - If the p-value is big, we say “This could be purely due to chance. No need to get excited about this.”
  - That in a nutshell is how Chi-square works: It is a measure of deviation, compared against pre-computed values that tells us how probable these deviations are.
- Chi-square tests, or similar resampling simulations, are used in data science applications more as a filter to determine whether an effect or feature is worthy of further consideration than as a formal test of significance.
- They can also be used in automated feature selection in machine learning, to assess class prevalence across features and identify features whether the prevalence of a certain class is unusually high or low, in a way that is not compatible with random variation.

[back to current section](#statistical-experiments-and-significance-testing)

### Multi-Arm Bandit Algorithm

Multi-arm bandits offer an approach to testing, especially web testing, that allows explicit optimization and more rapid decision making than the traditional statistical approach to designing experiments.

**How it works**

Your goal is to win as much money as possible, and more specifically, to identify and settle on the winning arm sooner rather than later. The challenge is that you don’t know at what rate the arms pay out — you only know the results of pulling the arm. Suppose each “win” is for the same amount, no matter which arm. What differs is the probability of a win. Suppose further that you initially try each arm 50 times and get the following results:

* **Arm A**: 10 wins out of 50
* **Arm B**: 2 win out of 50
* **Arm C**: 4 wins out of 50

We start pulling A more often, to take advantage of its apparent superiority, but we don’t abandon B and C. We just pull them less often. If A continues to outperform, we continue to shift resources (pulls) away from B and C and pull A more often. If, on the other hand, C starts to do better, and A starts to do worse, we can shift pulls from A back to C. If one of them turns out to be superior to A and this was hidden in the initial trial due to chance, it now has an opportunity to emerge with further testing.

A more sophisticated algorithm uses “**Thompson’s sampling.**” This procedure “samples” (pulls a bandit arm) at each stage to maximize the probability of choosing the best arm. Of course you don’t know which is the best arm — that’s the whole problem! — but as you observe the payoff with each successive draw, you gain more information. Thompson’s sampling uses a Bayesian approach: some prior distribution of rewards is assumed initially, using what is called a beta distribution (this is a common mechanism for specifying prior information in a Bayesian problem). As information accumulates from each draw, this information can be updated, allowing the selection of the next draw to be better optimized as far as choosing the right arm.

[back to current section](#statistical-experiments-and-significance-testing)

### Power and Sample Size

- Finding out how big a sample size you need requires thinking ahead to the statistical test you plan to conduct.
- You must specify the minimum size of the effect that you want to detect.
- You must also specify the required probability of detecting that effect size (power).
- Finally, you must specify  the significance level (alpha) at which the test will be conducted.

[back to current section](#statistical-experiments-and-significance-testing)

[back to top](#practical-statistics-for-data-scientists)
