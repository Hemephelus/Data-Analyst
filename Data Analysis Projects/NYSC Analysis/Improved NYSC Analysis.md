# Improved NYSC Analysis
To carry out this analysis, we would be making use of these tables.

- Form Responses Table

| Field name                                                                                                        | Type      |
|------- | --------- |
| Timestamp                                                                                                         | TIMESTAMP |
| State\_of\_Origin                                                                                                 | STRING    |
| Age                                                                                                               | INTEGER   |
| Religion                                                                                                          | STRING    |
| Sex                                                                                                               | STRING    |
| Marital\_Status                                                                                                   | STRING    |
| Qualification                                                                                                     | STRING    |
| Are\_you\_concessional\_deployment\_                                                                              | BOOLEAN   |
| ... | ...   |

- States Table

| Field name | Type    |
| ---------- | ------- |
| ID         | INTEGER |
| State      | STRING  |

## Improvements
### 1. State of Origin?
We improved this visualisation by changing the visualisation from a pie chart to a Map of Nigeria. Unlike a pie chart, we use maps to visualize locations such as the states in Nigeria. This implementation was done with SQL and R.

***SQL***
To get each state and the number of people in each state I needed to Join two tables together. The Form Responses Table and the States Table. I used an **INNER JOIN**  AND  **SUB QUERY** to archive this goal.

```SQL
SELECT

ST.State,

--This replaces all rows that are null with 0
IF(No_of_people_per_State IS  NULL, 0 ,No_of_people_per_State)  AS No_of_people_per_State

FROM  `data-analytics-projects-339822.NYSC_Camp_Analysis.States`  AS ST

-- Here I want to get all states regardless of whether there are no state respondents in the form.
LEFT  JOIN  

--SUBQUERY
-- Here I am getting a table with the State of Origin and the number of respondents from that state.
(SELECT

State_of_Origin,
COUNT(State_of_Origin)  AS No_of_people_per_State

FROM  `data-analytics-projects-339822.NYSC_Camp_Analysis.Form Responses`

GROUP  BY State_of_Origin)  AS FR

ON ST.State = FR.State_of_Origin

 --This returns the states and the number of people in each state
```

| State                     | No\_of\_people\_per\_State |
| ------------------------- | -------------------------- |
| Abia                      | 31                         |
| Adamawa                   | 4                          |
| Akwa Ibom                 | 1                          |
| Anambra                   | 30                         |
| Bauchi                    | 0                          |
| Bayelsa                   | 1                          |
| Benue                     | 20                         |
| Borno                     | 0                          |
| Cross River               | 1                          |
| Delta                     | 9                          |
| Ebonyi                    | 0                          |
| Edo                       | 0                          |
| Ekiti                     | 17                         |
| Enugu                     | 33                         |
| Federal Capital Territory | 0                          |
| Gombe                     | 0                          |
| Imo                       | 56                         |
| Jigawa                    | 0                          |
| Kaduna                    | 0                          |
| Kano                      | 0                          |
| Katsina                   | 0                          |
| Kebbi                     | 0                          |
| Kogi                      | 22                         |
| Kwara                     | 22                         |
| Lagos                     | 17                         |
| Nassarawa                 | 0                          |
| Niger                     | 4                          |
| Ogun                      | 41                         |
| Ondo                      | 14                         |
| Osun                      | 47                         |
| Oyo                       | 30                         |
| Plateau                   | 3                          |
| Rivers                    | 8                          |
| Sokoto                    | 0                          |
| Taraba                    | 1                          |
| Yobe                      | 0                          |
| Zamfara                   | 0                          |


***R***
I used Choropleth maps to display differences among regions. We used the values from the table above to create the map in R.
```R
# Installation of the naijR package for visualizing the Nigerian Map.
install.packages("naijR")

#Loading the package
library(naijR)

# Initiating the states in Nigeria
ss <- states()

# Mapping each state to its corresponding values.
nn <- c(31, 4, 1, 30, 0, 1, 20, 0, 1, 9, 0, 0, 17, 33, 0, 0, 56, 0, 0, 0, 0, 0, 22, 22, 17, 0, 4, 41, 14, 47, 30, 3, 8, 0, 1, 0, 0)  # random real numbers ranging from 0 - 100

# Creating groups in intervals of 10
bb <- c(0,10, 20, 30, 40, 50, 60)

# Plotting the Map showing the number of corpers from each state.
map_ng(region = ss, x = nn, breaks = bb, col = 'YlOrRd', show.text = TRUE)
```
  
[Click Here to see the Map](https://imgur.com/wsFA0ou)

### 2. Age

I improved the visualisation by changing the visualisation from a pie chart to a Bar Chart. This is because, with a bar chart, we can easily evaluate and differentiate one age group from another. This implementation was done with SQL and Tableau.

***SQL***
The data I have has not done any form of grouping. Thus, I would use the **CASE** statement and **SUB QUERY** to group the data into 6 groups. 

```SQL
SELECT

-- This Creates a column called Age Group that groups the ages of each corp member into 6 groups.

CASE  

WHEN Age <  20  THEN  '<20'

WHEN Age >  19  AND Age <  23  THEN  '20 - 22'

WHEN Age >  22  AND Age <  26  THEN  '23 - 25'

WHEN Age >  25  AND Age <  29  THEN  '26 - 28'

WHEN Age >  28  AND Age <  32  THEN  '29 - 31'

WHEN Age >  31  THEN  '>31'

END  As Age_group,
  
-- This creates a column called No_of_people_in_age_group that finds the frequency of respondents in each age group. 
COUNT(Age)  AS No_of_people_in_age_group,

-- This creates a column called Percentage_of_people_in_age_group that find the percentage of respondents in each age group.
--SUBQUERY
ROUND((COUNT(Age)/(

SELECT

COUNT(Age)

FROM  `data-analytics-projects-339822.NYSC_Camp_Analysis.Form Responses`))*100,2)

AS Percentage_of_people_in_age_group  

FROM  `data-analytics-projects-339822.NYSC_Camp_Analysis.Form Responses`

  
-- We filter to remove all null values.
WHERE Age IS  NOT  NULL

  
-- Here we group by age group
GROUP  BY Age_group

-- Here we sort the table by the frequency of respondents in each age group in descending order.
ORDER  BY No_of_people_in_age_group DESC

-- This will return a table of the Age groups, their Frequency and Percentage.
```
| Age\_group | No\_of\_people\_in\_age\_group | Percentage\_of\_people\_in\_age\_group |
| ---------- | ------------------------------ | -------------------------------------- |
| 26 - 28    | 174                            | 40.65                                  |
| 23 - 25    | 158                            | 36.92                                  |
| 20 - 22    | 55                             | 12.85                                  |
| 29 - 31    | 38                             | 8.88                                   |
| <20        | 2                              | 0.47                                   |
| \>31       | 1                              | 0.23                                   

To see the **Tableau** bar chart check out **Slide 3**.	

### 3. Qualification 

Like Age, we can easily evaluate and differentiate the number of people holding one qualification from people holding another with a bar chart. This implementation was done with SQL and Tableau.

SQL

```SQL
SELECT

Qualification AS QUALIFICATION,

COUNT(Qualification)  AS NUMBER_OF_QUALIFICATIONS

FROM  `data-analytics-projects-339822.NYSC_Camp_Analysis.Form Responses`

WHERE Qualification IS  NOT  NULL

GROUP  BY Qualification 

ORDER  BY NUMBER_OF_QUALIFICATIONS DESC

-- This will return a table of the Qualification and their Frequency.
```
| QUALIFICATION       | NUMBER\_OF\_QUALIFICATIONS |
| ------------------- | -------------------------- |
| BSc 				  | 264                        |
| HND                 | 133                        |
| B.ed                | 21                         |
| B.a                 | 16                         |
| B.Eng               | 2                          |


### 4. **How do you rate the purpose for establishing the NYSC Scheme?**

For this question, there are 4 possible responses. 
- Very low, 
- low, 
- high, 
- very high.
Like in number 3, the same rules will be used in **SQL**. In addition, the same bar chart will be implemented in **Tableau**.

```SQL
SELECT

How_do_you_rate_the_purpose_for_establishing_the_NYSC_Scheme_ AS PURPOSE_SCORE,

COUNT(How_do_you_rate_the_purpose_for_establishing_the_NYSC_Scheme_)  AS NUMBER_OF_PEOPLE

FROM  `data-analytics-projects-339822.NYSC_Camp_Analysis.Form Responses`

WHERE How_do_you_rate_the_purpose_for_establishing_the_NYSC_Scheme_ IS  NOT  NULL

GROUP  BY How_do_you_rate_the_purpose_for_establishing_the_NYSC_Scheme_

ORDER  BY NUMBER_OF_PEOPLE DESC

-- This will return a table of the PURPOSE_SCORE and their Frequency.

```
| PURPOSE\_SCORE | NUMBER\_OF\_PEOPLE |
| -------------- | ------------------ |
| High           | 263                |
| Very high      | 135                |
| Low            | 26                 |
| Very Low       | 5                  |


### 4. How_satisfied_were_you_with_the_following?


```SQL
SELECT

DISTINCT(How_satisfied_were_you_with_the_following___Mode_of_serving_food_)  AS Score,

count(How_satisfied_were_you_with_the_following___Mode_of_serving_food_)  AS Mode_of_serving_food,

count(How_satisfied_were_you_with_the_following___involvement_of_corps_in_the_preparation_of_food_)  AS involvement_of_corps_in_the_preparation_of_food,

count(How_satisfied_were_you_with_the_following___Quality_of_food_served_)  AS Quality_of_food_served,

count(How_satisfied_were_you_with_the_following___Quantity_of_food_)  AS Quantity_of_food,

count(How_satisfied_were_you_with_the_following___Feeding_arrangement_in_general_)  AS Feeding_arrangement_in_general_

  

FROM  `data-analytics-projects-339822.NYSC_Camp_Analysis.Form Responses`

  

WHERE How_satisfied_were_you_with_the_following___Mode_of_serving_food_ IS  NOT  NULL

GROUP  BY Score
```

| Score            | Mode\_of\_serving\_food | involvement\_of\_corps\_in\_the\_preparation\_of\_food | Quality\_of\_food\_served | Quantity\_of\_food | Feeding\_arrangement\_in\_general\_ |
| ---------------- | ----------------------- | ------------------------------------------------------ | ------------------------- | ------------------ | ----------------------------------- |
| Satisfied        | 184                     | 182                                                    | 183                       | 182                | 184                                 |
| Fairly Satisfied | 96                      | 95                                                     | 95                        | 96                 | 94                                  |
| Very Satisfied   | 97                      | 97                                                     | 96                        | 96                 | 97                                  |
| Not Satisfied    | 53                      | 52                                                     | 53                        | 52                 | 53                                  |

### 5. How do you rate observance of physical distancing protocol in the following areas?

```SQL
SELECT

DISTINCT How_do_you_rate_observance__if_physical_distancing_protocol_in_the_following_areas___Bed_spacing_ Score,

  

count(How_do_you_rate_observance__if_physical_distancing_protocol_in_the_following_areas___Bed_spacing_) Bed_spacing,

count(How_do_you_rate_observance__if_physical_distancing_protocol_in_the_following_areas___Registration__) Registration,

count(How_do_you_rate_observance__if_physical_distancing_protocol_in_the_following_areas___Lecture__) Lecture,

count(How_do_you_rate_observance__if_physical_distancing_protocol_in_the_following_areas___Sports__) Sports,

count(How_do_you_rate_observance__if_physical_distancing_protocol_in_the_following_areas___Issuance_of_kit_) Issuance_of_kit,

count(How_do_you_rate_observance__if_physical_distancing_protocol_in_the_following_areas___Serving_meals__) Serving_meals,

count(How_do_you_rate_observance__if_physical_distancing_protocol_in_the_following_areas___Camp_market__) Camp_market

FROM  `data-analytics-projects-339822.NYSC_Camp_Analysis.Form Responses`

WHERE How_do_you_rate_observance__if_physical_distancing_protocol_in_the_following_areas___Bed_spacing_ IS  NOT  NULL

GROUP  BY Score
```

| Score     | Bed\_spacing | Registration | Lecture | Sports | Issuance\_of\_kit | Serving\_meals | Camp\_market |
| --------- | ------------ | ------------ | ------- | ------ | ----------------- | -------------- | ------------ |
| Good      | 220          | 219          | 218     | 218    | 216               | 215            | 215          |
| Poor      | 128          | 128          | 128     | 128    | 126               | 126            | 127          |
| Very good | 91           | 91           | 91      | 89     | 91                | 88             | 90           |


### 6. Assess_compliance_with_COVID_19_safety_protocols_by_the_following

**SQL**
```SQL
SELECT 
DISTINCT Assess_compliance_with_COVID_19_safety_protocols_by_the_following___NYSC_Officials__ Score,

count(Assess_compliance_with_COVID_19_safety_protocols_by_the_following___NYSC_Officials__) NYSC_Officials, 
count(Assess_compliance_with_COVID_19_safety_protocols_by_the_following___Soldiers__) Soldiers, 
count(Assess_compliance_with_COVID_19_safety_protocols_by_the_following___Police_) Police, 
count(Assess_compliance_with_COVID_19_safety_protocols_by_the_following___NSCDC_) NSCDC, 
count(Assess_compliance_with_COVID_19_safety_protocols_by_the_following___Man_O_War___) Man_O_War, 
count(Assess_compliance_with_COVID_19_safety_protocols_by_the_following___Red_Cross_) _Red_Cross, 
count(Assess_compliance_with_COVID_19_safety_protocols_by_the_following___Stewards__Cleaners_) Stewards__Cleaners, 
count(Assess_compliance_with_COVID_19_safety_protocols_by_the_following___Camp_Market_Operators__) Camp_Market_Operators, 
count(Assess_compliance_with_COVID_19_safety_protocols_by_the_following___Visitors__) Visitors

 FROM `data-analytics-projects-339822.NYSC_Camp_Analysis.Form Responses` 
 WHERE Assess_compliance_with_COVID_19_safety_protocols_by_the_following___NYSC_Officials__ IS NOT NULL 
 GROUP BY Score
```
| Score     | NYSC\_Officials | Soldiers | Police | NSCDC | Man\_O\_War | \_Red\_Cross | Stewards\_\_Cleaners | Camp\_Market\_Operators | Visitors |
| --------- | --------------- | -------- | ------ | ----- | ----------- | ------------ | -------------------- | ----------------------- | -------- |
| Good      | 208             | 208      | 206    | 206   | 208         | 207          | 207                  | 207                     | 205      |
| Very good | 215             | 215      | 211    | 212   | 215         | 209          | 208                  | 206                     | 203      |
| Poor      | 13              | 13       | 13     | 13    | 13          | 13           | 13                   | 13                      | 13       |
