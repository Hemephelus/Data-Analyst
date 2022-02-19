# Personal Finance
In other to improve my relationship with money, I decided to make a finance tracker to help with that.
For most this project I use [Google sheet](https://docs.google.com/spreadsheets/d/1vEobyPacJvvCKcYRdku-EP6aoEGuqFK67RVonRGobpY/edit?usp=sharing). However, I use [Google Form](https://forms.gle/rfmUZF7yRDtMbejJA). for data collection and [Apps Script](https://github.com/Hemephelus/Data-Analyst/blob/ebd313ba68055096e133469ec488202a3d95cd4b/Data%20Analysis%20Projects/Personal%20Finance%20Project/Automation%20Code). for Automation.


## Google Sheets

### The Tabs
In the sheet we have 6 Tabs.

 ### 1. Summary
  - This tab represents the dashboard as it shows a live and dynamic interface that allows you to see a summary of my finances at any point in time. 
  - You can change the time frame to see a summary during a particular period.
  - There are 2 charts on the tab.  The 1st is a bar graph that shows the average amount of money spent in a particular category. Secondly, we have the another bar graph that shows the average amount spent in a particular item (a subset of a category).
  - The cells with a gray background shows the places you can edit.

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
   This tab helps the dashboard be dynamic. This is done by using the query function and concatenation operation "&". You will not be able to edit this tab.

## Google Forms
  ### 5. Form Responses
  The form responses tab is linked to a google form. I found that it was very difficult for me to religiously go to my laptop to update my expenses, so I made a google form. I also made the form link look like an app on my phone. Thus reducing the friction of recording my expenses, Now I could do track my finance from any where.

The form keeps track of:

 - *Timestamp,  Person(s),  Type Of transaction,  Item, Sources,  Price,
   Picture of the receipt: (if any),  Description*

  
## JavaScript (Apps Script)
  ### 6. Details
In order to make life easier for myself and any other person that would like to use the sheet, I wrote a script that creates a custom menu called  "**Your Tools**". This menu is beside the "**Help**", at the right hand side. This function allows you to update the form, Activate Daily Form Reminder Email, Activate Weekly Checkup Reminder Email. These function work hand in hand with the Details tab.
		  - Update Form:
			The update form function allow people to update the form from the spread sheet without going to the actual form.
			-The Activate Daily Form Reminder Email function creates a trigger that send an email reminding me to record my expenses or Income for the day. I have found this to increase the amount of times I remember to track my finances.
			-Activate Weekly Checkup Reminder Email function creates a trigger that send an email reminding you to record my expenses or Income for the week. This is for people that would prefer a weekly reminder.


## Conclusion

After carrying out this project, I found that I have been Spending a lot on food and Airtime credit. I learnt a lot about automation and Dynamic dashboards In this Project.
  

