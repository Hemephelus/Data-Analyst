# Mr. Macaroni

This is a passion project that I use to demonstrate my skills of data analysis, and my thought process when it comes to asking and answering question to find insights in the data.


## Introduction
Mr. Macaroni is a project that tries to analyze  a YouTube creator and actor call Mr. Macaroni. He plays the character of a **Rich Yoruba Married Man who loves women**. His major strategy for getting women is to send them large among of money with the hope of getting sexual favors from the lady or ladies in question. 

## Summary
**These are some insights from the data.**

1. Mr. Macaroni has spent 81,516,000 naira on women from 2019 to 2022
2. Mr. Macaroni has a Net Expense of 41,466,000 naira on women from 2019 to 2022. As some women have given him money.
3. Mr. Macaroni has met 45 women since 2019 to 2022
4. We found that Mr. Macaroni spends an average of 921,466.66 naira per women.
5. The  cost of acquisition is 6,911,000.00 naira. That is, for Mr. Macaroni to earn 1 success, he would need to speed almost 7 million naira.	

## Asking Questions
 While watching his videos, The data analyst in me asked a single question.

**How much money has he spent all through out the time he has been making such videos?**

From this one question, other questions came.
How successful has he been with women?
How much money does he spend on an average on women?
Has he ever made money from a woman, how much?
How many women has he met?
What is the least amount of he has spent on a woman?

We could ask some more questions, but we would stop here. 


## Data Preparation
*Google Sheets*

In other to answer these question we need data. The process of collecting the data was watching all Mr. Macaroni's Videos from 2019 to 2022. While collecting the data we looked at 5 data points (Attributes).

### Definition of Attributes
 1. **Date** - This refer to the date in which the video was uploaded.
 2. **Amount Spent** - This refer to the amount of money Mr. Macaroni gives a woman in the video with the intention of having a sexual favor returned to him. Money given to his wife is also record. Lastly, some video's did not give clear monetary values in the video. In those case, They where labeled as null.
 3. **Title** - This refers to the title of the video.
 4. **Amount Received** - This refers to the amount of money Mr. Macaroni directly or indirectly received from a woman.
 5. **Successful Encounters** - This refers to the a yes or no/ 0 or 1 question that asks whether Mr. Macaroni was successful with the women or not. Success is define appearance of getting the lady, or the uncertainty getting the lady. 

Since certain attributes could not be automated, data collection was done manually, and recorded on a google sheet the table is called Freaky table.

### Schema of Freaky Table
|Field Name|Type|
|--|--|
| Date | Date |
| Amount Spent| Integer|
| Title| String|
| Amount Received| Integer|
| Success| Integer|

### Freaky Table

|Date |Amount Spent|Amount Received|Title|Success
|--|--|--|--|--|
|2019-12-03 | 4000000|null|OWO COOPERATIVE|0
|2019-12-14 | 2559000|null|CAN YOU IMAGINE THIS LADY|0
|2020-01-15 | 500000|null|DOUBLE WAHALA OOO|1
|2020-09-11 | 1000000|null|THE GOOD LIFE 😂😩🙆🏾‍♂️|0
|2022-01-07|  0|10000000|NEW YEAR NEW ME \ MR MACARONI \ QUEEN \ DADDY WA IS CASHING OUT|1

**Note**: This table above does note represent the actual data set but it is used as an example of how the table looks.

## Processing and Analysis

*Big Query - SQL*

### Processing

Given the questions established and the table shown above, I decided that a column should be added called **Net Expenses**. This refers to the difference between Amount Spent and Amount Received. However, while creating the column in SQL, There was an issue.

If one of the cells you are subtraction from or add to is null your result would be null. Thus, I need to use a different code to solve the problem.

    SELECT
	    *,
	    IF(Amount_Spent IS  null, 0, Amount_Spent)  -  IF(Amount_Received IS  null, 0, Amount_Received) Net_Exp
    
    FROM  `data-analytics-projects-339822.Mr_Macaroni_Dataset.Freaky_Data`

> This code chuck set all the null values in the Amount_Spent and Amount_Received column to 0. Then the their difference is take away to give us the Net_Exp column as well as every other column.

### Analysis
For the analysis part, we would be answering the questions that were asked earlier.

 - **How much money has he spent all through out the time he has been making such videos?** 
		 - This has two possible answers, the Total Net Expenses or Total Expenses

	**Total Expenses**
				Mr. Macaroni has spent 81,516,000 naira on women from 2019 to 2022

> 	The code chunk below find the Total Net Expense.

    	SELECT
	        SUM(Amount_Spent)
	    FROM  `data-analytics-projects-339822.Mr_Macaroni_Dataset.Freaky_Data`
		
		
**Total Net Expenses**
Mr. Macaroni has a Net Expense of 41,466,000 naira on women from 2019 to 2022

> The code chunk below find the Total Net Expense
	
			
    	SELECT
	        SUM(Amount_Spent) -  SUM(Amount_Received) Total_Net_Exp
	    FROM  `data-analytics-projects-339822.Mr_Macaroni_Dataset.Freaky_Data`

Here we look at a graph showing [Mr. Macaroni's Net Expenses from 2019 to 2022 by Month/ Year](https://public.tableau.com/views/MrMacaroni/Dashboard2?:language=en-US&:display_count=n&:origin=viz_share_link)

It is also interesting to find out that in some case, Mr. Macaroni has made money women too.

 **Has he ever made money from a woman, how much?**
		 Yes he has.
	**How much? Total Received**
	Mr. Macaroni has a Total Revenue of 40,050,000 naira from women from 2019 to 2022
> 	The code chunk below find the Total Net Expense.
	
	    SELECT
		    SUM(Amount_Received)
	    FROM  `data-analytics-projects-339822.Mr_Macaroni_Dataset.Freaky_Data`

**How successful has he been with women?**
This question refer to the success rate of Mr. Macaroni. The success rate is calculated by dividing his successful encounter by the number of encounters. This give us a success rate of 13.33%.

	SELECT
		(sum(Success_)/count(Date))*100
	FROM  `data-analytics-projects-339822.Mr_Macaroni_Dataset.Freaky_Data`
	
**On average, how much money does he spend on women?**
We found that Mr. Macaroni spends an average of 921,466.66 naira per women.

	SELECT
	(SUM(Amount_Spent)  -  SUM(Amount_Received))/  count(Title)
	FROM  `data-analytics-projects-339822.Mr_Macaroni_Dataset.Freaky_Data`

How many women has he met?
Mr. Macaroni has met 45 women since 2019 to 2022

    SELECT
    count(Title)
    FROM  `data-analytics-projects-339822.Mr_Macaroni_Dataset.Freaky_Data`

> This code chuck counts the number of title in the table. We use titles because we know that every video would have a single title, and in each video a single woman is featured.

**What is the least and most amount of he has spent on a woman?**
For least, we can easily say Zero because of null values that were turned to 0. we are also assuming that he ever spent is not a negative number. This is not so interesting, so we can look at the second smallest amount of money.

	SELECT
	MIN(Amount_Spent)  AS Min_AS_2nd
	FROM  `data-analytics-projects-339822.Mr_Macaroni_Dataset.Freaky_Data`
	WHERE Amount_Spent NOT  IN  (SELECT  MIN(Amount_Spent)  FROM  `data-analytics-projects-339822.Mr_Macaroni_Dataset.Freaky_Data`)

> This code chunk finds the second smallest amount of money Mr. Macaroni has spent on a women from 2019 to 2022.

Mr. Macaroni has also spent at his highest, 10,000,000 naira. 

    SELECT
    MAX(Amount_Spent)  AS Max_AS
    FROM  `data-analytics-projects-339822.Mr_Macaroni_Dataset.Freaky_Data`

**What is the cost of being successful?**
It would be also interesting to see Mr. macaroni's cost of acquisition. That is, how much does it cost him to be successful? In order words, cost of acquisition. To calculate this, we would need to divide the net expenses by the number of successes.

    SELECT  
    SUM(Net_Exp)/SUM(Success_)  
    FROM  `data-analytics-projects-339822.Mr_Macaroni_Dataset.lol`

The  cost of acquisition is 6,911,000.00 naira. That is, for Mr. Macaroni to earn 1 success, he would need to speed almost 7 million naira.	



### Correlation Between Success Rate and Amount Spent
*Google Sheet*

An interesting thing to looking into is to see if there is any correlation between Success Rate and Amount Spent.
Using the Pearson product-moment correlation coefficient, we found that there is a weak correlation of 0.27 between the two variables.

    =CORREL(B2:B46,D2:D46)

*Tableau*
Here we look at [relationship between Success and Net Expenses](https://public.tableau.com/views/MrMacaroni/Dashboard1?:language=en-US&:display_count=n&:origin=viz_share_link)

## Conclusion
In this project we explored the spending habits of a fictional character call Mr. macaroni, We saw that there is little to no correlation between his net spending and  his chances of being successful. We strongly recommend that Mr. macaroni to stop spend excessive amount of money on 
 women, as it is costing him millions every year.
