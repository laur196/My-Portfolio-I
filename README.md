# Investment Efficiency and Market Dynamics in the Global Unicorn Community: An Analysis of ROI Patterns and Industry Performance (2012-2022)

## Problem Statement
Easy Currency is a financial platform that offer financial services to the public. With various ROI across sectors and funding, the operations team were interested in investigating how investment is efficient across sectors and what geographic region play a vital role in unicorn community. The team decide to design a trend chart to enable investors and stakeholders get an insight into which sectors, region and investment strategies delivers returns while managing risk in a competitive market.
The project has important key metrics like valuation, funding, industry, top investors, geographic region and year founded.
This project was carried out to understand how industries, companies in various geographic regions performed from 2012-2022. 

## Project question

Here are the project objectives;

	Identify industries and investors that demonstrate the highest ROI in the unicorn community?

	Investigate how geographic region complement ROI and valuation?

## Data Structure 
This Dataset contains important metrics such as valuation, funding and select investors from 2012 to 2022.

	Factunicorn: This dataset contains key metrics such as funding, Valuation, Select Investors, industry, company, Geographic region. 

Metrics calculated for this table are : ROI(Divide(Total valuation-Total funding, Total funding), No of Unicorn(COUNTROWS(FILTER(FACT_Unicorn, FACT_Unicorn[valuation] >= 1000000000), Average Valuation(Average (FACT_Unicorn[Valuation])

	DimDate: The table contains column with day, weeks, months, month year and year.

![Unicorn data structure](https://github.com/laur196/My-Portfolio-I/blob/main/Unicorn%20Diagram.png)


## Technical Details 
This project used Power BI for all stages of data cleaning and analysis, with a focus on unicorn ROI across Industries and continent between 2012 and 2022.

## Skill Details
Skills: Format, Calculate, Aggregate Function(Sum, Divide, AVERAGEX)

Steps Details
Initial Inspection: Checked all source tables (DimDate, FactUnicorn) for missing values, duplicate entries and inconsistent data types.
Cleaning & Standardization: Converted Types, Renamed Columns, removed Duplicate.
Calculated Metrics: ROI, Average Valuation, No. of Unicorn.

## Data Cleaning Action
Here are the key cleaning operation
	Removed Duplicate
Purpose: A company name appeared twice but the difference was the location. I had to place the company side by side with their location and this enabled me avoid duplicate.

	Renamed Column
Purpose: To understand my table better while I removed duplicate, I had to rename the row ‘company 2’ back to it initial name ‘Company’.

	Converted Types
Purpose: Valuation and funding columns were converted from text to numbers in other to make calculation possible for accurate analysis.

## Date Table Details
The date was inserted into the StartDate and the last day was inserted as the EndDate and this helped to create a date table which contains day, week, month, month year, Quarter year, year.  
Steps Details
The date table was created through this method;
let 
// Create parameter 
    StartDate = List.Min(FACT_Unicorn[Date Joined]),
    EndDate = List.Max(FACT_Unicorn[Date Joined]),
    Step = Duration.Days(EndDate - StartDate)+1, 
// Create the List of date
    Source = List.Dates(StartDate,Step, #duration(1,0,0,0)), 
    #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    #"Changed Type" = Table.TransformColumnTypes(#"Converted to Table",{{"Column1", type date}}),
    #"Renamed Columns" = Table.RenameColumns(#"Changed Type",{{"Column1", "Date"}}),
// Create additional columns 
    #"Inserted Year" = Table.AddColumn(#"Renamed Columns", "Year", each Date.Year([Date]), Int64.Type),
    #"Inserted Quarter" = Table.AddColumn(#"Inserted Year", "Quarter", each Date.QuarterOfYear([Date]), Int64.Type),
    #"Inserted Quarter Year" = Table.AddColumn(#"Inserted Quarter", "Quarter Year", each Text.Combine({"Q", Text.From([Quarter], "en-US"), " ", Text.From([Year], "en-US")}), type text), 
    #"Inserted Month" = Table.AddColumn(#"Inserted Quarter Year", "Month", each Date.Month([Date]), Int64.Type),
    #"Inserted Month Name" = Table.AddColumn(#"Inserted Month", "Month Name", each Text.Start(Date.MonthName([Date]),3), type text),
    #"Inserted Month Year" = Table.AddColumn(#"Inserted Month Name", "Month Year", each Text.Combine({[Month Name], " ", Text.From([Year], "en-US")}), type text),
    #"Inserted Month Year S" = Table.AddColumn(#"Inserted Month Year", "Month Year S", each Text.Combine({Text.From([Year], "en-US"), Text.PadStart(Text.From([Month], "en-US"), 2, "0")}), type text),
    #"Inserted End of Month" = Table.AddColumn(#"Inserted Month Year S", "End of Month", each Date.EndOfMonth([Date])),
    #"Inserted Week Day Name" = Table.AddColumn(#"Inserted End of Month", "Week Day", each Text.Start(Date.DayOfWeekName([Date]),3), type text),
    #"Inserted Day of Week" = Table.AddColumn(#"Inserted Week Day Name", "Day of Week", each Date.DayOfWeek([Date]), Int64.Type),
    #"Inserted Day" = Table.AddColumn(#"Inserted Day of Week", "Day", each Date.Day([Date]), Int64.Type),
    #"Inserted Week of Month" = Table.AddColumn(#"Inserted Day", "Week of Month", each Date.WeekOfMonth([Date]), Int64.Type),
    #"Inserted Week of Month W" = Table.AddColumn(#"Inserted Week of Month", "Week", each Text.Combine({"W", Text.From([Week of Month], "en-US")}), type text),
    #"Inserted Week of Year" = Table.AddColumn(#"Inserted Week of Month W", "Week of Year", each Date.WeekOfYear([Date]), Int64.Type),
    #"Inserted Week of Year W" = Table.AddColumn(#"Inserted Week of Year", "Week of Year W", each Text.Combine({"W", Text.From([Week of Year], "en-US")}), type text),
    #"Added Fiscal Month" = Table.AddColumn(#"Inserted Week of Year W", "Fiscal Month", each if Date.Month([Date]) <= 3 then Date.Month([Date]) + 9 else Date.Month([Date]) - 3),
    #"Added Fiscal Year" = Table.AddColumn(#"Added Fiscal Month", "Fiscal Year", each if Date.Month([Date]) <= 3 then Date.Year([Date]) else Date.Year([Date]) + 1),
    #"Added Fiscal Quarter" = Table.AddColumn(#"Added Fiscal Year", "Fiscal Quarter", each Number.RoundUp([Fiscal Month]/3))
in
    #"Added Fiscal Quarter"

    ## Executive Summary
    
Despite the high funding, Fintech sector leads in both the number of unicorn and ROI, making it a sector for investment. The analysis also identifies Tiger Global Management and Sequoia Capital China as the most investors, which identify as high-growth companies. Around 2013-2014 ROI peaked at nearly100% but declined by 500% in 2022 which is as a result of a competitive market. North America and Asia dominated the unicorn community which indicate an innovative community. Tiger global management ranks as the top investor concentrating on funding power among top-tier firms. 
While there is a positive relationship between total funding and total ROI, the highest ROI does not always correlate with the highest funding. For example, while ByteDance has a higher valuation, Stripe and Klarna show good ROI despite lower total funding.

## Key Insight

	Fintech leads with 716% ROI exceeding the average of 469.76% establishing it as the most lucrative sector while Supply chain/logistics shows 298% ROI . 
	ByteDance shows good valuation-to-funding ratios, while Stripe and Klarna show good ROI despite lower total funding.
	North America and Asia lead the global unicorn community in total valuation and funding, which indicate hubs for high-growth tech companies. 
	Tiger global management ranks as the top investor concentrating on funding power among top-tier firms followed by Sequoia capital China, SIG Asia investment, Sina weibo and Softbank Group.

## Recommendation

	Identify industries and investors that demonstrate the highest ROI in the unicorn community?
Prioritize every sector by focusing on investment strategies on industries showing both high ROI and sustainable growth patterns such as Fintech, Internet software, and AI sectors which consistently deliver ROI  greater than 500%.
	Investigate how geographic region complement ROI and valuation?
There is need for markets diversification in regions like North America and Asia. Explore emerging unicorn to capture early-stage opportunities is a form of geographic diversification.




![Unicorn Dashboard](https://github.com/laur196/My-Portfolio-I/blob/main/An%20Analysis%20of%20ROI%20Patterns%20and%20Industry%20Performance%20(2012-2022).JPG)

![Unicorn Dashboard](https://github.com/laur196/My-Portfolio-I/blob/main/An%20Analysis%20of%20ROI%20Patterns%20and%20Industry%20Performance%20(2012-2022)%20II.JPG)

