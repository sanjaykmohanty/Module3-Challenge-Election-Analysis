# PyBer Analysis

## Overview 
The purpose of this project is to analyze ride-sharing data and crate a report to summarize how PyBer, a ride-sharing compay is performing in cities under urban, suburban and rural categories. The performance data for each city type and the recommendations from the analysis can help the decision-makers at PyBer to understand the differences which will help them in their future decision making process. 

The datasets used for this analysis are **City Data** and **Ride Data**. **City Data**. The **City Data** includes 'City Name',	'Driver Count', and 'Type of City (i.e. Urban, Suburban, and Rural)'. **Ride Data** includes 'City Name', Date of Ride',	'Fare', and 'Ride ID'. In exploring the datasets some of the questions need to answered are:

1. Total number of rides for each city type
2. Total number of drivers for each city type
3. Sum of the fares for each city type
4. Vverage fare per ride for each city type
5. Average fare per driver for each city type 

In adition to this, whatever insights can be gathered while exploring the datasets.

## Resources
Data Source: city_data.csv, ride_data.csv Software: Python 3.9.12, Jupyter Notebook 6.4.12 

## Data Exploration
The requirements described above was addressed in 2 steps.
1. Create a summary report with information by each city type.
2. Create a line chart that shows the total weekly of the fares for each type

### Summary Report
First, necessary python liberires were imported and datasets were lodaed into Pandas DataFrames. From a closer look at the data in the DataFrame, it was evident that the datasets need to be mergerd to get the required output.

Second, a new DataFrame was created after merging the two earlier DataFrames. The data in the new DataFrame is shown below.

![image](https://user-images.githubusercontent.com/31812730/192045183-96ae6809-39cd-41ef-b3e9-7614ebceb921.png)

Third, agregate functions were used against DataFrame columns to calculate the following:

**Total rides for each city type:**

![image](https://user-images.githubusercontent.com/31812730/192046952-7d877aee-5eca-4d23-9e49-3fea4c1cd65b.png)

**Total drivers for each city type:**

![image](https://user-images.githubusercontent.com/31812730/192047536-f47cb919-3e7e-4590-bd9d-6e64e96e37f7.png)

**Total amount of fares for each city type:**

![image](https://user-images.githubusercontent.com/31812730/192047749-6c560a05-33b7-4cdf-8eae-7c4a05241dff.png)

**Average fare per driver for each city type:**

![image](https://user-images.githubusercontent.com/31812730/192048127-dc0c8c99-3e74-4faf-b90f-06bbfb37ad18.png)

**Average fare per driver for each city type:**

![image](https://user-images.githubusercontent.com/31812730/192049617-6c105663-a114-4677-be22-09469d5f838f.png)

Finally, another new DataFrame is created using these calculated results. The columns are formatted to make them more readable. 

### Line Chart
The DataFrame created in the previous step by merging 'city data' and 'ryde data' DataFrames was also used to create this line chart. Following steps were followed to create the line chart:

To start with, a new DataFrame was created showing the city type, date, and sum of the fares for each date. 
![image](https://user-images.githubusercontent.com/31812730/192055403-7ddaeb13-f34b-4d75-9565-292543c9a33a.png)

Then, a pivot table was created with date as an index, fare as values and city types as columns. The date range was restricted from Jan-1-2019 to Apr-29-2019.

![image](https://user-images.githubusercontent.com/31812730/192058526-30c97a42-cb0e-4a15-a992-5c9ec6209568.png)

Next, the "date" index was set to datetime datatype.

![image](https://user-images.githubusercontent.com/31812730/192061158-e9a1178e-3403-484e-b44f-d304f551a864.png)

Afterwards, a new DataFrame was created using the "resample()" function by week ('W') to get the sum of the fares for each week.

![image](https://user-images.githubusercontent.com/31812730/192061685-b9b6af72-6135-4a63-b018-4ee6ae72d431.png)

In the end, the line chart was created using the resample DtaFrame. 

## Results
The summary report created from the the merged PayBer summary DataFrame to show the information of rides, drivers and fares for each city type.

![image](https://user-images.githubusercontent.com/31812730/192103917-900c3089-927c-45c6-a989-1ca542505aad.png)

Line Chart to show total fares for each city type during the period between January 1, 2019 and April 29, 2019 for each week. 

![image](https://user-images.githubusercontent.com/31812730/192103978-6a648463-925c-48fd-ae81-7b2272693493.png)


## Summary
The summary report shows that number of rides are the least (125) in the rural cities and are the most (1,625) in the urban cities. However, average fare per ride ($34.62) and average fare per driver (55.49) are more for the rural cities. it is possible that either the rides in rural cities are longer than the rides in urban and suburban cities or per mile fare cost is more in rural cities.

The total number of drivers (2,981) supporting PyBer business are 3% from the rural cities (78), 17% from the suburban cities (498), and 81% from the urban cities (2405).

The total revenue ($63,538.64) generated from these rides in terms of total fares is close to 7% from the rural cities ($4,327.93), about 30% from the suburban cities ($19,356.33), and approximately 63% from the urban cities ($39,854.38).

The driver to revenue ratio suggests that PyBer business is more profitable in rural cities than in the suburban and urban cities.

For all three city types, there is an increase in revenue from the rides during February third week.

Revenue from the urban cities reached its peak during February third week and March first week.

Revenue from the suburban cities reached its peak during February third week and headed towards peak during April 4th week.

Revenue from the rural cities reached its peak during March fourth week.

## Observations
There is substantial revenue drop between February third week and April fourth week for the suburban cities requires further investigation to understand the reason for this dip.

Similar investigation is required for the rural cities to understand the revenue drop between February third week and April first week.


