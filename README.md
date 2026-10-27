# InsightReach | Customer & Restaurant Analytics

## Project Context

This project addresses the optimization of segmentation strategies in the field of digital marketing, using the company InsightReach as the subject of study. In the context of its current phase of scalability and market diversification, the study proposes a technical evaluation model based on data science. The central objective is to demonstrate the methodological feasibility of integrating multiple data sources and predictive analytics to generate actionable insights and sustainable competitive advantages.

## Structure:
```
InsightReach-analysis/
├── data/
│   └── base_datos_restaurantes_USA_v2/         #source
│
└── docs/
│   └── Recomendations.md                       #Segmentation proposals
│
├── notebooks/
│   └── 01_EDA.ipynb                            #InsightReach database, data cleaning using ETL techniques, and variable charting
│   └── 02_API_YELP.ipynb                       #External Yelp API database, complementary table for analysis.
│
└── README.pdf                                  #Steps and results
```


## Steps and Considerations for EDA

These steps apply to both Avance_1_EDA.ipynb and Avance_API_Yelp.ipynb.

> _Library Import_

Import necessary libraries: Numpy, Pandas, Seaborn, Matplotlib.

> _Data Import_

Load the file "Raw_Data/base_datos_restaurantes_USA_v2.csv" and verify that it loaded correctly by checking the first five rows.

> _Data Verification_

Use the .info() function to check variable types and missing data. Initial inspection identifies missing data in edad, promedio_gasto_comida, preferencias_alimentarias, telefono, and correo electrónico. Duplicates will be removed, and outliers will be converted into null values before deciding whether to impute or drop them. Convert the data type of edad to an integer.

> _Duplicates Review_

Check for duplicate clients in the dataset using id_persona as a reference.
Since no duplicate client records are found, no action is taken. If found in other datasets, a code block can be added within this section.

> _Data Cleaning_

Use the .describe() function for a general analysis of min, max, quartiles, mean, and standard deviation.

Findings: Age and frequency fields should not contain negative numbers. Age should have an upper threshold limit of up to 100 years. Outliers such as -5 and 300 for age, as well as negative frequency values, are found; conditional statements are applied to set these values to null.

Verify city spelling to avoid double-counting.

> _Null Values_

Since this is a small dataset of 3,000 clients, and missing values account for less than 10%, values in edad, frecuencia_visita, and promedio_gasto_comida will be imputed with the median to avoid losing monthly income data (ensuring future datasets are not negatively affected if data bias exists).
For Correo_electronico and telefono, missing fields will be imputed with the value "Desconocido" to avoid filling in false or incorrect information.

> _String Data Standardization_

Convert text data to standardized string format to streamline analysis and prevent data entry errors. Applied across all string columns except contact phone numbers and email addresses.

> _Filtering by City_

Display the list of cities and select "denver". Create a copy of the dt_restaurant dataframe into a new one named dt_restaurant_filtered to avoid conflicts in the original dataset when aggregating columns.

### *Preliminary Tables for Analysis*

1. Gender Distribution: Gender distribution in the city of Denver is nearly equal, differing by only about 1%. Therefore, it is ruled out as a determining or causal factor for other variables.

2. Age Distribution: The age table shows an even distribution between 7% and 10% across all age ranges from 18 to 80. Consequently, it is not considered a determining or causal factor for other variables either.

3. Dietary Preferences: Meat (25%) and vegetarian food (24.8%) account for 49.9% of diners' dietary preferences.

4. Socio-Economic Level: 63.8% of diners belong to the middle (30.3%) and high (33.6%) socio-economic strata.

5. Visit Frequency & Channels: 42.8% of people visit restaurants 4–5 times a month. Contrasting this with Yelp data, only 7% of diners physically visit restaurants. 56% prefer delivery options, and 45.6% prefer takeout (pickup on site), making these critical factors to consider for new restaurant sales strategies in Denver.

6. Spending: 74.6% of diners' average spending ranges from $0 to $45 USD, providing an idea of product pricing based on current trends.

7. Income: 30.1% earn between $800 and $2,233 USD per month, while 21.1% earn between $2,233 and $3,665 USD per month.

8. Alcohol Consumption: 59.5% of diners consume alcohol, ruling it out as a determining or causal factor over other variables.