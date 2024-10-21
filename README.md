# Credit_Card_Financial_Dashboard
Power Bi Dashboard
#Project Objective:
To develop a comprehensive credit 
card weekly dashboard that 
provides real-time insights into key 
performance metrics and trends, 
enabling stakeholders to monitor 
and analyze credit card operations 
effectively.




#DAX Queries:
AgeGroup = SWITCH(
    TRUE(),
    'ccdb cust_detail'[Customer_Age]<30,"20-30",
    'ccdb cust_detail'[Customer_Age]>=30 && 'ccdb cust_detail'[Customer_Age]<40,"30-40",
    'ccdb cust_detail'[Customer_Age]>=40 && 'ccdb cust_detail'[Customer_Age]<50,"40-50",
    'ccdb cust_detail'[Customer_Age]>=50 && 'ccdb cust_detail'[Customer_Age]<60,"50-60",
    'ccdb cust_detail'[Customer_Age]>=60,"60+",
    "Unkown")
    
IncomeGroup = SWITCH(
    TRUE(),
  'ccdb cust_detail'[Income]<35000,"Low",
  'ccdb cust_detail'[Income]>=35000 && 'ccdb cust_detail'[Income]<70000,"Med",
  'ccdb cust_detail'[Income]>=70000,"High",
  "Unkown")

Revenue = 'ccdb cc_detail'[Annual_Fees]+'ccdb cc_detail'[Total_Trans_Amt]+'ccdb cc_detail'[Interest_Earned]

Week_num2 = WEEKNUM('ccdb cc_detail'[Week_Start_Date])

Current_week_Revenue = CALCULATE(
    SUM('ccdb cc_detail'[Revenue]),
    FILTER(
        ALL('ccdb cc_detail'),
        'ccdb cc_detail'[Week_num2]=MAX('ccdb cc_detail'[Week_num2])))


Previous_week_Revenue = CALCULATE(
    SUM('ccdb cc_detail'[Revenue]),
    FILTER(
        ALL('ccdb cc_detail'),
        'ccdb cc_detail'[Week_num2]=MAX('ccdb cc_detail'[Week_num2])-1))

Wow_Revenue = DIVIDE([Current_week_Revenue]-[Previous_week_Revenue],[Previous_week_Revenue])


#Project Insights- Week 53 (31st Dec):
WoW change: 
• Revenue increased by 28.8%, 
• Total Transaction Amt & Count increased by 35.04% & 3.39%
• Customer count increased by 28.31%
Overview YTD:
• Overall revenue is 57M
• Total interest is 8M
• Total transaction amount is 46M
• Male customers are contributing more in revenue 31M, female 26M
• Blue & Silver credit card are contributing to 93% of overall 
transactions
• TX, NY & CA is contributing to 68%
• Overall Activation rate is 57.5%
• Overall Delinquent rate is 6.06%


