# Health-Lifestyle-Analysis
### Project Overview
This project analyzes the relationship between sleep patterns, lifestyle choices, and health indicators using SQL. The dataset, sourced from Kaggle, contains information on sleep duration, quality, stress levels, BMI, physical activity, and health metrics. By using SQL queries, we extract key insights to understand how different factors impact sleep health.
### Data Source
The dataset used in this project is sourced from Kaggle.It contains information about sleep duration, sleep quality, lifestyle factors  and their impact on overall health.
### Tools
- Excel- cLeaning Data
- Sql Server- Data Analysis
- Power Bi- Creating Dashboard and Report
  
  ##  Data Cleaning & Preparation
  Before performing analysis, the dataset was cleaned and preprocessed to ensure accuracy and consistency. The key steps taken include:
  - Checked for missing values
  - Removed duplicate records
  - Standardized Data Formats
   -  Performed data integrity checks after cleaning.
     ### Exploratory Data Analysis
  After thorough cleaning the data, Exploratory Data Analysis  was performed to uncover trends, patterns, and relationships in sleep health and lifestyle factors and answer questions such as :
  - How many people fall into each BMI category?
  - Which occupation has the highest and lowest average sleep duration?
  - Who are the top 5 individuals with the highest daily steps?
  - How many people in each BMI category have sleep disorders?
  - How do individuals rank based on sleep quality and stress level?
  - What is the Average Heart Rate by BMI Category?
  - What is the  Running Total of Daily Steps per Person?
    ### Data Analysis
    
  ```sql SELECT `BMI Category`, count('person ID') as count
from sleepdata.sleep_health_and_lifestyle_dataset
group by `BMI Category`
order by count;
```

select Occupation, avg(`Sleep Duration`) as AVG_Sleep_Duration
from sleepdata.sleep_health_and_lifestyle_dataset
group by Occupation
Order by AVG_Sleep_Duration desc;

select `person ID`,`Daily Steps` as  `Highest Daily Steps`
from  sleepdata.sleep_health_and_lifestyle_dataset
order by  `Highest Daily Steps`
limit 5;

SELECT "Sleep Disorder", COUNT(*) AS count
FROM   sleepdata.sleep_health_and_lifestyle_dataset
WHERE "Sleep Disorder" IS NOT NULL 
GROUP BY "Sleep Disorder"
ORDER BY count DESC;


SELECT `Person ID`, `Sleep Duration`, `Quality of Sleep`, `Stress Level`
FROM  sleepdata.sleep_health_and_lifestyle_dataset
WHERE `Sleep Duration` < 6 AND `Quality of Sleep` < 5 AND `Stress Level` > 7;

WITH HeartRateStats AS (
    SELECT `BMI Category`, ROUND(AVG(`Heart Rate`), 2) AS avg_heart_rate
    FROM  sleepdata.sleep_health_and_lifestyle_dataset
    GROUP BY `BMI Category`
)
SELECT * FROM HeartRateStats
ORDER BY avg_heart_rate DESC;


SELECT `Person ID`, `Daily Steps`,
SUM(`Daily Steps`) OVER(PARTITION BY `Person ID` ORDER BY `Person ID`) AS running_total_steps
FROM   sleepdata.sleep_health_and_lifestyle_dataset;

Findings
1. Most people fall into the "Normal" category  of 195 people.
2. Overweight individuals (148) form the second-largest group, which suggests a significant portion of the dataset has higher BMI values.
3. Engineers (7.98 hrs), Lawyers (7.41 hrs), and Accountants (7.11 hrs) get the highest average sleep.
4.  Nurses (7.06 hrs) and Doctors (6.97 hrs) sleep less than Engineers and Lawyers , while Managers (6.9 hrs) also have lower sleep, likely due to stress and long working hours.
5.  The highest steps recorded are 3,300 steps, which suggests a sedentary lifestyle for most individuals in the dataset.
6.  Overweight individuals have the highest risk of both sleep apnea and insomnia.
7.  Obese individuals have the highest average heart rate  of 84.30 bpm while Normal BMI individuals have the lowest heart rate of 
68.73 bpm.
 Recommendations
Based on the analysis , I recommend the following actions:
1. Investigation of lifestyle factors that contribute to BMI variations
2. Examination of  stress levels across different occupations and Check if work shifts day/night impact sleep duration.
3. Cross-analysis of  sleep duration to see if overweight individuals sleep less overall.
4. Conducting  a lifestyle survey to understand why overweight individuals have the highest cases.
5. Investigation of blood pressure levels to assess cardiovascular risks in obese individuals.
6. Identification of stress reduction strategies for those with poor sleep quality.
Limitations
1. The dataset does not specify age, gender, or location, which could impact the analysis
2. Other factors may influence both sleep quality and BMI, but the dataset may not include these details.
3. Sleep quality depends on environmental factors (noise, screen time, caffeine intake), which are not in the dataset.
   
