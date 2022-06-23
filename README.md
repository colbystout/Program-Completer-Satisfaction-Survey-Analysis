# Program-Completer-Satisfaction-Survey-Analysis
## My process of appending, cleaning, visualizing, and analyzing survey data in Power BI

### Project Overview

This survey project was completed on behalf of my employer in higher education. The dataset used is a collection of 3-year cycles of survey data for analysis of completer satisfaction and program success of each survey respondent. The two tables used covered 3 academic years: (17-18, 18-19, 19-20) and (18-19, 19-20, and 20-21) and collected via Qualtrics surveys. A typical academic year runs from 9/1 to 8/31 of the following year. The datasets cannot be shared to to FERPA and the existence of sensisitive PII within the data sets.

This dashboard is built slightly different than most analytical dashboards. It was built to compliance specifications of the state department of education; also, it was kept simple with easy-to-find filters for inexperienced dashboard users in mind.

### Limitations to the Data

1. Several respondents left certain response prompts empty, decreasing some viability of certain data points.
2. The open-ended response data is not sufficient enough to perform a qualitative analysis due to lack of responses in these prompts.

### Methodology and Tools

Each table was initially inspected and reviews via Microsoft Excel. The dataset is not incredibly large, so visible inspection through spreadhseets was a viable option to get preliminary insights to cleaning needs.

Initial cleaning on obvious and quick items was performed through spreadsheet functions and the 'replace values' tool. Trimming was also required in empty cells.

For larger cleanup needs and model building, I used Power Query to make changes, transformations, and additions to the dataset.

Finally, Power BI was the key tool in creation of an analytical dashboard.

### Building the Dataset

As explained in the overview, the dataset consisted of two tables with separate, 3-cycle data tables. To begin, I created a fresh .xlsx Excel workbook and performed 'Data (tab)' > 'import from Excel' from both spreadsheets into separate tabs of my new workbook. After checking to see if both tables' columns were in the same exact order, I manually appended the newest survey data to the oldest and deleted the old sheet in the workbook. Once one sheet remained, I renamed the tab.

