# Limits

A good way to learn is to practice. Understanding the statistics involved in **Data Analysis and Econometrics** is vital for learning. Hence, I created a statistics calculator add-on that allows economists and data analysts to carry out statistical analysis on google sheets. Right now the addon can do things a simple a **mean, median mode,** to more complex operations like multiple **linear regression.**

The Inspiration for this project was to recreate a desktop application called **EViews**. 

**EViews** is a statistical package for Windows, used mainly for time-series oriented econometric analysis. It is developed by Quantitative Micro Software, now a part of IHS.

## What can it do?
For now,
 1. it can calculate the summary of your data with the Descriptive statistics functions such as:
	 - Mean 
	 - Sum 
	 - Minimum 
	 - Maximum 
	 - Observation 
	 - Median 
	 - Standard Deviation 
	 - Skewness 
	 - Kurtosis 
	 - Sum of Squares 
	 - Jarque -Bera

 2. It can also find the correlation between multiple variables. That is 
	 -  Multiple Correlation

 3. It can also calculate linear multiple regression.
	 - Multiple Regression

***To see the implementation, check out this [Google sheet](https://docs.google.com/spreadsheets/d/1Jeb0HK7usLIUjxXinogwNm6lENWkpIEqeCJ1pROOyYk/edit?usp=copy).***

# Guide For Using Limits

## Setup
There are 2 ways to set up a limit on a sheet.
1. Make a copy of this [Google sheet](https://docs.google.com/spreadsheets/d/1Jeb0HK7usLIUjxXinogwNm6lENWkpIEqeCJ1pROOyYk/edit?usp=copy). When that is done, the sheet would contain all the functions stated above.
2. Go to [GitHub](https://github.com/Hemephelus/Data-Analyst/tree/main/Data%20Analysis%20Projects/Limits), make a copy of the code, create a new google sheet, go-to apps scripts and paste the code there. After that,  save and run the code. **This would be done only once**, after that, the sheet would contain all the functions stated above.


```mermaid
graph LR
A[GitHub]  --> B[Copy Code]
B  --> C[Create a New Google Sheet]
C --> D[Go to Apps Scripts]
D --> E[Paste Code]
E --> F[Save and Run The Code]
```
## How it works	
Like every other function in google sheets, you can write the same functions in a cell by starting with an "=" sign and the function name.


Example: Multiple Regression

    =MULTREG('Data Set'!B3:G42,1)
	 //Returns the coefficients of all the independent vairables
    =MULTREG(Array,  Depdt_Var_Col_Num)

**Array**
	    The range of cells to calculate.
    **Depdt_Var_Col_Num**
	    The value or cell would be the dependent variable.

# Explanation of Each Function.
In this explanation, I would be making use of a data set I made to find if there is any relationship between **Oil Price and Military Expenditure** from **1981 to 2020**. I used 4 control variables as **Inflation, Real Gross Domestic Product, Budget Surplus/Deficit and Public Debt.**

### Schema of Data Set
|Field Name | Type|
|--|--|
| Year| Date |
| Military  Expenditure (ME)| Integer|
| Inflation (INF)| Integer|
| Real Gross Domestic Product (RGDP)| Integer|
| Budget Surplus/Deficit (BSD)| Integer|
| Public Debt (PD)| Integer|
| Oil Price (OP)| Integer|

### Data Set Table

> Part of the table can be seen below.

| Year | ME     | INF         | RGDP         | BDS       | PD    | OP    |
| ---- | ------ | ----------- | ------------ | --------- | ----- | ----- |
| 1981 | 1.3191 | 20.81282291 | 130707610046 | 4977.0979 | 13.52 | 56.17 |
| 1982 | 1.1125 | 7.697747247 | 121815063124 | 4974.8959 | 23.83 | 52.75 |
| 1983 | 1.1789 | 23.21233155 | 108507882040 | 4977.6355 | 32.8  | 48.37 |
| 1984 | 0.9282 | 17.82053329 | 107297342914 | 4978.3396 | 40.48 | 47.75 |
| 1985 | 0.9757 | 7.435344828 | 113641864269 | 4977.9603 | 45.25 | 45.79 |
| 1986 | 0.9069 | 5.717151454 | 113711123611 | 4972.7457 | 69.89 | 21.52 |


1. **Descriptive statistics**
	This function combines the 11 functions below into one function and returns the required values. Using the Descriptive statistics function represent as "StatsSummary()" in the code, we can the 11 functions for each of the 6 variables with a single function.
```SQL
=StatsSummary('Data Set'!B2:G42,1)
//returns the table below
```
| Title              | ME           | INF        | RGDP                  | BDS            | PD              | OP          |
| ------------------ | ------------ | ---------- | --------------------- | -------------- | --------------- | ----------- |
| Mean               | 166.6734     | 18.9990    | 246126665574.0250     | 4243.1344      | 5281.6735       | 47.7828     |
| Sum                | 6666.9345    | 759.9620   | 9845066622961.0000    | 169725.3755    | 211266.9400     | 1911.3100   |
| Minimum            | 0.8100       | 5.3880     | 107297342914.0000     | 1.0000         | 13.5200         | 15.4800     |
| Maximum            | 974.9100     | 72.8355    | 477161826016.0000     | 5013.0494      | 32915.0000      | 101.6300    |
| Observation        | 40           | 40         | 40                    | 40             | 40              | 40          |
| Median             | 54.4360      | 12.7158    | 173293887708.0000     | 4870.4928      | 2726.0450       | 45.4200     |
| Standard Deviation | 232.6917     | 16.8684    | 132086333694.5565     | 1335.1584      | 7329.8096       | 26.1796     |
| Skewness           | 232.6917     | 16.8684    | 132086333694.5565     | 1335.1584      | 7329.8096       | 26.1796     |
| Kurtosis           | 2.7502       | 2.6218     | \-1.1906              | 4.1544         | 4.9495          | \-0.6281    |
| Sum of Squares     | 3222872.5409 | 25535.7829 | 3.103558602669437e+24 | 789690849.5487 | 3211161228.9780 | 118057.1113 |
| JarqueBera         | 19.3913      | 24.1864    | 32.1817               | 35.3009        | 37.8689         | 24.9509     |

2. **Multiple Correlation**
		This function finds the relationship between two variables. we use the Pearson correlation coefficient formula to make this function. 
![r =\frac{\sum\left(x_{i}-\bar{x}\right)\left(y_{i}-\bar{y}\right)}{\sqrt{\sum\left(x_{i}-\bar{x}\right)^{2} \sum\left(y_{i}-\bar{y}\right)^{2}}}](https://www.gstatic.com/education/formulas2/397133473/en/correlation_coefficient_formula.svg)

![r](https://www.gstatic.com/education/formulas2/397133473/en/correlation_coefficient_formula_correlation_coefficient_formula_var_1.svg)  = correlation coefficient
![x_{i}](https://www.gstatic.com/education/formulas2/397133473/en/correlation_coefficient_formula_correlation_coefficient_formula_var_2.svg) = values of the x-variable in a sample
![\bar{x}](https://www.gstatic.com/education/formulas2/397133473/en/correlation_coefficient_formula_correlation_coefficient_formula_var_3.svg) = mean of the values of the x-variable
![y_{i}](https://www.gstatic.com/education/formulas2/397133473/en/correlation_coefficient_formula_correlation_coefficient_formula_var_4.svg) = values of the y-variable in a sample
![\bar{y}](https://www.gstatic.com/education/formulas2/397133473/en/correlation_coefficient_formula_correlation_coefficient_formula_var_5.svg) = mean of the values of the y-variable
This formula is run on all two pair combinations of the 6 variables.
```SQL
=MultipleCorrelation('Data Set'!B3:G42)
//returns the table below
```
| Titles | ME             | INF            | RGDP           | BDS            | PD             | OPV            |
| ------ | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| ME     | 1              | \-0.2877641244 | 0.9132564905   | \-0.9393273271 | 0.9597081789   | 0.5164875695   |
| INF    | \-0.2877641244 | 1              | \-0.3468104851 | 0.2045494194   | \-0.2428219981 | \-0.4535691727 |
| RGDP   | 0.9132564905   | \-0.3468104851 | 1              | \-0.7975515379 | 0.8257790733   | 0.6906221997   |
| BDS    | \-0.9393273271 | 0.2045494194   | \-0.7975515379 | 1              | \-0.9658078392 | \-0.3004479417 |
| PD     | 0.9597081789   | \-0.2428219981 | 0.8257790733   | \-0.9658078392 | 1              | 0.3243313049   |
| OP     | 0.5164875695   | \-0.4535691727 | 0.6906221997   | \-0.3004479417 | 0.3243313049   | 1              |

From the table above, we can see that there is a positive but weak relationship between Oil Price and Military Expenditure. On the other hand, there is a positive and strong relationship between  Military Expenditure and Public Debt. 

The highest correlated pair is  Public Debt and Budget Surplus/Deficit. This makes sense as Public Debt is a function of Budget Surplus/Deficit.

3. **Multiple Regression**

This function finds the **coefficient **of the independent variables that would be used to estimate/predict  Military Expenditure on a linear scale. 
 
Ideally, we should log these variables to account for variables that are either too big or too small.


$$
\Beta = (X'X)^{-1}X'Y\,.
$$

**B** = coefficients of each variable

That is, we first need to find the minor product moment of **X**, which is **X′X**. Next, we find the inverse of **X′X** and post multiply this inverse by **X′Y**.

```SQL
=MULTREG('Data Set'!B3:G42,1)

//The results can be represented as an equation
ME = 48.1728*CONSTANT + 0.0607*INF + 0.0001*RGDP + -0.0022*BDS + -0.0025*PD + -0.4175*OPV

//returns the table below
```

| VARIABLES | COEFFICIENTS |
| --------- | ------------ |
| CONSTANT  | 48.1728      |
| INF       | 0.0607       |
| RGDP      | 0.0001       |
| BDS       | \-0.0022     |
| PD        | \-0.0025     |
| OP        | \-0.4175     |



From the table above, we can see that a unit increase in Oil price would lead to a -0.4174 change in Military Expenditure.

## Conclusion
What makes the data set interesting is the fact that when we looked at the correlation between Oil Price and Military Expenditure we saw a weak positive relationship, but the regression line shows a negative coefficient implying a negative relationship. These insights show that there should be more exploration as to why the discrepancies exist.
