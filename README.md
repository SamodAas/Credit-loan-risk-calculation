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

### Data and its cleaning

* There are 5442 observations and 16 features containing information about the credit history of the borrower as well as the information about the loan itself.  
* There are also 5212 empty cells. When an observation doesn't have mortgage value then it is dropped, otherwise, other empty cells get median or mean values depending which is lower (in every case the difference is negligible).  
* JOB column gets 6 dummy variables.  
