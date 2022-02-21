
# Personal Finance
In order to improve my relationship with money, I decided to keep track of my money so I can be aware of where most of my money is going to. Thus, I made a finance tracker to help with that.
For most this project I use [Google sheet](https://docs.google.com/spreadsheets/d/1vEobyPacJvvCKcYRdku-EP6aoEGuqFK67RVonRGobpY/edit?usp=sharing) for the analysis and dashboard. In addition, I used [Google Form](https://forms.gle/rfmUZF7yRDtMbejJA) for data collection and [Apps Script](https://github.com/Hemephelus/Data-Analyst/blob/ebd313ba68055096e133469ec488202a3d95cd4b/Data%20Analysis%20Projects/Personal%20Finance%20Project/Automation%20Code) for Automation.


## Google Sheets

### The Tabs
In the sheet we have 6 Tabs.

 ### 1. Summary
  - This tab represents the dashboard as it shows a live and dynamic interface that allows you to see a summary of my finances at any point in time. 
  - You can change the time frame to see a summary during a particular period.
  - There are 2 charts on the tab.  The 1st is a bar graph that shows the total amount of money earned from a particular period, grouped by **sources**. Secondly, we have the another bar graph that shows the total amount spent from a particular period, grouped by **category**, and then grouped by **item**.
  - The cells with a gray background shows the places you can edit.

Category
|  Category| Education |Food |Fashion |Gifts |Utilities |Transportation |Home Up Keep|
|:--------:| -------------:|:--------:| -------------:|:--------:| -------------:|:--------:| -------------:|
| Item| Books |Groceries| Wears| Gifts| Phone| Fuel| Supplies|
| Item| |Restaurants| Laundry/dry cleaning| Donations (charity)| AirTime | Repairs |Maintenance|
| Item| | | Hair/beauty| | Internet| Registration/license| Improvements| 
| Item| | | | | Heat/gas| Public transit| |
| Item| | | | |Electricity | | 
| Item| | | | |Trash | | 

***You can see the dashboard/summary here [Google sheet](https://docs.google.com/spreadsheets/d/1vEobyPacJvvCKcYRdku-EP6aoEGuqFK67RVonRGobpY/edit?usp=sharing)***

  ### 2. Expenses
  - This tab shows a live and dynamic interface that allows you to see all our expenses at any point in time. 
  - You can change the time frame to see how much was spent during a particular period.
  - The cells with a gray background shows the places you can edit.
  - In the table we keep track of the Date, Person, Item, Price, Picture of Receipt, Description, and Categories
  ### 3. Income
  
   - This tab shows a live and dynamic interface that allows you to see all our income at any point in time. 
  - You can change the time frame to see how much was made during a particular period.
  - The cells with a gray background shows the places you can edit.
  - In the table we keep track of the Date, Person, Sources, Price, and Description

  ### 4. Helpers
  >   *(Hidden Sheet)*
  
   This tab helps the dashboard be dynamic. This is done by using the query function and concatenation operation "&". You will not be able to edit this tab.

## Google Forms
  ### 5. Form Responses 

>   *(Hidden Sheet)*

  The form responses tab is linked to a google form. I found that it was very difficult for me to religiously go to my laptop to update my expenses, so I made a google form. I also made the form link look like an app on my phone. Thus reducing the friction of recording my expenses, Now I could do track my finance from any where.

The form keeps track of:

 - *Timestamp,  Person(s),  Type Of transaction,  Item, Sources,  Price,
   Picture of the receipt: (if any),  Description*

  
## JavaScript (Apps Script)
  ### 6. Details
In order to make life easier for myself and any other person that would like to use the sheet, I wrote a script that creates a custom menu called  "**Your Tools**". This menu is beside the "**Help**", at the right hand side. This function allows you to update the form, Activate Daily Form Reminder Email, Activate Weekly Checkup Reminder Email. These function work hand in hand with the Details tab.
 -  **The Update Form** function allow people to update the form from the spread sheet without going to the actual form.
 - **The Activate Daily Form Reminder Email** function creates a trigger that send an email reminding me to record my expenses or Income for
   the day. I have found this to increase the amount of times I remember
   to track my finances.
 - **Activate Weekly Checkup Reminder Email** function creates a trigger that send an email reminding you to record my expenses or Income for the week. This is for people that would prefer a weekly reminder.

## Conclusion

After carrying out this project, Here is what I found.

For the month of February 2022, I found that I have been spending a lot on **Food and Home Up Keep as these 2 account for  around 70% of my Expenses**. On the other hand, **My Grohe salary accounts for 60% of income**. In addition, **I saves around 47% of my income.** I learnt a lot from this project. for example automation, building a dynamic dashboard in google sheets, and most importantly, I learnt about my finance.

