# Program-Completer-Satisfaction-Survey-Analysis
### My process of appending, cleaning, visualizing, and analyzing survey data in Power BI

## Project Overview

This survey project was completed on behalf of my employer in higher education. The dataset used is a collection of 3-year cycles of survey data for analysis of completer satisfaction and program success of each survey respondent. The two tables used covered 3 academic years: (17-18, 18-19, 19-20) and (18-19, 19-20, and 20-21) and collected via Qualtrics surveys. A typical academic year runs from 9/1 to 8/31 of the following year. The datasets cannot be shared to to FERPA and the existence of sensisitive PII within the data sets.

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
5. I used the VLOOKUP function to fill in the aforementioned attributes using the 'student ID' as my primary key. (code in repository)

## Excel Cleaning Process

1. The first order of business, before I could move into my Power BI/Power Query workspace, was to transform my 'working as a licensed teacher column'. The values were in a binary 0/1 system, which would not be very helpful in my workspace and would be much quicker to fix in a spreadsheet instance. I did two 'replace values' to change my 1's to "Employed as Teacher" and my 0's to "Not Employed as Teacher."
2. For respondents who did not complete the whole survey, null values existed. Used another 'replace values' to change null values to "Unknown.
3. At the request of the state, 'race' and 'ethnicity' data should be reported as one. With two existing columns for each separate data point, I used a concatenate function to bring them together. (Code in repository)
4. Highlight the entire table and used 'trim' tool. I want to make sure Power BI/Power Query only had (null) and no (blank) values. They are not the same and will negatively affect visualizations.
