---
title: "Cashflow And Networth Analysis Documentation"
date: 2024-02-28
draft: false
---
# Overview
The Cashflow and Networth Analysis spreadsheet was designed to help you better understand your personal finances by providing detailed insights into your spending, income, assets, and liabilities over time, and by making your progress towards financial independence visible using powerful data visualizations.

The spreadsheet was designed to integrate seamlessly with Tiller as an extension to the Tiller foundation template but it also functions as a standalone spreadsheet for anyone who wants to import their data through other means.

The spreadsheet was built without using any macros, scripts or VBA code. This decision was made for two main reasons: To make the spreadsheet more accessible to those who aren't familiar with programming and VBA and to meet the requirements outlined by the Tiller Community Builder Rewards Program (since I eventually plan to share this spreadsheet there).
## Map
To help guide you through the numerous sheets included in the spreadsheet and their relationships, the following map was created:
![image](images/"Pasted image 20240208085759.png")
This map depicts the flow of data between sheets (dependencies). At a high level, the data flows from the foundation sheets (transactions, categories, balance history, accounts, and balances) to hidden intermediate sheets that progressively organize and summarize the raw data, and finally to dashboards that summarize the data using charts controls to filter the data as required.
## Sheet Overview
## Foundation Sheets
The foundation sheets are the core sheets that store your "fact" data (Transactions and Balance History) and "dimension" data (Categories, and Accounts). The Balances sheet function predominantly as a dashboard, but is also referenced externally.
## Spending and Income Dashboard and Intermediate Sheets
![image](images/"Pasted image 20240209101831.png")
These sheets allow you to analyze your spending and income over time by category and group. The sheets that make up each are identical save for the separation of income and spending transactions, and the increased focus on categories rather than groups for income (since most people will have considerably fewer income categories than spending categories). 

Use the slicers on the left to filter the data as desired. Use the plus/minus buttons on each pivot chart to switch between aggregating the data monthly and yearly.

The intermediate sheets contain pivot tables summarizing the data in the following ways:
- Total by Category
- Total by Group
- Average by Group (spending) or Category (income)
These three pivot tables are then referenced by the dashboards which provide summarized data, pivot charts and user controls.
## Networth Dashboard and Intermediate sheets
![image](images/"Pasted image 20240209101814.png")
These sheets allow you to analyze your assets, liabilities, and resulting networth over time.

The first intermediate sheet uses a combination of pivot tables and standard excel formulas to summarize the balance history data into balances by month (using the latest balance for each month). It also incorporates the account dimension data (account name, group, class) and calculates other useful information about each monthly balance. 

This sheet is then used to generate four more intermediate sheets which also use a combination of pivot tables and regular excel formulas to separate the data into monthly and yearly assets and liabilities organized by group. As with monthly data, the yearly balance data reports the latest available balance for the year. The monthly sheets also perform networth related calculations.

These four intermediate sheets are then referenced by the Networth Dashboard which provides summarized data, pivot charts, and user controls.
## Cashflow Dashboard and Intermediate Sheets
![image](images/"Pasted image 20240209101822.png")
While the spending and income sheets allow your to analyze your income and spending predominantly by categories and groups, these sheets allow you to analyze your total income and spending over time, your savings rate, and the frequency of your monthly spending via a histogram. Moving average trendlines for spending and income are also included to help identify longer term trends.

The histogram implementation for this dashboard was created using a custom bar chart rather than the built-in excel histogram. This was due to the built-in histogram being buggy and lacking in customization. Use the histogram overflow bin minimum and maximum input cells to define the bounds of your spending histogram. Any monthly spend greater than the bounds specified will be incorporated into these overflow bins. The overflow bins help keep the histogram clean in the presence of extreme one-off months. By default, the bin widths are defined as $500. The bin width can't easily be configured, though like anything in the spreadsheet it's technically modifiable if you're willing to invest the effort. You can see how the histogram is generated in the Income and Spending Monthly intermediate sheet.

The cashflow dashboard also features an inflation adjustment feature. Enter an inflation value to adjust past spending to the present year. This adjustment is important when analyzing spending across multiple years, since nominal monthly spend values will give you a somewhat inaccurate picture of how your spending is changing over time. If this adjustment isn't desired, enter 0% as the inflation rate. Any changes to this inflation rate requires a data refresh to take effect (see Updating Data below).

The intermediate sheets contain a combination of pivot tables and regular excel formulas to aggregate the spending and income by month and year, as well as perform the savings rate and histogram calculations.

These sheets are then referenced by the Cashflow dashboard which provides summarized data, pivot charts, and user controls.
## Year to Date Summary Dashboard
![image](images/"Pasted image 20240209102150.png")
This sheet allows you to analyze a summary of your year to date finances. It displays monthly cashflow in tabular and chart form, charts of spending and income by category, and a summary of current networth.

This summary dashboard doesn't depend on any intermediate sheets, and draws its data directly from the foundation sheets. 
## Cashflow and Networth Summary Dashboard
![image](images/"Pasted image 20240209102115.png")
This sheet attempts to summarize all of your key financial data and progress towards financial independence in a single chart. This chart features two vertical axes: The left axis displays monthly cashflow (income, spending, and safe withdrawal income), while the right axis displays networth. Moving average trendlines for spending and income are included to help identify longer term trends.

You can input a safe withdrawal rate in the cell at the top and the sheet will automatically calculate a monthly safe withdrawal income and plot it on the chart. Financial Independence is achieved when your yellow safe withdrawal line crosses your average spending line.

This summary dashboard draws its data from intermediate cashflow sheets and assets and liabilities sheets.
# Tiller Integration and Initial Setup
See https://help.tillerhq.com/en/articles/2283680-getting-started-with-tiller-for-microsoft-excel and https://help.tillerhq.com/en/articles/5668286-tiller-foundations-guide#h_c338c1baa8 for an overview on setting up Tiller to integrate your accounts with the spreadsheet and set up the foundation sheets.

Once you have a Tiller account setup and linked to the spreadsheet, you can import your transactions and balance history data. Follow the Tiller guides above to fill your spreadsheet using the Tiller Money Feeds add-on. 

For non-Tiller users, you won't be able to link your accounts and fill your spreadsheet using Tiller Money Feeds, but the rest of the information in the guides above for setting up your foundation sheets is still applicable.

Next, it's time to configure your accounts (https://help.tillerhq.com/en/articles/3250970-reviewing-balances-customizing-accounts) and categories (https://help.tillerhq.com/en/articles/3250769-customizing-categories). You can verify your accounts are setup correctly by inspecting the Balances sheet.
# General Usage

## Updating Data
Once the initial setup is complete you can update the spreadsheet periodically with new transaction and balance history entries as they come in.

Next, you must categorize your transactions. Follow the guidelines described in the Tiller Foundations guides above. The transactions sheet features validation on the category column which helps prevent invalid categories from being assigned. Tiller offers an auto-categorization feature (https://help.tillerhq.com/en/articles/6172979-autocat-for-microsoft-excel) for those interested in automating this process as much as possible, though personally I don't use it as I find the process of manually reviewing, categorizing, and reflecting on each transaction highly valuable. 

Next, verify that the Unique Account Identifier column in your Balance History sheet is populated for each row. This column is a custom add-on, and is critical for the dashboards and intermediate sheets to function correctly. If there are empty cells, simply apply the formula to the blank cells using the fill handle.

Once all your new data has been added and your transactions categorized, **you must refresh all data in order for the dashboards and pivot tables to update.** 

To refresh your data, navigate to the Data tab in the menu and click "Refresh All" as shown below, or press ctrl+alt+F5:
![image](images/"Pasted image 20240214094215.png")
## Reviewing Data
You can review your data whenever you like, however the spreadsheet was designed predominantly for reviewing on a monthly basis, with some dashboards going so far as to exclude the present month to avoid unsightly partial data. The dashboards excluding the present month include the Cashflow, Networth, and Cashflow and Networth Summary dashboards.
## Excluding Transactions
Often, our financial data contains numerous transactions that we do not want to include in our analysis. The spreadsheet features two designated ways to achieve this. The first, is by applying a category of type "Transfer" to a transaction. The second, is by applying the specific label "Reimbursable" to a transaction. These types of transactions often come in twos (the income transaction and the spending transaction) so make sure you exclude both!
## Configuring Moving Average Trendlines
The Cashflow and Networth Summary and Cashflow dashboards feature moving average trendlines to help you understand your data. These trendlines are created by averaging the values over a configurable number of prior periods, and thus may need to be adjusted based on the amount of data you have. As you accumulate more data you will likely want to increase the averaging window to determine longer term trends. 

The period over which these averages are calculated can be configured by right clicking on a chart, selecting "Format chart area" and then selecting the trendlines from the chart options dropdown as shown below. 
![image](images/"Pasted image 20240216092538.png")
Then, select "Trendline Options" and modify the period as shown:
![image](images/"Pasted image 20240216092718.png")
## Error Validation
Due to the complexity of the workbook, various sheets include error validation to help prevent issues. Unfortunately, this error checking can't be done automatically or on the entire workbook in one click so sheets have to be checked individually. To check a sheet for errors, navigate to the formulas toolbar and select error checking as shown below:
![image](images/"Pasted image 20240221110946.png")
If you notice discrepancies in the dashboard, try performing an error check on the following sheets:
- Transactions (for invalid categories)
- Balance History (for missing unique account identifiers)
# Advanced Functionality
The following sections describe some of the more advanced functionality behind the spreadsheet for anyone interested in a deeper understanding or who are interested in modifying and extending the spreadsheet.
## Power Pivot and the Excel Data Model
The Excel Data Model allows you to conveniently reference multiple tables at once as a single data source. This allows for the creation of pivot tables that can draw data from multiple tables.

When using the Data Model, it's highly beneficial to have Power Pivot installed. Follow the instructions provided by Microsoft here: https://support.microsoft.com/en-us/office/start-the-power-pivot-add-in-for-excel-a891a66d-36e3-43fc-81e8-fc4798f39ea8. 

Once installed, navigate to the new Power Pivot toolbar and select "Manage"
![image](images/"Pasted image 20240221112140.png")
A window will pop up displaying the tables included in the data model (in this case, the data contained in the four foundation sheets as well as two custom tables to support additional functionality).
![image](images/"Pasted image 20240221112310.png")
Once added to the Data Model, a pivot table can be created from a data model by navigating to Insert => PivotTable => From Data Model. This pivot table will have access to all the columns in the data model.

The Data Model also provides the ability to add custom columns that can include some basic formulas (unfortunately many Excel formulas are not supported here). This turned out to be the only way I could find to perform calculations on pivot table columns since the standard calculated field feature is disabled when using the Data Model.
![image](images/"Pasted image 20240221112903.png")
## Dynamic Chart Ranges and the Name Manager
While Pivot Charts update automatically when their underlying data changes, standard charts referencing a range of cells do not. However, standard charts are much more flexible than Pivot Charts and were required in multiple places in order to display data in the desired way. To enable standard charts to update their data automatically, you can create dynamic formulas to automatically retrieve the necessary data, and then store these formulas in the Name Manager which can subsequently be referenced anywhere in your workbook (including charts!)

You can see all the named formulas in the workbook by navigating to the Formulas toolbar, then clicking "Name Manager":
![image](images/"Pasted image 20240222091638.png")
![image](images/"Pasted image 20240222092854.png")
To see how these named references are wired up to the charts, you can right click on a standard chart (you can determine if a chart is a pivot chart if the "Pivot Table Analyze" toolbar shows up when you select it), click "Select Data", and then edit one of the dynamic data series:
![image](images/"Pasted image 20240222092252.png")
![image](images/"Pasted image 20240222092256.png")
So in the above example, the "Spending" series values in the Cashflow and Networth summary chart is set to `='Cashflow and Networth Analysis.xlsx'!DynamicSpendingMonthly` (you also need to reference the workbook when referencing names from charts for some reason). This points to the named reference `DynamicSpendingMonthly`, which you can see from the Name Manager points to the formula `=GetDynamicRange('Income and Spending Monthly'!$H$7, 'Income and Spending Monthly'!$H:$H, 1)` (all cell references in the name manager must be absolute references i.e. `$H` must be used in place of `H`). Now, there's still one more layer of indirection: `GetDynamicRange` isn't a built in Excel function, it's a custom function. See Custom Functions below for how these work.

It's worth noting that the process of referencing named formulas in charts can be very fussy. For example, Excel will throw an annoying error (which doesn't even seem legitimate since everything seems to work fine) if you try to reference a name in a chart that refers to anything more complex than a single function (for example, a function multiplied by -1, or two functions added together). Incorporating the additional calculation into the source data to keep the named reference simple resolves the issue. 
## Custom Functions
Custom functions are extremely useful for reusing complex formulas. There are likely multiple ways to create custom functions, but the method I used was through Excel Labs https://www.microsoft.com/en-us/garage/profiles/excel-labs/. 

Once installed, you can open the Excel Labs pane by navigating to the Home toolbar and clicking Excel Labs on the far right:
![image](images/"Pasted image 20240223090713.png")
From here, select "Names" to see the `GetDynamicRange` custom formula:
![image](images/"Pasted image 20240223091141.png")
## Troubleshooting Dynamic Charts
Despite my best efforts, I still occasionally find issues with the dynamic charts in the dashboard sheets. Often these are due to small changes in pivot table filters which can mess up the dynamic range formulas described above. These formulas determine the cells of interest by looking at the number of cells in a column containing values minus a manual offset, so if you add a new cell containing a value to said column (like a new pivot table filter) then you need to subsequently increase the offset. To help troubleshoot these issues, each dashboard features a hidden table depicting a mirror of the formulas used to generate the series values. The table displays the formulas used by the chart and their results as shown below:
![image](images/"Pasted image 20240223091731.png")
This makes it much easier to identify inconsistencies in data and which formula and underlying intermediate sheets are creating the issue. To see these tables, simply unhide the columns to the right of the gray sections of the dashboards and re-hide them when you're done. 