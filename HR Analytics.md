### Employees Age Group Wise
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

**Employees in the Age Group of 26-35 are 41.46% followed by 36 - 45 are 31.55%, 46 - 55 are 15.67%, 18 - 25 are 8.22% and  55+ are 3.09%.**

### Attrition Rate
````sql
select count(*) emploee_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_rate
from hr_analytics
where attrition = "yes";
````
**Attrition Rate is 16.16%.**

## Attrition Age Group Wise
````sql
select agegroup, count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by agegroup
order by count(attrition) desc;
````
**Employees in the Age Group of 26-35(7.8%) are leaving the company more in number followed by 18 - 25(3.02%),36 - 45(2.88%), 46-55(1.90%) and 55+(0.56%).**

## Employees by Age  Group
````sql
select businesstravel,agegroup, count(businesstravel) employees, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as percentage
from hr_analytics
group by agegroup,businesstravel
order by count(businesstravel) desc, businesstravel desc;
````
**Employees in the Age Group of 26-35(28.04%), 36-45(21.71%) and 46-55(11.74%) are traveling rarely when compared to other.**


## Attrition by businesstravel and agegroup
````sql
select businesstravel,agegroup, count(businesstravel) employees, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by agegroup,businesstravel
order by count(businesstravel) desc;
````
**Employees belongs to age group 26-35(4.78%) - Travel Rarely,26-35(2.60%) - Travel frequently, 36 - 45(2.11%) - Travel Rarely.**

## Avg Daily Rate by Agegroup
````sql
select agegroup, avg(dailyrate) average_daily_rate
from hr_analytics
group by agegroup
order by avg(dailyrate) desc;
````
**Employees in the age group 46 - 55 are earning an average daily rate of $824.2 and 18 - 25 are earning a average daily rate of $772.**

## Attrition by businesstravel and agegroup
````sql
select agegroup, gender, department, avg(dailyrate), count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by agegroup,gender
order by count(attrition) desc;
````
**Employees in the Research & Development(68 - 4.78%) and Human Resourcces Departments(3.02%) are leaving the company are in more number.**

## Distance from home by Attrirtion
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
**Employess who are in the distance of 1 - 10 kms are leaving in more Male - 6.32%, Female - 3.37%.**

## Education by Attrirtion
````sql
select education,educationfield, count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by educationfield
order by count(attrition) desc;
````
**Employes with Life Sciences(6.18%) and Medical(4.01%) as there education field are leaving in more number.**


## Gender by Attrirtion
````sql
select gender, count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by gender
order by count(attrition) desc;
````
**Male(10.26%) Employees are leaving in more number than compared to female(5.90%) employees.**


## Marital Status by Attrirtion
````sql
select maritalstatus, count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by maritalstatus
order by count(attrition) desc;
````
**Employees whose marital staus Single(8.22%) and Married(5.62%) are leaving in more number.**

## Hourly Rate and Job level by Attrirtion
````sql
select joblevel, avg(hourlyrate), count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by joblevel
order by count(attrition) desc;
````

## job level by employees
````sql
select joblevel,count(*) employees, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage  
from hr_analytics
group by joblevel;
````
**Employees in the Job level 1(36.54%) and 2(36.68%) are leaving in more number.**  

## salaryslab by Attrirtion
````sql
select salaryslab, count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by salaryslab
order by count(attrition) desc;
````
**Employees in the slary slab upto 5k(11.10%) and 5k - 10k(3.37%) are leaving in more number.**

## NumCompaniesWorked by Attrirtion
````sql
select numcompaniesworked, count(attrition) employees_left, concat(round((count(empid) / (select count(*) from hr_analytics) * 100),2),"%") as attrition_percentage
from hr_analytics
where attrition = "yes"
group by NumCompaniesWorked
order by count(attrition) desc;
````
**Employees who are having 0 - 1 year(6.68%) experience are leaving in more number.**

## Jobsatisfaction by Attrirtion
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
**Males(5.62%) felt the job satisfaction as best.**

## Worklifebalance by Attrirtion.
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
**Even employees(8.91%) felt Work Life Balnce was good but they are leaving.**

## Avg Percent Salary Hike and job level by Attrirtion
````sql
select joblevel, avg(percentsalaryhike), count(attrition) Employees_left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
from hr_analytics
where attrition = "yes"
group by joblevel
order by count(attrition) desc;
````
**13.35% Employees belongs to low job level are gettibg same hike nearly 15%**

## Relationshipsatisfaction by Attrirtion
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
**Both Male and Female of 6.82% felt the Relationship satisfaction as worst, So need to work on there bonding by arranging team lunches and extra-curicular activities to know them better.**


## Jobinvolvement by Attrirtion
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
**4.99% Employees are not involving in the job. So, before recruiting the employees check with thee roles and responsibilities twice or thrice**
