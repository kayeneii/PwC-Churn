# Churn
This data analysis and customer retention report was created for the PricewaterhouseCooper (PwC) Job Simulation.

[Overview](#overview)
[Dataset](#dataset)
[Objectives](#objectives)
[Methods](#methods)
[Findings and Recommendations](#findings-and-recommendations)
[Visualizations](#visualizations)

## Customer Demography and Churn Metrics for PhoneNow 

### Overview
---
This project aims to analyze and report the churn data for a PhoneNow, to identify key metrics and trends. The goal is to understand customer demography, track account information, identify key trends in subscription services, and visually communicate these in a manner that best helps customer retention at PhoneNow.


### Dataset
---
The dataset used in generating this report was the Churn Dataset.xlsx provided by the _PricewaterhouseCooper_ (PwC) Power BI Internship Program. For more info, see [Forage](https://www.theforage.com/virtual-experience/a87GpgE6tiku7q3gu/pw-c-switzerland/power-bi-cqxg/introduction).

### Objectives
---
To derive answers to the following questions:
  - What is the percentage of customers that signed up for:
       * Phone Services
       * Multiple Lines
       * Internet Services
       * Online Security
       * Online Backup
       * Device Protection
       * Tech Support
       * Streaming TV and
       * Streaming Movies
  - How long as a customer been subscribed?
  - What is the total number of customers per contract?
  - What is the most popular payment method?
  - How many customers use paperless billing? 
  - What is the overall monthly charges?
  - What is the total annual charges?
  - What is the total number of tickets opened in:
      * Administrative
      * Technical 
  - What is the customer distribution by gender?
  - How many have partners?
  - How many have dependents?
  - What percentage of customers are senior citizens?
    
### Methods
---
The following tools were used in the creation of this report.
1. **Microsoft Excel:** For data cleaning and preparation, initial exploration, and visualization.
  * Data Cleaning and Preparation:
    - Data loading and inspection
    -  Data cleaning
       
2. **Microsoft Power BI:** For,
  * Further Data Processing:
    - Data loading and quality inspection
    -  Data transformation and formatting

  * Data Analysis: During the analysis, the following conditional columns were created in the Power Query:

  = **Contract Count**
	
 ```DAX 
	= If Contract equals Two year Then 2
	Else if Contract equals One year Then 1
	Else 0
```
	
   = **Loyalty**
	
```DAX 
	= If tenure is less than 12 Then <1 Year
	Else if tenure is less than 24 Then <2 Years
	Else if tenure is less than 36 Then <3 Years
	Else if tenure is less than 48Then <4 Years
	Else if tenure is less than 60 Then <5 Years
	Else <6 Years
```
	
   = **Internet Service Count**

```DAX 
	= If InternetService equals DSL Then 1
	Else if InternetService equals Fiber optic Then 2
	Else 0
```

   = **Payment Method Count**
	
```DAX 
	= If PaymentMethod contains Electronic Then 1
	Else if PaymentMethod contains Bank Then 2
	Else if PaymentMethod contains Credit Then 3
	Else 0
```

   = **Internet Service**

```DAX
	If InternetService does not contain No Then Yes
	Else No
```

   = **PaperlessBilling Count**
	
```DAX
	If PaperlessBilling equals Yes Then 1
	Else 0
```

 
 Several measures were also derived:
   - To get the percentage value of churns.
		
```DAX
Churn Rate = DIVIDE(CALCULATE(COUNT('Churn-Dataset'[Churn]), 'Churn-Dataset'[Churn] = "Yes"), CALCULATE(COUNT('Churn-Dataset'[Churn]), ALLSELECTED('Churn-Dataset'[Churn])))
```

  - To get total count of churn
		
```DAX
Total Churn = CALCULATE(COUNTA('Churn-Dataset'[Churn]), 'Churn-Dataset'[Churn] = "Yes")
```

  - To get total count of Device Protection
		
```DAX
Active Device Protection = CALCULATE(COUNTA('Churn-Dataset'[DeviceProtection]), 'Churn-Dataset'[DeviceProtection] ="Yes")
```	

  - To get total count of Phone Service
		
```DAX
Active Phone Service = CALCULATE(COUNTA('Churn-Dataset'[PhoneService]), 'Churn-Dataset'[PhoneService] = "Yes")
```	

  - To get total count of Online Security
	
```DAX
Active Online Security = CALCULATE(COUNTA('Churn-Dataset'[OnlineSecurity]), 'Churn-Dataset'[OnlineSecurity] = "Yes")
```	
	    
  - To get total count of Online Backup
	
```DAX
Active Online Backup = CALCULATE(COUNTA('Churn-Dataset'[OnlineBackup]), 'Churn-Dataset'[OnlineBackup] = "Yes")
```
  - To get total count of Multiple Lines
		
```DAX
Active Multiple Lines = CALCULATE(COUNTA('Churn-Dataset'[MultipleLines]), 'Churn-Dataset'[MultipleLines] = "Yes")
```	

  - To get total count of Active Tech Support
		
```DAX
Active Tech Support = CALCULATE(COUNTA('Churn-Dataset'[TechSupport]), 'Churn-Dataset'[TechSupport] = "Yes")
```	

  - To get total count of active StreamingTV
		
```DAX
Total StreamingTV = CALCULATE(COUNTA('Churn-Dataset'[StreamingTV]), 'Churn-Dataset'[StreamingTV] = "Yes")
```	

  - To get total count of active StreamingMovies
	
```DAX
Total StreamingMovies = CALCULATE(COUNTA('Churn-Dataset'[StreamingMovies]), 'Churn-Dataset'[StreamingMovies] = "Yes")
```	

  - To get total count of PaperlessBilling

```DAX
Total PaperlessBilling = CALCULATE(COUNTA('Churn-Dataset'[PaperlessBilling]), 'Churn-Dataset'[PaperlessBilling] = "Yes")
```

  - To get percentage value of Dependents
		
```DAX
%Dependents = DIVIDE(CALCULATE(COUNT('Churn-Dataset'[Dependents]), 'Churn-Dataset'[Dependents] = "Yes", 'Churn-Dataset'[Churn] = "Yes"), CALCULATE(COUNT('Churn-Dataset'[Dependents]), 'Churn-Dataset'[Churn] = "Yes"), 0)
```	
	    
  - To get percentage value of Active Multiple Lines
		
```DAX
%Active Multiple Lines = DIVIDE(CALCULATE(COUNT('Churn-Dataset'[MultipleLines]), 'Churn-Dataset'[MultipleLines] = "Yes", 'Churn-Dataset'[Churn] = "Yes"), CALCULATE(COUNT('Churn-Dataset'[MultipleLines]), 'Churn-Dataset'[Churn] = "Yes", 'Churn-Dataset'[MultipleLines] <> "No phone service"), 0)
```	

  - To get percentage value of No Multiple Lines
		
```DAX
%No Multiple Lines = DIVIDE(CALCULATE(COUNT('Churn-Dataset'[MultipleLines]), 'Churn-Dataset'[MultipleLines] = "No", 'Churn-Dataset'[Churn] = "Yes"), CALCULATE(COUNT('Churn-Dataset'[MultipleLines]), 'Churn-Dataset'[Churn] = "Yes", 'Churn-Dataset'[MultipleLines] <> "No phone service"), 0)
```	

  - To get percentage value of Active Device Protection
		
```DAX
%Active Device Protection = CALCULATE(COUNTA('Churn-Dataset'[DeviceProtection]), 'Churn-Dataset'[DeviceProtection] ="Yes")  / 7043
```
	
  - To get percentage value of Active Phone Service
		
```DAX
%Active Phone Service = DIVIDE(CALCULATE(COUNT('Churn-Dataset'[PhoneService]), 'Churn-Dataset'[PhoneService] = "Yes", 'Churn-Dataset'[Churn] = "Yes"), CALCULATE(COUNT('Churn-Dataset'[PhoneService]), 'Churn-Dataset'[Churn] = "Yes"), 0)
```	

  - To get percentage value of Active Online Backup
		
```DAX
%Active Online Backup = DIVIDE(CALCULATE(COUNT('Churn-Dataset'[OnlineBackup]), 'Churn-Dataset'[OnlineBackup] = "Yes", 'Churn-Dataset'[Churn] = "Yes"), CALCULATE(COUNT('Churn-Dataset'[OnlineBackup]), 'Churn-Dataset'[Churn] = "Yes"), 0)
```

 - To get percentage value of Active Online Security
		
```DAX
%Active Online Security = DIVIDE(CALCULATE(COUNT('Churn-Dataset'[OnlineSecurity]), 'Churn-Dataset'[OnlineSecurity] = "Yes", 'Churn-Dataset'[Churn] = "Yes"), CALCULATE(COUNT('Churn-Dataset'[OnlineSecurity]), 'Churn-Dataset'[Churn] = "Yes"), 0)
```
	
  - To get percentage value of Active Tech Support
		
```DAX
%Active Tech Support = DIVIDE(CALCULATE(COUNT('Churn-Dataset'[TechSupport]), 'Churn-Dataset'[TechSupport] = "Yes", 'Churn-Dataset'[Churn] = "Yes"), CALCULATE(COUNT('Churn-Dataset'[TechSupport]), 'Churn-Dataset'[Churn] = "Yes"), 0)
```
	
  - To get percentage value of Active Streaming TV
	
```DAX
%Active StreamingTV = DIVIDE(CALCULATE(COUNT('Churn-Dataset'[StreamingTV]), 'Churn-Dataset'[StreamingTV] = "Yes", 'Churn-Dataset'[Churn] = "Yes"), CALCULATE(COUNT('Churn-Dataset'[StreamingTV]), 'Churn-Dataset'[Churn] = "Yes"), 0)
```	
	 
  - To get percentage value of Active StreamingMovies
	
```DAX
%Active StreamingMovies = DIVIDE(CALCULATE(COUNT('Churn-Dataset'[StreamingMovies]), 'Churn-Dataset'[StreamingMovies] = "Yes", 'Churn-Dataset'[Churn] = "Yes"), CALCULATE(COUNT('Churn-Dataset'[StreamingMovies]), 'Churn-Dataset'[Churn] = "Yes"), 0)
```
	
  - To get percentage value of Active Internet Service
  	
```DAX
%Active Internet Service = SUM(COUNT('Churn-Dataset'[InternetService]), 'Churn-Dataset'[InternetService] ="Yes")  / 7043
```

  - To get percentage value with Partner
	
```DAX
%Partner = DIVIDE(CALCULATE(COUNT('Churn-Dataset'[Partner]), 'Churn-Dataset'[Partner] = "Yes", 'Churn-Dataset'[Churn] = "Yes"), CALCULATE(COUNT('Churn-Dataset'[Partner]),'Churn-Dataset'[Churn] = "Yes"), 0)
```	

  - To get percentage value of Senior Citizens
	
```DAX
%Senior Citizens = SUM('Churn-Dataset'[SeniorCitizen]) / 7043
```	

  - To get percentage value of Active Tech Support
		
```DAX
%Active Tech Support = DIVIDE(CALCULATE(COUNT('Churn-Dataset'[TechSupport]), 'Churn-Dataset'[TechSupport] = "Yes", 'Churn-Dataset'[Churn] = "Yes"), CALCULATE(COUNT('Churn-Dataset'[TechSupport]), 'Churn-Dataset'[Churn] = "Yes"), 0)
```


   * Data Visualizations: Cards, Bar, Pie and Donut Charts was used to visually plot out the subscription service rates,  customer account and demographic information, among other summarized data.

3. **GitHUb:** For,
   - Portfolio Building
   - Communication


### Findings and Recommendations
---
1. **Findings:** Following the conclusive analysis of the Churn Dataset, the following findings were made:
    * The percentage of customers that signed up for: 
          - Phone Services was 90.90%
          - Multiple Lines was 50.03%
          - Internet Services was  93.95%
          - Online Security was 15.78%
          - Online Backup was 27.98%
          - Device Protection was 34.39%
          - Tech Support was 16.59%
          - Streaming TV was 43.55%
          - Streaming Movies was 43.77%
    * 7% of the customers have been subscribed for less than 6 years, 15% for less than 5 years, 20% for less than 4 years, 22% for less than 3 years, 30% for less than 2 years, and 48% for less than a year.
    * 3.88K are monthly contractors, while 1.7K two-year contractors and 1.47K are yearly contractors.
    * More customers pay via 'Electronic Check'.
    * 4,171 customers use paperless billing. 
    * The overall monthly charge is 456.12K
    * Total annual charge is 16 Million.
    * Total number of tickets opened in:
         - Administrative is 3,632
         - Technical is 2,955
    * 49.5% of customers are female customers while 50.5% are male.
    * Of the total 7,043 customers, 16.21% are Senior Citizens.
    * 17.44% have dependents.
    * 35.79% have partners.

2. **Recommendations:**
   - Make subscription services more accessible and inclusive for the senior citizens.
   - Create a marketing and sales strategy that improves subscription rate to at least 60% across all services. Only Phone and Internet Services seem to have excellent rates.
   - Take customer survey on customer satisfaction with services provided and suggestions for improvement.
   - Conduct a deep research to discover why customer subscription drops after the first year period. This might have to do with the 'free-trial' offered.
   - Ensure seamless electronic billing services as the more customers prefer paperless billing.


### Visualizations
---
![Visual](https://github.com/kayeneii/Churn/blob/main/PWC_Churn-Metrics_1.png)
