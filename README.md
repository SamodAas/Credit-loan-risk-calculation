This project calculates the capital requirement for given mortgage loans by a bank according to both the standard approach and F-IRB approach established by the Basel committee.

[Link](https://docs.google.com/spreadsheets/d/1ab1TLiSjM7uA31HGqcP_-YkW5MMo4hCveACZfAOwfos/edit?usp=sharing)

## Standard approach

The standard approach is calculated simply by checking the loan to value (LTV) ratio and giving an according risk weight, with which the capital requirement is calculated.

## F-IRB approach

This approach involves using formula for mortgage exposure made by the Basel committee. The most important part of the formula is probability of default (PD) which is calculated using the forecast of logistic regression.  

## Conclusion

As F-IRB is better at managing the risk which is brought by cyclic nature of economy, in this particular case where the percentage of defaulted loans (~19%) is so high, the F-IRB approach to calculating risk and the following capital requirement shows that capital requirement is much higher than the one calculated using the standard approach.  
It could further be adjusted by changing the parameters of the logistic regression


## Logistic regression

### Data, cleaning, and preparing

* There are 5442 observations and 16 features containing information about the credit history of the borrower as well as the information about the loan itself.  
* There are also 5212 empty cells. When an observation doesn't have mortgage value then it is dropped, otherwise, other empty cells get median or mean values depending which is lower (in every case the difference is negligible).  
* JOB column gets 6 dummy variables.  
* Few of the extreme outliers are dropped.
* All of the columns get scaled using *MinMaxScaler* to values ranging from 0 to 1.
* DEROG and DELINQ columns get maximum value for all observations having values above that particular value. As the complete majority of the values in these two features are less then 4 and 5 accordingly, any values above that get values 4 for DEROG and 5 for DELINQ. This is done to minimize the effect of those few outliers, especially considering that these features get scaled afterwards.
* Similar to DEROG and DELINQ, DEBTINC gets value 100 if its original value is 100 and above.

### Model building

Because the dataset does not contain many positive (defaulted) observations, resampling function is used (SMOTE).  
Further, forward and backward stepwise resgression model selection is used.

### Model evaluation

Coefficients:  
const          -1.2264     
DELINQ          3.7080      
DEROG           0.7345      
NINQ            1.4585      
CLAGE          -4.6598     
DEBTINC         6.1082      
JOB_Office     -0.5189      
JOB_Sales       1.1965      
YOJ            -0.4465      
VALUE          -1.8367        
JOB_ProfExe     0.0661       
JOB_Self        0.5804  

Odd ratios:  
const            0.338274  
DELINQ          43.616474  
DEROG            2.170131  
NINQ             4.069364  
CLAGE            0.012491  
DEBTINC        235.476192  
JOB_Office       0.566841  
JOB_Sales        2.731567  
YOJ              0.646138  
VALUE            0.200962  
JOB_ProfExe      0.963847  
JOB_Self         1.428451  

Metrics:
AUC_ROC score:  0.7244596920188633  
Accuracy:  0.7628676470588235  
Recall score:  0.6633663366336634  

Confusion Matrix:   
![image](https://github.com/SamodAas/Credit-loan-risk-calculation/assets/55328989/8ff52b40-2b63-473e-a8e3-6789109bdcb3)


