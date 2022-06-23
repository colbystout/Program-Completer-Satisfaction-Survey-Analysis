# Program-Completer-Satisfaction-Survey-Analysis
### My process of appending, cleaning, visualizing, and analyzing survey data in Power BI

## Project Overview

This survey project was completed on behalf of my employer in higher education. The dataset used is a collection of 3-year cycles of survey data for analysis of completer satisfaction and program success of each survey respondent. The two tables used covered 3 academic years: (17-18, 18-19, 19-20) and (18-19, 19-20, and 20-21) and collected via Qualtrics surveys. A typical academic year runs from 9/1 to 8/31 of the following year. The datasets cannot be shared to to FERPA and the existence of sensisitive PII within the data sets. Each survey question is on a 4-step likert scale from "Strongly Agree" to "Strongly Disagree."

This dashboard is built slightly different than most analytical dashboards. It was built to compliance specifications of the state department of education; also, it was kept simple with easy-to-find filters for inexperienced dashboard users in mind.

### Limitations to the Data

1. Several respondents left certain response prompts empty, decreasing some viability of certain data points.
2. The open-ended response data is not sufficient enough to perform a qualitative analysis due to lack of responses in these prompts.

### Methodology and Tools

Each table was initially inspected and reviewed via Microsoft Excel. The dataset is not incredibly large, so visible inspection through spreadhseets was a viable option to get preliminary insights to cleaning needs.

Initial cleaning on obvious and quick items was performed through spreadsheet functions and the 'replace values' tool. Trimming was also required in empty cells.

For larger cleanup needs and model building, I used Power Query to make changes, transformations, and additions to the dataset.

Finally, Power BI was the key tool in creation of an analytical dashboard.

## Building the Dataset

As explained in the overview, the dataset consisted of two tables with separate, 3-cycle data tables. 

1. To begin, I created a fresh .xlsx Excel workbook and performed 'Data (tab)' > 'import from Excel' from both spreadsheets into separate tabs of my new workbook. 
2. After checking to see if both tables' columns were in the same exact order, I manually appended the newest survey data to the oldest and deleted the old sheet in the workbook. 
3. Once one sheet remained, I renamed the tab. Both original tables were archived safely in a protected company SharePoint folder.
4. The dataset had some key data missing that was imperative for analysis: program codes, race, ethnicity, licensure areas for state licenses, and graduation dates. I ran an internal report for all active candidates from the beginning of 2016 to the end of 2021, and then exported that as a separate spreadsheet.
6. I used the VLOOKUP function to fill in the aforementioned attributes using the 'student ID' as my primary key. Some students did not have a reported race or ethnicity so I used the IF logical operator to deal with the "#N/As."(code in repository)
7. Used 'copy' and 'paste as values' on each new column to make the data static values and non-function.

## Excel Cleaning Process

1. The first order of business, before I could move into my Power BI/Power Query workspace, was to transform my 'working as a licensed teacher column'. The values were in a binary 0/1 system, which would not be very helpful in my workspace and would be much quicker to fix in a spreadsheet instance. I did two 'replace values' to change my 1's to "Employed as Teacher" and my 0's to "Not Employed as Teacher."
2. Performed 'copy' and 'pasted as values' to make data static and non-function.
3. Fixed 'State(s) license' case to read 'State(s) License'.
4. Fixed long title 'Content state licensure subject' to 'Content Area'. (This is standard language for the state.)
5. Highlight the entire table and used 'trim' tool. I want to make sure Power BI/Power Query only had (null) and no (blank) values. They are not the same and will negatively affect cleaning and visualizations.
6. The file was prepared enough to store in our Power BI data repository at this point.

## Power Query Cleaning Process

1. Once the data was stored in the repository, I opened a fresh Power BI desktop instance, imported the data via Excel from the repository, and selected to transform the data.
2. Used 'replace values' tool to replace all null race and ethnicity values
3. At the request of the state, 'race' and 'ethnicity' data should be reported as one. Used the 'merge field' tool to concatenate both columns using a "/" as a delimiter.
4. Each survey question had its own column the the dataset, which was not a very useful format for visualization. I selected each survey questioncolumn and used the unpivot tool to change the structure of the dataset. The format was no longer wide, rather, it was in a long format. Meaning, all survey question columns were changed to an "Attribute" column and "Value" column.
5. I renamed these columns 'Question' and 'Response,' respectively.
6. I knew I wanted each column to be in order by best to worst instead of alphabetically. To do this, I created a conditional column ranking ('LikertSortOrder'):
   - Strongly Agree = 1
   - Agree = 2
   - Disagree = 3
   - Strongly Disagree = 4
7. For respondents who did not complete the survey fully, I use the 'replace values' tool to change 'Employed as Teacher' attrivute null values to 'Unknown'.
8. I realized my 'GradDate' column can in as 'text' type. This would be problematic for my plan to create a custom graduation academic year column/slicer. I changed the column type to 'Date'.
9. This was everything I could find that needed cleaned, so I used 'close and apply' and went into my Power BI instance.

## Power BI Dashboard Creation (See Dashboard PNG in Repository)

1. I started by centering the canvas and adding a background. The background is a simple, texture gradient in a gray hue. I am a big fan of dark themes.
2. I added a card to the canvas, using 'student id' as the attribute and set it to 'Count (Distinct)'. This gave me the unique count of students contained in the data set: 161. I titled the card "Student Count" and removed "Distinct count of user id."
3. I created the 4 different slicers: Program, State(s) License, Race/Ethnicity, and Content Area
4. I started a custom column for my 'Grad Year' column using logical operators with DAX on the 'GradDate' column. (See repository for code.)
5. I created the slicer from the new 'Grad Year' column.
6. I created a pie chart named "Employed as Teacher" to give a visible representation for the employement status at all times while slicing and analyzing.
7. Now it is time to make the main, horizontal stacked-bar visualization. I set the 'Response' column to X-axis, 'Question' column to Y-axis, and 'Response' as the legend.
8. Earlier I created the "LikertSortOrder' column to organize the order of the legend/chart. I set 'Response' ordered by 'LikertSortOrder' to cleanly label everything best to worst.
9. I created a benchmark constant line at 80%. (It is standard practice for my organization to KPI performance at 80%.)
   - Note: The goal is to have each question rate above 80% when aggregating 'Strongly Agree' and 'Agree' together. If the disagree responses go beyond 20%, the topic needs investigated.
