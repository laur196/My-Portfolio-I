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

