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
