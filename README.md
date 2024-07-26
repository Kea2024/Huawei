# Huawei

## Table of Contents

- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Data Loading and Inspections](#data-loading-and-inspections)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results/Findings](#results-findings)
- [Recommendations](#recommendations)
- [Limitations](limitations)

### Project Overview

The goal is to make a report in Power BI out of Google’s Play Store dataset which will be used to report during a business review to find and talk through competitor insights together with the leadership team that’s attending.

![Screenshot 2024-07-26 114017](https://github.com/user-attachments/assets/5fa116e9-640a-4970-9fb0-449aade66a4e)


### Data Source

Sales Data: The priamry source for this data is " Google Play Store Data.xlsx" file containing detailed information about the app.

### Tools

Power BI - Data cleaning, Analysis and Creating Reports

### Data Loading and Inspections

- Importing the dataset by creating a new table and the filling out the data
- Handling missing values
- Data cleaning and formatting

### Exploratory Data Analysis

EDA involved exploring the sales data to answer key questions such as:

1. What year has the highest profit from the app?
2. What platform gained the highest review and install?
3. What age group are most likely to install the app?

### Data Analysis

Power BI

```
 Source = Excel.Workbook(File.Contents("C:\Users\kea\Downloads\Google Play Store data.xlsx"), null, true),

= Source{[Item="googleplaystore",Kind="Sheet"]}[Data],

= Table.PromoteHeaders(googleplaystore_Sheet, [PromoteAllScalars=true]),

= Table.TransformColumnTypes(#"Promoted Headers",{{"App", type text}, {"Category", type text}, {"Rating", type number}, {"Reviews", Int64.Type}, {"Size (in megabytes)", type any}, {"Installs", Int64.Type}, {"Type", type text}, {"Price (in USD)", Int64.Type}, {"Content Rating", type text}, {"Genres", type text}, {"Last Updated", type date}, {"Current Ver", type any}, {"Android Ver", type text}}),

= Table.ReplaceValue(#"Changed Type",#nan,0,Replacer.ReplaceValue,{"Rating"}),

= Table.ReplaceValue(#"Replaced Value",#nan,0,Replacer.ReplaceValue,{"Rating"}),

= Table.SelectRows(#"Replaced Value1", each [Rating] <> null and [Rating] <> ""),

= Table.TransformColumnTypes(#"Filtered Rows",{{"Rating", type text}}),

= Table.ReplaceValue(#"Changed Type1","NaN","0",Replacer.ReplaceText,{"Rating"}),

= Table.TransformColumnTypes(#"Replaced Value2",{{"Rating", type number}}),

= Table.AddColumn(#"Changed Type2", "year updated", each [Last Updated]),

= Table.TransformColumns(#"Added Custom", {{"year updated", each Text.End(Text.From(_, "en-PH"), 4), type text}}),

= Table.SelectRows(#"Extracted Last Characters", each true)
in

= Filtered Rows1"
```

### Results/Findings:

The analysis results are summarized as follows:
1. ﻿At 4876, 2018 had the highest Sum of Price (in USD) and was Infinity higher than 2010, which had the lowest Sum of Price (in USD) at 0.
2. ﻿Facebook gained the highest review and install with 78M reviews.
3. ﻿The age group that most likely to install the app is EVERYONE with 81.8% and 52B installs, followed by TEEN with 14.08% rating and 20B installs

### Recommendations:

Based from the given data, it is recommended to innovate apps suitable for adults to increase the sales number of installs in this particular age bracket.

### Limitations

Most of the data were identified as "everyone". This causes confusion on what age bracket does this category belong and affects the data on identifying clearly what age bracket is being referred to.
