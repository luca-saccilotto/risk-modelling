# Finance & Risk - Risk Modelling & Analytics

The calculation of credit risk is a crucial process that involves evaluating the probability of a borrower being unable to fulfill their debt obligations. This assessment plays a vital role for financial institutions and lenders, enabling them to make informed decisions regarding the creditworthiness of individuals, companies, or other entities seeking credit.

## Definition
The _Expected Loss_ (EL) is the amount that the firm loses as a result of the default on a loan. EL is the overall estimation of the potential loss that a lender may face from a borrower, combining the following three components:

1. _Probability of Default_ (PD) - PD measures the likelihood of a borrower defaulting on their debt within a specific time frame, usually expressed as a percentage.

2. _Loss Given Default_ (LGD) - LGD represents the proportion of the outstanding debt that the lender is likely to lose in the event of default.

3. _Exposure at Default_ (EAD) - EAD represents the amount of exposure or outstanding debt the lender faces at the time of default.

## Objectives
The primary objective of this project is to create a predictive model that can estimate the probability of default on specific financial obligations, such as credit cards or mortgages. By accurately forecasting the likelihood of default, the project aims to provide valuable insights that can inform the development of strategies to mitigate risk and preserve clients' financial stability.

## Approach
The model construction process involves several key steps. Firstly, data preparation and pre-processing are carried out to ensure the data is clean, formatted correctly, and ready for analysis. Secondly, feature engineering and selection techniques are applied to extract relevant information and identify the most predictive features. Lastly, the model is developed using suitable algorithms and evaluated to assess its performance.

## About Data
The data contains application and behavioural information about individuals, including their age, income, loan details, and credit history. It provides insights into the relationship between these variables and loan outcomes, such as loan status and default rates.

| Variable                     | Description                                                          |
|------------------------------|----------------------------------------------------------------------|
| *person_age*                 | Age of the person                                                    |
| *person_income*              | Income of the person in dollars                                      |
| *person_home_ownership*      | Home ownership status                                                |
| *person_emp_length*          | Employment length                                                    |
| *loan_intent*                | Intention of the loan                                                |
| *loan_grade*                 | Grade assigned to the loan                                           |
| *loan_amnt*                  | Loan amount in dollars                                               |
| *loan_int_rate*              | Interest rate on the loan                                            |
| *loan_status*                | Status of the loan with one being default and zero being non-default |
| *loan_percent_income*        | Loan amount as a percentage of income                                |
| *cb_person_default_on_file*  | Historical default on file                                           |
| *cb_person_cred_hist_length* | Length of credit history                                             |

_Source:_ https://app.datacamp.com/workspace/sample-datasets.

## Exploring Data
In this section, the focus is on checking the structure of the data as well as visualizing what is inside it. This process not only helps identifying any patterns or trends, but also enables us to spot the presence of anomalies that may require further investigation.

The following picture depicts the distribution of loan amounts, providing a visual representation of the spread of loan values. In addition, it offers useful insights into the range and frequency of different loan amounts within the dataset.

<div align = "center">
  <img src = "https://github.com/luca-saccilotto/credit-risk-modelling/blob/main/charts/histogram-loan_amnt.png" alt = "Alt Text" width = "50%">
</div>

Based on the data, the boxplot below suggests that the average percentage of income for defaults is comparatively higher. This could indicate that those recipients have a debt-to-income ratio that is already too high.

<div align = "center">
  <img src = "https://github.com/luca-saccilotto/credit-risk-modelling/blob/main/charts/boxplot-loan_percent_income.png" alt = "Alt Text" width = "50%">
</div>

Finally, notice that the following plot shows a different color depending on the status of loan. In this case, it is loan default in red and non-default in blue, and it looks like there are more defaults with high interest rates. Additionally, it is worth noting the presence of outliers.

<div align = "center">
  <img src = "https://github.com/luca-saccilotto/credit-risk-modelling/blob/main/charts/scatter-person_age.png" alt = "Alt Text" width = "50%">
</div>

## Processing Data
In this section, the focus is on the process of data preparation. Properly preparing the data is crucial because it reduces the training time of models and ensures that our models can accurately predict defaults.

The first type of preparation is outlier detection and removal. As seen in the chart before, it is not uncommon for data entry errors or technical issues to introduce outliers into the data. With outliers in our training set, predictive models will have a difficult time estimating parameters like coefficients. This can cause models to not predict as many defaults.

One effective method for identifying outliers is through the use of visualizations such as histograms, scatter plots, or cross tables. During the analysis, several records with unrealistic values for a person's age and employment length were discovered. Since such values are not possible, it has been decided to remove these observations from our data.

In addition, handling missing data is another essential aspect of data preparation. Three options are available: retaining, replacing, or removing missing data. In the case of `person_emp_length`, values were replaced using the `median()` function. On the other hand, the presence of missing data in `loan_int_rate` is unusual and could be a result of data ingestion errors. That is why it has been chosen to drop these records before proceeding.

Having processed the missing values and outliers, the data is now ready for modeling. While financial information is generally well-organized, it is always a good practice to prepare the data for analytical work.

## Building Models
The expected loss is driven mainly by borrower-specific factors and factors of the economic environment.