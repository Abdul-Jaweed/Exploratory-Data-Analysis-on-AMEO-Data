# Aspiring Mind Employment Outcome 2015 (AMEO)


The dataset was released by Aspiring Minds from the Aspiring Mind Employment Outcome 2015 (AMEO). The study is primarily limited  only to students with engineering disciplines. The dataset contains the employment outcomes of engineering graduates as dependent variables (Salary, Job Titles, and Job Locations) along with the standardized scores from three different areas – cognitive skills, technical skills and personality skills. The dataset also contains demographic features. The dataset  contains  around  40 independent variables and 4000 data points. The independent variables are both continuous and categorical in nature. The dataset contains a unique identifier for each candidate. Below mentioned table contains the details for the original dataset.



| VARIABLE                | TYPE          | DESCRIPTION                                                |
|-------------------------|---------------|-------------------------------------------------------------|
| ID                      | UID           | A unique ID to identify a candidate                        |
| Salary                  | Continuous    | Annual CTC offered to the candidate (in INR)                |
| DOJ                     | Date          | Date of joining the company                                 |
| DOL                     | Date          | Date of leaving the company                                 |
| Designation             | Categorical   | Designation offered in the job                              |
| JobCity                 | Categorical   | Location of the job (city)                                  |
| Gender                  | Categorical   | Candidate’s gender                                          |
| DOB                     | Date          | Date of birth of candidate                                  |
| 10percentage            | Continuous    | Overall marks obtained in grade 10 examinations             |
| 10board                 | Continuous    | The school board whose curriculum the candidate followed in grade 10 |
| 12graduation            | Date          | Year of graduation - senior year high school                |
| 12percentage            | Continuous    | Overall marks obtained in grade 12 examinations             |
| 12board                 | Date          | The school board whose curriculum the candidate followed in grade 12 |
| CollegeID               | NA/ID         | Unique ID identifying the college which the candidate attended |
| CollegeTier             | Categorical   | Tier of college                                             |
| Degree                  | Categorical   | Degree obtained/pursued by the candidate                    |
| Specialization          | Categorical   | Specialization pursued by the candidate                     |
| CollegeGPA              | Continuous    | Aggregate GPA at graduation                                 |
| CollegeCityID           | NA/ID         | A unique ID to identify the city in which the college is located in |
| CollegeCityTier         | Categorical   | The tier of the city in which the college is located        |
| CollegeState            | Categorical   | Name of States                                              |
| GraduationYear          | Date          | Year of graduation (Bachelor’s degree)                       |
| English                 | Continuous    | Scores in AMCAT English section                             |
| Logical                 | Continuous    | Scores in AMCAT Logical section                             |
| Quant                   | Continuous    | Scores in AMCAT Quantitative section                        |
| Domain                  | Continuous/Standardized | Scores in AMCAT’s domain module              |
| ComputerProgramming     | Continuous    | Score in AMCAT’s Computer programming section               |
| ElectronicsAndSemicon   | Continuous    | Score in AMCAT’s Electronics & Semiconductor Engineering section |
| ComputerScience         | Continuous    | Score in AMCAT’s Computer Science section                   |
| MechanicalEngg          | Continuous    | Score in AMCAT’s Mechanical Engineering section             |
| ElectricalEngg          | Continuous    | Score in AMCAT’s Electrical Engineering section             |
| TelecomEngg             | Continuous    | Score in AMCAT’s Telecommunication Engineering section      |
| CivilEngg               | Continuous    | Score in AMCAT’s Civil Engineering section                  |
| conscientiousness       | Continuous/Standardized | Scores in one of the sections of AMCAT’s personality test |
| agreeableness           | Continuous/Standardized | Scores in one of the sections of AMCAT’s personality test |
| extraversion            | Continuous/Standardized | Scores in one of the sections of AMCAT’s personality test |
| neuroticism             | Continuous/Standardized | Scores in one of the sections of AMCAT’s personality test |
| openness_to_experience  | Continuous/Standardized | Scores in one of the sections of AMCAT’s personality test |




## Research Questions

- Times of India article dated Jan 18, 2019 states that “After doing your Computer Science Engineering if you take up jobs as a Programming Analyst, Software Engineer, Hardware Engineer and Associate Engineer you can earn up to 2.5-3 lakhs as a fresh graduate.” Test this claim with the data given to you.

- Is there a relationship between gender and specialisation? (i.e. Does the preference of Specialisation depend on the Gender?)


### Research Question No : 1

After doing your Computer Science Engineering if you take up jobs as a Programming Analyst, Software Engineer, Hardware Engineer and Associate Engineer you can earn up to 2.5-3 lakhs as a fresh graduate. Test this claim with the data given to you.


```python
# Grouping the data by Designation and Specialization and calculating the average salary for each group

grouped_df = rq.groupby(['Designation', 'Specialization']).agg({'Salary': 'mean'}).reset_index()

# Checking if the average salaries are within the range of 2.5-3 lakhs

lower_bound = 250000
upper_bound = 300000
result = (rq['Salary'] >= lower_bound) & (rq['Salary'] <= upper_bound)

if result.all():
    print("The claim is supported by the data.")
else:
    print("The claim is not supported by the data.")
```

**The claim is not supported by the data.**


### Research Question No : 2

Is there a relationship between gender and specialisation? (i.e. Does the preference of Specialisation depend on the Gender?).


```python
# Calculating the frequency distribution of each specialization based on gender

freq_table = pd.crosstab(df['Gender'], df['Specialization'], margins=True)

# Normalizing the frequency table to get the proportions

freq_table.div(freq_table['All'], axis=0)

```


| Specialization | Aeronautical Engineering | Biomedical Engineering | Biotechnology | Chemical Engineering | Civil Engineering | Computers | ETRX | Instrumentation and Control Engineering | Instrumentation Engineering | Mech | Other | All |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Female | 0.001045 | 0.00209 | 0.009404 | 0.001045 | 0.006270 | 0.630094 | 0.327064 | 0.009404 | 0.000000 | 0.013584 | 0.000000 | 1.0 |
| Male | 0.000658 | 0.00000 | 0.001973 | 0.002960 | 0.007563 | 0.554094 | 0.351858 | 0.003617 | 0.001644 | 0.071358 | 0.004275 | 1.0 |
| All | 0.000750 | 0.00050 | 0.003752 | 0.002501 | 0.007254 | 0.572286 | 0.345923 | 0.005003 | 0.001251 | 0.057529 | 0.003252 | 1.0 |


**Research Question No : 2 Observation**


- The most popular specializations for both males and females are Computer Science and Electronics and Telecommunications (ETRX), which make up more than 60% and 55% of their respective proportions.

- The proportion of females in Aeronautical Engineering, Biomedical Engineering, and Biotechnology is higher than the proportion of males in these fields.

- The proportion of males in Chemical Engineering, Civil Engineering, and Mechanical Engineering is higher than the proportion of females in these fields.

- Other specializations have a higher proportion of males than females.