# Global Air Pollution Analysis

### Project Overview

This project aims to analyze the AQI values and categories of major pollutants globally. By analyzing air pollution data, I'm seeking to identify key patterns and relationships among major pollutant concentrations in regions around the world and gain a deeper understanding of how they vary.

### Data Sources

Global Air Pollution Data: The dataset for this analysis is the "global air pollution dataset.csv" file collected from eLichens, containing AQI value and category information for each pollutant (Ozone (O3), Carbon monoxide (CO), Nitrogen Dioxide (NO2), and Particulate Matter (PM2.5)) for each country and city documented.

### Tools

- Google Colab - Data Analysis
- Python - Data Analysis
- Powerpoint, Word - Documentation, Reporting


### Data Cleaning/Preparation

In the initial data preparation phase, I performed the following tasks:
1. Data loading and exploration. 
2. Handling missing values and outliers.
3. Resampling AQI categories.


### Exploratory Data Analysis

EDA involved exploring the pollution data to answer key questions such as:

- How do the AQI values among pollutants differ?
- Which pollutant has the highest maximum AQI value?
- Which countries have the highest average AQI values?
- Which country has the highest count of cities with an AQI value of 500?
- How do individual pollutant values correlate to the overall AQI and each other?

### Data Analysis

Include some interesting code/features worked with:

```python
#Average AQI by Country
import plotly.express as px
fig = px.choropleth(aqibycountry,
                    locations="Country",
                    locationmode="country names",
                    color="AQI Value",
                    hover_name="Country",
                    color_continuous_scale= "Turbo",
                    title='Average AQI by Country')
fig.show()
```
```python
#find the average AQI values for each country in the dataframe by grouping countries then calculating the average
aqibycountry = df.groupby('Country')['AQI Value'].mean().reset_index()

#Sort the data do the countries are listed from highest AQI average to lowest AQI average
aqibycountry_sorted = aqibycountry.sort_values(by='AQI Value', ascending=False)

#Print top 10 countries with the highest AQI values
top10 = aqibycountry_sorted.head(10)
print(top10)

#Print the bottom 10 countries with the lowest AQI values
lowest10 = aqibycountry_sorted.tail(10)
print(lowest10)
```
```python
#count the number of cities within each country that has experienced the maximum AQI of 500
maxaqi = df[df['AQI Value'] == 500][['Country', 'City', 'AQI Value']]
maxaqi['Country'].value_counts()
```

### Results/Findings
1. Particulate Matter (2.5) values are highly correlated with AQI values.
2. PM2.5 values are highly variable in comparison to the pollutants of the dataset. Ozone is the second most variable. The lack of variability in NO2 and CO made it difficult to determine if any regions are suffering more than others from high concentrations of NO2 and CO.
3. Support Vector Machine and Neural Networks are promising models for classifying AQI value data into AQI categories but have room for improvement.
4. Asia and Africa are disproportionately affected by high AQI levels.
5. Generally, higher AQI values are observed around the equator.

### Recommendations

Based on the analysis I recommend:
- Prioritize PM2.5 monitoring as the highest AQI values .
- Focus on preventative measures and policies for addressing unhealthy air pollution levels , especially in low- and middle- income countries.
- Attempting another resampling method on the data and refining the data models, particularly SVM, to address potential overfitting.

### Limitations
I had to remove a small percentage (less than 2%) of records because there were missing values in the country column which would have little value in the analysis considering the global scope of the dataset. Additionally, I removed the data for the Republic of Korea because there was only one recorded AQI value which was very high in comparison to the rest of the data.

