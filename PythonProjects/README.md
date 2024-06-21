# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles? 

To find the most demanded skills for the top 3 most popular data roles, I filtered out the top 3 demanded job positions by count, then filtered the top 5 skills needed for these top data roles. This question to be explored, highlights the most popular job titles and their top skills, showing which skills should be mastered by aspiring data analysts like myself.

View my notebook with detailed steps here: [2_Skill_Demand.ipynb](https://github.com/NicholasGalvan/Python/blob/main/PythonProjects/2_Skill_Demand.ipynb)

### Visualizing Data [1]
```python
# for Count of Top Skills 
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles): 
    df_plot = df_skills_count[df_skills_count['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_count', y='job_skills', ax=ax[i], palette='viridis')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].set_xlim(ax[0].get_xlim()) # setting the x limit for each graph to the maximum value between all, in this case the first graph has the highest counts
fig.suptitle('Counts of Top Skills in job Postings', fontsize=15)
plt.tight_layout()
plt.show()
```

### Visualizing Data [2]
```python 
# Likelihood of Skills Requested 
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles): 
    df_plot = df_skills_percent[df_skills_percent['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], palette='rocket', )
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].set_xlim(ax[0].get_xlim())# setting the x limit for each graph to the maximum value between all, in this case the first graph has the highest counts
    
    for index, value in enumerate(df_plot['skill_percent']): # adding the % sign to each bar in the figure
       ax[i].text(value , index, f'{value}%', va='center') # Adding text to the X and Y position where the value ends in the graph and adding a % 
    if i != len(job_titles) -1:  # removing all x labels except for the last graph 
        ax[i].set_xticks([])

fig.suptitle('Likelihood of Skills Requested in US Job Postings', fontsize=15)
plt.tight_layout()
plt.show()
```
### Results
![Data visualization for Top Skills in Data Jobs](https://github.com/NicholasGalvan/Python/blob/main/PythonProjects/Images/count%20of%20job%20postings.png)

![Data Visualization for Likelihood of Skills Requested in Data Jobs](https://github.com/NicholasGalvan/Python/blob/main/PythonProjects/Images/likelihood%20of%20skills%20requested.png)

### Insights 
- Python is highly versatile and this can be seen throughout the count and likelihood of requirement. This skill is in high demand across all data roles, but is most prominent in Data Scientist Roles. 
- SQL hovers from first to second in most demand depending on the job. Specifically in Data Engineer Roles, SQL is a must to master. 
- Some top skills can be job specific where they might not at all be used in other positions. Look at Data Analyst, Excel is the 2nd in demand skill which is less specialized in comparison to the technical skills of Data Engineers (AWS, Azure, Spark). 


## 2. How are in-demand skills trending for Data Analysts in the United States?

For this question, I filtered our original (job data) data frame to include only postings that are from the 'United States' and have the title position 'Data Analyst'. I then aggregated the count of each skill by each month into a pivot table. Lastly I converted the counts of each skill in each month, to a percent of total postings in each month to get a 'Likelihood' that a certain skill will appear in a Data Analyst job posting. 

View my notebook with detailed steps here: [3_Skills_Trend.ipynb](https://github.com/NicholasGalvan/Python/blob/main/PythonProjects/3_Skills_Trend.ipynb)

```python 
sns.lineplot(data=df_plot, dashes=False)
sns.set_theme(style='ticks')
sns.despine()

plt.title('Trending Top Skills for Data Analysts in the US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
plt.legend().remove()

ax= plt.gca() #getting the current axis to format the Y axis
from matplotlib.ticker import PercentFormatter # change yaxis to percent using matplotlib.ticker
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

#creating labels for each line within the range of the 5 values 
# plt.text(X position, y value, string label ). Notice each of our lines end at the 12th-1 index value of 11 or "Dec". We want our labels to start here. 
# to specify the y value we want it also to locate the last row of each index value (last row for sql, python...etc)
# lastly we want our label to be the string of the column names in the range
for i in range(5): 
    plt.text(11, df_plot.iloc[-1, i], df_plot.columns[i])
plt.tight_layout()
plt.show()
```
![Trending Top Skills for Data Analysts in the US](https://github.com/NicholasGalvan/Python/blob/main/PythonProjects/Images/Trending%20Top%20Skills%20for%20Data%20Analysts%20in%20the%20US.png)

### Insights: 
- SQL remains as the top skill throughout the year specifically in "Data Analyst" Positions throughout the United States. 
- Excel maintained the 2nd top Skill throughout the year and increased towards the end of 2023
- Interestingly, Python passed Tableau for the #3 spot of Trending skills. 
- It is good to note that the more stable a skill is in this case, the more likely it will appear in the future years, showing as an excellent skill to master for Aspiring Data Analysts. In the chart, the bottom 3 skills have less overall variability compared to the top 2. 


## 3. How well do jobs and skills pay for Data Analysts and Related Jobs?


### Salary Analysis For the top 6 Requested Roles in the United States 
In this analysis, I filtered for the top 6 Data Related roles by job posting count for the year. After getting these roles, I created an aggregated table of job titles by the median of the values in the (salary_year_avg) column. Plotting as a boxplot investigated the salary distributions for each. 

### Visualizing the Data 
```python 
# plotting the salary distrubtions for top 6 roles, Notice they are the same roles yet divided into general and senior 
sns.boxplot(data=df_us_Top6, x='salary_year_avg', y='job_title_short', order = job_order) # sort by median salary from the job order variable above 
sns.set_theme(style='ticks')

plt.title('Salary Distributions in the United States')
plt.ylabel('')
plt.xlabel('Yearly Salary $(USD)')
plt.xlim(0, 600000)
ticks_xaxis = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_xaxis)
plt.show()
```

### Results 

![Salary Distributions in the United States]()

#### Insights
- Between the top 6 data roles in the United States, there is a large variation in the distribution of salary, where Senior Data Scientists take the top spot for the highest average yearly salary. 
- There seems to be an immense ammount of "outliers" for Data Scientists and Data Engineers, indicating that certain jobs may require specialized skills where employers could have a much harder time in finding the right candidate. 
- In comparison to the rest, Senior and Junior Data Analysts might get paid the least but the range in their median yearly salary is quite small, indicating stability in these positions. 
- Lastly, It makes sense that each senior position leads to an increase in median salary when compared to their junior counterpart. 


### Highest Paid & Most Demanded Skills for Data Analysts in the US

To go further into detail, I compared the highest paying vs the highest in demand skills for Data Analyts. First, I grabbed the top 10 most paying skills for Data Analyst jobs by aggregating on median salary. Secondly, I created an aggregation of the top 10 'most common' skills for Data Analysts by count. The goal here is to more or less map out the essential and in-demand skills along with their salaries. Will it be better to specialize in niche technologies? Do less technical skills such as microsoft products still hold up in demand? 

#### Visualize Data 
```python 
# plot both the top 10 highest paying skills and the 10 most in demand skills 
fig, ax = plt.subplots(2,1)
sns.set_theme(style='ticks')
sns.barplot(data=df_da_us_top_pay, x='median', y=df_da_us_top_pay.index, ax=ax[0], palette='viridis')
ax[0].set_xlabel('Median Salary ')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K'))#changing the x-axis values to currency 
ax[0].set_ylabel('') # remove the y-axis label, the title is sufficient
ax[0].set_title('Top 10 Highest Paying Skills for Data Analysts')


sns.barplot(data=df_da_us_top_skills, x='median', y=df_da_us_top_skills.index, ax=ax[1],palette='viridis') # plotting with seaborn
 # flipping the order of the barh 
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K')) #changing the x-axis values to currency 
# ax[1].invert_yaxis() Dont have to invert with seaborn! 
ax[1].set_ylabel('') # remove y label 
ax[1].set_xlabel('Median Salary ')
ax[1].set_xlim(ax[0].get_xlim()) # matching xlim or xaxis values to the chart above it. 
ax[1].set_title('Top 10 Most In-Demand Skills for Data Analysts')

plt.tight_layout()
plt.show()
```
#### Results 
Here is the breakdown for the top 10 highest paying skills for Data Analysts in the US along with the top 10 most in-demand. 
![Highest Paid and Most in Demand Skills]()


#### Insights

- The top graph depicts the highest paying skills which are 'dpylr', 'bitbutcket' and 'gitlab', these all pay well above 175k. This suggest that learning niche and advanced technical skills can increase earning potential. 
- When looking at the bottom graph, we can see that the 'Microsoft 365' Stack such as (word, excel, powerpoint, power bi) are high in-demand yet they do not pay as much as more technical/programming skills like python, r, and sql. 
- There is a clear correlation between the most in-demand skills and median salary. An aspiring analyst should take note of this and learn a wide range of both technical and non technical skills to increase their chances of success. 