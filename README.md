Credit Card Transaction and Customer Dashboard using Power BI
Initially SQL database were used to process and allign data then it was imported to Power BI for Data Processing and DAX queries. 
-- creating new column as Current_week_revenue
Current_week_revenue = CALCULATE(
    SUM('credit_card'[Revenue]),
    FILTER( 
        ALL('credit_card'),
        'credit_card'[Week_num2] = MAX('credit_card'[Week_num2])))
 -- create new column as Previous_week_revenue       
Previous_week_revenue = CALCULATE(
    SUM(credit_card[Revenue]),
    FILTER(
        ALL(credit_card),
        credit_card[Week_num2] = MAX(credit_card[Week_num2])-1))
  -- calculated revenue 
Revenue = credit_card[Annual_Fees] + credit_card[Total_Trans_Amt] + credit_card[Interest_Earned]     
  Week_num2 = WEEKNUM(credit_card[Week_Start_Date])
  -- created age group in customer table 
  AgeGroup = SWITCH(
    TRUE(),
    customer[Customer_Age] < 30, "20-30", 
    customer[Customer_Age] >= 30 && 'customer'[Customer_Age] < 40, "30-40",
    customer[Customer_Age] >= 40 && 'customer'[Customer_Age] < 50, "40-50",
    customer[Customer_Age] >= 50 && 'customer'[Customer_Age] < 60, "50-60",
    customer[Customer_Age] >= 60, "60+",
    "unknown"
    )
    -- created income group column in customer table 
    IncomeGroup = SWITCH(
    TRUE(),
    customer[Income] < 35000, "low", 
    customer[Income] >= 35000 && customer[Income] < 70000, "medium",
    customer[Income] >= 70000, "high",
    "unknown"
)
# WoW change in KPI'S of the data is the major part of analysis 
Revenue increased by given percentage 
total transaction amount and count increased can be easily seen at dashboard 
Change in customer count over week can easily analysized 
# Year to Date Overview are the lightened shade of project 
