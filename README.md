# Building an Accounting Fraud Classification Model

## Abstract

[Slides](https://docs.google.com/presentation/d/1zLSNhcjEG1QAUX_T6kX5mTN187Hze6NA68W-U2k29aw/edit#slide=id.g4b294b7a6a_0_6)

I built a Machine Learning model to detect accounting fraud. My model achieved its best metrics with a Gradient Boosting Classifier: .99 AUC; .85 F1 Score; .91 Cross Validation; and .96 Accuracy.

## Motivation

On both a federal and international level, we spend a lot of money on [compliance costs,](https://www.investopedia.com/terms/c/compliance-cost.asp) including adherence to anti-fraud regulation, such as the [Sarbanes-Oxley Act of 2002](https://www.thebalance.com/sarbanes-oxley-act-of-2002-3306254). Despite all the regulation put in place to disincentivize fraud, companies and executives continue to commit accounting fraud. I wanted to introduce machine learning to this continuing issue as a first measure to catch potential fraud and also possibly deter it.


## Research

First, I needed to find the companies that had actually committed fraud. I did this by combing through the Securities and Exchange Commission's (SEC) [Press Releases](https://www.sec.gov/news/pressreleases) for the last 5 years to gather a list of 25 companies that had been accused of fraud by the SEC. There, I had access to the SEC orders which specified which financial statements were deemed fraudulent, when they had previously been filed, and the companies' CIK numbers (a unique identifier assigned each corporation).

## Dataset

Then, I downloaded the [Financial Statement Data Sets](https://www.sec.gov/dera/data/financial-statement-data-sets.html) containing the above mentioned fraudulent filings as well as some non-fraudulent filings.

<p align="center">
<img width="1000" alt="dataset" src="https://github.com/Erika-Russi/accounting_fraud_detect/blob/master/images/pandas.png">


## Feature Engineering

1. Once I had my datasets, I added [Benford's Law](https://medium.com/@erika.russi/benny-and-the-di-gits-e6bb9f40c552) as my first feature. Benford's Law is the "Mathematical theory of leading digits. Specifically, in data sets, the leading digit(s) is (are) distributed in a specific, nonuniform way." If a company had committed fraud, then the counts of leading digits from their financial statements should stray from the theoretical numbers, and when graphing the numbers, it appeared to be the case:

<p align="center">
<img width="1000" alt="Benford's Law" src="https://github.com/Erika-Russi/accounting_fraud_detect/blob/master/images/benford_frauds.png">
    
I used the [Kullback–Leibler divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence) as a measurement of how much a company's filing actually strayed from Benford's Law.

2. The next features I wanted to include were tags used within the financial statements. I bucketed common tags/account names listed on financial statements using repeating patterns. For instance, if the phrase "Accounts Receivable" occured in the Balance Sheet, it should be tagged as such even if it read "Trade accounts receivable, net". I found common tags across three financial statements: Balance Sheet, Income Statement, and Statement of Cash flows

<p align="center">
<img width="1000" alt="Fin Statement" src="https://github.com/Erika-Russi/accounting_fraud_detect/blob/master/images/fin_statement.png">


3. Next, I added financial ratios typically used by forensic accountants to detect fraud.
<p align="center">
<img width="1000" alt="Finratios" src="https://github.com/Erika-Russi/accounting_fraud_detect/blob/master/images/finratios.png">







