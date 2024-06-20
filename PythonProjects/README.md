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
[Data visualization for Top Skills in Data Jobs]()
