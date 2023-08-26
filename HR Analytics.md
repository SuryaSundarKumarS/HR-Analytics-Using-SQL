### 1) Employees Age Group Wise
````sql
select
agegroup,
count(empid) as employees,
concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as percentage
from
  hr_analytics
group by
  agegroup
order by
  count(empid) desc;
````
| Age Group | Employees | Percentage |
|-----------|-----------|------------|
| 26-35     | 590       | 41.46%     |
| 36-45     | 449       | 31.55%     |
| 46-55     | 223       | 15.67%     |
| 18-25     | 117       | 8.22%      |
| 55+       | 44        | 3.09%      |

**Employees in the Age Group of 26-35 are 41.46% followed by 36 - 45 are 31.55%, 46 - 55 are 15.67%, 18 - 25 are 8.22% and  55+ are 3.09%.**


### 2) Attrition Rate
````sql
select count(*) emploee_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_rate
from hr_analytics
where attrition = "yes";
````
| Employees_Left | Attrition_Rate |
|----------------|----------------|
| 230            | 16.16%         |

**Attrition Rate is 16.16%.**


## 3) Attrition Age Group Wise
````sql
select agegroup, count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by agegroup
order by count(attrition) desc;
````
| Agegroup | Employees_Left | Attrition_Percentage |
|----------|----------------|---------------------|
| 26-35    | 111            | 7.80%               |
| 18-25    | 43             | 3.02%               |
| 36-45    | 41             | 2.88%               |
| 46-55    | 27             | 1.90%               |
| 55+      | 8              | 0.56%               |

**Employees in the Age Group of 26-35(7.8%) are leaving the company more in number followed by 18 - 25(3.02%),36 - 45(2.88%), 46-55(1.90%) and 55+(0.56%).**


## 4) Employees by Age  Group
````sql
select businesstravel,agegroup, count(businesstravel) employees, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as percentage
from hr_analytics
group by agegroup,businesstravel
order by count(businesstravel) desc, businesstravel desc;
````
| BusinessTravel     | Agegroup | Employees | Percentage |
|--------------------|----------|-----------|------------|
| Travel_Rarely      | 26-35    | 399       | 28.04%     |
| Travel_Rarely      | 36-45    | 309       | 21.71%     |
| Travel_Rarely      | 46-55    | 167       | 11.74%     |
| Travel_Frequently  | 26-35    | 126       | 8.85%      |
| Travel_Rarely      | 18-25    | 88        | 6.18%      |
| Travel_Frequently  | 36-45    | 83        | 5.83%      |
| Non-Travel         | 26-35    | 59        | 4.15%      |
| Non-Travel         | 36-45    | 56        | 3.94%      |
| Travel_Frequently  | 46-55    | 39        | 2.74%      |
| Travel_Rarely      | 55+      | 35        | 2.46%      |
| Travel_Frequently  | 18-25    | 17        | 1.19%      |
| Non-Travel         | 46-55    | 17        | 1.19%      |
| Non-Travel         | 18-25    | 12        | 0.84%      |
| TravelRarely      | 26-35    | 6         | 0.42%      |
| Travel_Frequently  | 55+      | 5         | 0.35%      |
| Non-Travel         | 55+      | 4         | 0.28%      |
| TravelRarely      | 36-45    | 1         | 0.07%      |

**Employees in the Age Group of 26-35(28.04%), 36-45(21.71%) and 46-55(11.74%) are traveling rarely when compared to other.**


## 5) Attrition by businesstravel and agegroup
````sql
select businesstravel,agegroup, count(businesstravel) employees, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by agegroup,businesstravel
order by count(businesstravel) desc;
````
| BusinessTravel     | Agegroup | Employees_Left | Attrition_Percentage |
|--------------------|----------|----------------|---------------------|
| Travel_Rarely      | 26-35    | 68             | 4.78%               |
| Travel_Frequently  | 26-35    | 37             | 2.60%               |
| Travel_Rarely      | 36-45    | 30             | 2.11%               |
| Travel_Rarely      | 18-25    | 28             | 1.97%               |
| Travel_Rarely      | 46-55    | 18             | 1.26%               |
| Travel_Frequently  | 18-25    | 13             | 0.91%               |
| Travel_Frequently  | 36-45    | 8              | 0.56%               |
| Travel_Frequently  | 46-55    | 8              | 0.56%               |
| Travel_Rarely      | 55+      | 7              | 0.49%               |
| Non-Travel         | 26-35    | 6              | 0.42%               |
| Non-Travel         | 36-45    | 3              | 0.21%               |
| Non-Travel         | 18-25    | 2              | 0.14%               |
| Non-Travel         | 46-55    | 1              | 0.07%               |
| Travel_Frequently  | 55+      | 1              | 0.07%               |

**Employees belongs to age group 26-35(4.78%) - Travel Rarely,26-35(2.60%) - Travel frequently, 36 - 45(2.11%) - Travel Rarely.**


## 6) Avg Daily Rate by Agegroup
````sql
select agegroup, avg(dailyrate) average_daily_rate
from hr_analytics
group by agegroup
order by avg(dailyrate) desc;
````
| Agegroup | Average_Daily_Rate |
|----------|-------------------|
| 46-55    | 824.2422           |
| 36-45    | 805.6192           |
| 26-35    | 797.5797           |
| 55+      | 791.3182           |
| 18-25    | 772.0256           |

**Employees in the age group 46 - 55 are earning an average daily rate of $824.2 and 18 - 25 are earning a average daily rate of $772.**


## 7) Attrition by businesstravel and agegroup
````sql
select agegroup, gender, department, avg(dailyrate), count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by agegroup,gender
order by count(attrition) desc;
````
| Agegroup | Gender | Department             | Average_Daily_Rate | Employees_Left | Attrition_Percentage |
|----------|--------|------------------------|--------------------|----------------|---------------------|
| 26-35    | Male   | Research & Development | 784.7941           | 68             | 4.78%               |
| 26-35    | Female | Human Resources        | 607.6279           | 43             | 3.02%               |
| 36-45    | Male   | Sales                  | 807.4286           | 28             | 1.97%               |
| 18-25    | Male   | Research & Development | 669.4000           | 25             | 1.76%               |
| 46-55    | Male   | Sales                  | 790.8000           | 20             | 1.41%               |
| 18-25    | Female | Sales                  | 840.7778           | 18             | 1.26%               |

**Employees in the Research & Development(68 - 4.78%) and Human Resourcces Departments(3.02%) are leaving the company are in more number.**


## 8) Distance from home by Attrirtion
````sql
select 
    case
        when distancefromhome <= 10 then "1-10"
        when distancefromhome <= 20 then "11-20"
        when distancefromhome <= 30 then "21-30"
        else "check_logic"
    end as distance_range,
    gender,
    count(attrition) as employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by distance_range,gender
order by employees_left desc;
````
| Distance_Range | Gender | Employees_Left | Attrition_Percentage |
|----------------|--------|----------------|---------------------|
| 1-10           | Male   | 90             | 6.32%               |
| 1-10           | Female | 48             | 3.37%               |
| 21-30          | Male   | 31             | 2.18%               |
| 11-20          | Male   | 25             | 1.76%               |
| 11-20          | Female | 22             | 1.55%               |
| 21-30          | Female | 14             | 0.98%               |

**Employess who are in the distance of 1 - 10 kms are leaving in more Male - 6.32%, Female - 3.37%.**


## 9) Education by Attrirtion
````sql
select education,educationfield, count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by educationfield
order by count(attrition) desc;
````
| Education | Education_Field   | Employees_Left | Attrition_Percentage |
|-----------|-------------------|----------------|---------------------|
| 3         | Life Sciences     | 88             | 6.18%               |
| 1         | Medical           | 57             | 4.01%               |
| 3         | Marketing         | 35             | 2.46%               |
| 1         | Technical Degree  | 32             | 2.25%               |
| 3         | Other             | 11             | 0.77%               |
| 1         | Human Resources   | 7              | 0.49%               |

**Employes with Life Sciences(6.18%) and Medical(4.01%) as there education field are leaving in more number.**


## 10) Gender by Attrirtion
````sql
select gender, count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by gender
order by count(attrition) desc;
````
| Gender | Employees_Left | Attrition_Percentage |
|--------|----------------|---------------------|
| Male   | 146            | 10.26%              |
| Female | 84             | 5.90%               |

**Male(10.26%) Employees are leaving in more number than compared to female(5.90%) employees.**


## 11) Marital Status by Attrirtion
````sql
select maritalstatus, count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by maritalstatus
order by count(attrition) desc;
````
| Marital_Status | Employees_Left | Attrition_Percentage |
|----------------|----------------|---------------------|
| Single         | 117            | 8.22%               |
| Married        | 80             | 5.62%               |
| Divorced       | 33             | 2.32%               |

**Employees whose marital staus Single(8.22%) and Married(5.62%) are leaving in more number.**


## 12) Hourly Rate and Job level by Attrirtion
````sql
select joblevel, avg(hourlyrate), count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by joblevel
order by count(attrition) desc;
````
| JobLevel | Average_Hour_Rate | Employees_Left | Attrition_Percentage |
|----------|-------------------|----------------|---------------------|
| 1        | 64.8696           | 138            | 9.70%               |
| 2        | 66.6538           | 52             | 3.65%               |
| 3        | 65.4667           | 30             | 2.11%               |
| 4        | 79.0000           | 5              | 0.35%               |
| 5        | 61.8000           | 5              | 0.35%               |


## 13) job level by employees
````sql
select joblevel,count(*) employees, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage  
from hr_analytics
group by joblevel;
````
| Joblevel | Employees | Attrition_Percentage |
|----------|-----------|---------------------|
| 1        | 520       | 36.54%              |
| 2        | 522       | 36.68%              |
| 3        | 208       | 14.62%              |
| 4        | 107       | 7.52%               |
| 5        | 66        | 4.64%               |

**Employees in the Job level 1(36.54%) and 2(36.68%) are leaving in more number.**  


## 14) salaryslab by Attrirtion
````sql
select salaryslab, count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by salaryslab
order by count(attrition) desc;
````
| Salary   | Employees_Left | Attrition_Percentage |
|----------|----------------|---------------------|
| Upto 5k  | 158            | 11.10%              |
| 5k-10k   | 48             | 3.37%               |
| 10k-15k  | 19             | 1.34%               |
| 15k+     | 5              | 0.35%               |

**Employees in the slary slab upto 5k(11.10%) and 5k - 10k(3.37%) are leaving in more number.**


## 15) NumCompaniesWorked by Attrirtion
````sql
select numcompaniesworked, count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by NumCompaniesWorked
order by count(attrition) desc;
````
| NumCompaniesWorked | Employees_Left | Attrition_Percentage |
|---------------------|----------------|---------------------|
| 1                   | 95             | 6.68%               |
| 0                   | 22             | 1.55%               |
| 4                   | 18             | 1.26%               |
| 3                   | 16             | 1.12%               |
| 7                   | 16             | 1.12%               |
| 5                   | 15             | 1.05%               |
| 2                   | 15             | 1.05%               |
| 6                   | 15             | 1.05%               |
| 9                   | 12             | 0.84%               |
| 8                   | 6              | 0.42%               |

**Employees who are having 0 - 1 year(6.68%) experience are leaving in more number.**


## 16) Jobsatisfaction by Attrirtion
````sql
select 
    case
        when jobsatisfaction = 5 then "best"
        when jobsatisfaction = 4 then"better"
        when jobsatisfaction = 3 then "good"
        when jobsatisfaction = 2 then "bad"
        when jobsatisfaction = 1 then "worst"
        else "check_logic"
    end as job_satisfaction,
    gender,
    count(attrition) as employees_left,concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by jobsatisfaction,gender
order by employees_left desc;
````
| Job_Satisfaction | Gender | Employees | Attrition_Percentage |
|------------------|--------|-----------|---------------------|
| Good             | Male   | 45        | 3.16%               |
| Worst            | Male   | 44        | 3.09%               |
| Better           | Male   | 35        | 2.46%               |
| Good             | Female | 26        | 1.83%               |
| Bad              | Female | 24        | 1.69%               |
| Bad              | Male   | 22        | 1.55%               |
| Worst            | Female | 19        | 1.34%               |
| Better           | Female | 15        | 1.05%               |

**Males(5.62%) felt the job satisfaction as best.**


## 17) Worklifebalance by Attrirtion.
````sql
select 
    case
        when worklifebalance = 5 then "best"
        when worklifebalance = 4 then"better"
        when worklifebalance = 3 then "good"
        when worklifebalance = 2 then "bad"
        when worklifebalance = 1 then "worst"
        else "check_logic"
    end as worklifebalance,
    gender,
    count(attrition) as employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by worklifebalance,gender
order by employees_left desc;
````
| WorkLifeBalance | Gender | Employees_Left | Attrition_Percentage |
|-----------------|--------|----------------|---------------------|
| Good            | Male   | 78             | 5.48%               |
| Good            | Female | 46             | 3.23%               |
| Bad             | Male   | 37             | 2.60%               |
| Bad             | Female | 18             | 1.26%               |
| Worst           | Male   | 18             | 1.26%               |
| Better          | Female | 13             | 0.91%               |
| Better          | Male   | 13             | 0.91%               |
| Worst           | Female | 7              | 0.49%               |

**Even employees(8.91%) felt Work Life Balnce was good but they are leaving.**


## 18) Avg Percent Salary Hike and job level by Attrirtion
````sql
select joblevel, avg(percentsalaryhike), count(attrition) Employees_left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
from hr_analytics
where attrition = "yes"
group by joblevel
order by count(attrition) desc;
````
| Joblevel | Average_Percentage_Salary_Hike | Employees_left | Attrition_Percentage |
|----------|-------------------------------|----------------|---------------------|
| 1        | 15.2536                       | 138            | 9.70%               |
| 2        | 15.3462                       | 52             | 3.65%               |
| 3        | 14.1333                       | 30             | 2.11%               |
| 4        | 13.4000                       | 5              | 0.35%               |
| 5        | 13.6000                       | 5              | 0.35%               |

**13.35% Employees belongs to low job level are gettibg same hike nearly 15%**


## 19) Relationshipsatisfaction by Attrirtion
````sql
select 
    case
        when relationshipsatisfaction = 5 then "best"
        when relationshipsatisfaction = 4 then"better"
        when relationshipsatisfaction = 3 then "good"
        when relationshipsatisfaction = 2 then "bad"
        when relationshipsatisfaction = 1 then "worst"
        else "check_logic"
    end as relationship_satisfaction,
    gender,
    count(attrition) as employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by relationshipsatisfaction,gender
order by employees_left desc;
````
| Relationship_Satisfaction | Gender | Employees_Left | Attrition_Percentage |
|---------------------------|--------|----------------|---------------------|
| Good                      | Male   | 45             | 3.16%               |
| Better                    | Male   | 42             | 2.95%               |
| Bad                       | Male   | 31             | 2.18%               |
| Worst                     | Male   | 28             | 1.97%               |
| Worst                     | Female | 27             | 1.90%               |
| Good                      | Female | 23             | 1.62%               |
| Better                    | Female | 21             | 1.48%               |
| Bad                       | Female | 13             | 0.91%               |

**Both Male and Female of 6.82% felt the Relationship satisfaction as worst, So need to work on there bonding by arranging team lunches and extra-curicular activities to know them better.**


## 20) Jobinvolvement by Attrirtion
````sql
select 
    case
        when jobinvolvement = 5 then "best"
        when jobinvolvement = 4 then "better"
        when jobinvolvement = 3 then "good"
        when jobinvolvement = 2 then "bad"
        when jobinvolvement = 1 then "worst"
        else "check_logic"
    end as jobinvolvement,
    gender,
    count(attrition) as employees_left,
    concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by jobinvolvement, gender
order by employees_left desc;
````
| JobInvolvement  | Gender | Employees_Left | Attrition_Percentage |
|------------------|--------|----------------|---------------------|
| Good             | Male   | 76             | 5.34%               |
| Bad              | Male   | 48             | 3.37%               |
| Good             | Female | 44             | 3.09%               |
| Bad              | Female | 23             | 1.62%               |
| Worst            | Male   | 15             | 1.05%               |
| Worst            | Female | 11             | 0.77%               |
| Better           | Male   | 7              | 0.49%               |
| Better           | Female | 6              | 0.42%               |

**4.99% Employees are not involving in the job. So, before recruiting the employees check with thee roles and responsibilities twice or thrice**
