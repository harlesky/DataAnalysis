# Data Analyst Job Market Analysis

## Overview
Welcome to my analysis of the data job market, focusing on data analyst roles. This project was created out of a desire to navigate and understand the job market more effectively. It delves into the top-paying and in-demand skills to help find optimal job opportunities for data analysts.

The dataset is sourced from Luke Barousse's Python Course, providing a foundation for my analysis. It contains detailed information on job titles, salaries, locations, and essential skills. Through a series of Python scripts, I explore key questions such as:
- What are the most demanded skills for data analysts?
- How are these skills trending over time?
- How well do jobs and skills pay for data analysts?
- What are the optimal skills for data analysts to learn (high demand & high pay)?

## The Questions
Below are the key questions I explore in this project:
1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand & High Paying)

## Tools Used
For this analysis, I utilized the following tools:
- **Python**: The core language used for data analysis.
- **Pandas**: For data manipulation and cleaning.
- **Matplotlib**: For data visualization.
- **Seaborn**: To create advanced and aesthetically pleasing visuals.
- **Jupyter Notebooks**: To run Python scripts interactively and document findings.
- **Visual Studio Code**: For executing Python scripts.
- **Git & GitHub**: For version control and sharing the project.

## Data Preparation and Cleanup
### Importing and Cleaning Data
I start by importing the necessary libraries and loading the dataset. Initial data cleaning steps ensure accuracy and usability.

```python
import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt  

# Load dataset
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

# Convert job_posted_date to datetime
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])

# Convert job_skills from string to list
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```

### Filtering for US Jobs
To focus the analysis on the U.S. job market:
```python
df_US = df[df['job_country'] == 'United States']
```

## The Analysis
### 1. Most Demanded Skills for the Top 3 Data Roles
To determine the most demanded skills for the top 3 data roles, I identified the most popular job titles and extracted their top 5 skills.

#### Visualization
```python
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
```

#### Insights
- **SQL** is the most requested skill for Data Analysts and Data Scientists.
- **Python** is highly demanded across all roles but particularly important for Data Scientists and Data Engineers.
- Data Engineers require specialized technical skills (AWS, Azure, Spark), while Data Analysts and Data Scientists need general data management tools (Excel, Tableau).

### 2. Trends in In-Demand Skills for Data Analysts
To analyze skill trends in 2023, I grouped skills by month of job postings.

#### Visualization
```python
from matplotlib.ticker import PercentFormatter
sns.lineplot(data=df_DA_US_percent.iloc[:, :5], dashes=False, legend='full', palette='tab10')
plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))
plt.show()
```

#### Insights
- **SQL** remains the most consistently demanded skill but shows a slight decline over time.
- **Excel** increased in demand towards the end of the year.
- **Python and Tableau** remained stable but essential.

### 3. Salary Analysis for Data Jobs
To analyze salary distributions, I examined median salaries by role.

#### Visualization
```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)
plt.gca().xaxis.set_major_formatter(lambda y, pos: f'${int(y/1000)}K')
plt.show()
```

#### Insights
- **Senior Data Scientist** roles have the highest salary potential (~$600K in some cases).
- **Data Analyst salaries** are more consistent, with fewer high outliers.
- **Senior roles** (Data Scientists, Data Engineers) show a wider salary range, indicating higher pay potential with experience.

### 4. Optimal Skills for Data Analysts
To determine optimal skills (high demand & high pay), I analyzed demand percentage vs. median salary.

#### Visualization
```python
plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])
plt.show()
```

#### Insights
- **Oracle** offers the highest median salary (~$97K) despite lower demand.
- **Python, Tableau, and SQL Server** balance high demand and good salary potential.
- **Excel and SQL** are crucial for job postings but have lower salary leverage compared to specialized skills.

## Conclusion
This project provides key insights into the data analyst job market, highlighting in-demand skills, salary trends, and optimal skill combinations. Key takeaways include:
- **SQL, Python, and Excel** remain foundational for data analysts.
- **Specialized technical skills (AWS, Git, dplyr, Bitbucket) can lead to higher salaries.**
- **Tracking skill trends** helps professionals stay ahead in the job market.

For more details, explore my notebooks:
- **[2_Skill_Demand.ipynb](#)**: Most demanded skills analysis
- **[3_Skills_Trend.ipynb](#)**: Skill trends over time
- **[4_Salary_Analysis.ipynb](#)**: Salary insights
- **[5_Optimal_Skills.ipynb](#)**: High-demand & high-paying skills

---
Thank you for exploring my analysis! Feel free to check out the full project and code on [GitHub](#).

