## Employees Age Group Wise
SELECT
Agegroup,
COUNT(EmpID) AS Employees,
concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Percentage
FROM
  hr_analytics
GROUP BY
  Agegroup
ORDER BY
  COUNT(EmpID) DESC;
# Employees in the Age Group of 26-35 are 41.46% followed by 36 - 45 are 31.55%, 46 - 55 are 15.67%, 18 - 25 are 8.22% and  55+ are 3.09%.

## Attrition Rate
select count(*) Emploee_Left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Rate
from hr_analytics
where attrition = "yes";
# Attrition Rate is 16.16%.

## Attrition Age Group Wise
select Agegroup, count(attrition) Employees_Left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
from hr_analytics
where attrition = "yes"
group by Agegroup
order by count(attrition) desc;
# Employees in the Age Group of 26-35(7.8%) are leaving the company more in number followed by 18 - 25(3.02%),36 - 45(2.88%), 46-55(1.90%) and 55+(0.56%).

## Employees by Age  Group
select businesstravel,agegroup, count(businesstravel) employees, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Percentage
from hr_analytics
group by agegroup,businesstravel
order by count(businesstravel) desc, businesstravel desc;
# Employees in the Age Group of 26-35(28.04%), 36-45(21.71%) and 46-55(11.74%) are traveling rarely when compared to other.


## Attrition by businesstravel and agegroup
select businesstravel,agegroup, count(businesstravel) employees, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
from hr_analytics
where attrition = "yes"
group by agegroup,businesstravel
order by count(businesstravel) desc;
#Employees belongs to age group 26-35(4.78%) - Travel Rarely,26-35(2.60%) - Travel frequently, 36 - 45(2.11%) - Travel Rarely.

## Avg Daily Rate by Agegroup
select agegroup, avg(dailyrate) average_daily_rate
from hr_analytics
group by agegroup
order by avg(dailyrate) desc;
# Employees in the age group 46 - 55 are earning an average daily rate of $824.2 and 18 - 25 are earning a average daily rate of $772.

## Attrition by businesstravel and agegroup
select agegroup, gender, department, avg(dailyrate), count(attrition) Employees_Left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
from hr_analytics
where attrition = "yes"
group by agegroup,gender
order by count(attrition) desc;
# Employees in the Research & Development(68 - 4.78%) and Human Resourcces Departments(3.02%) are leaving the company are in more number.

## Distance from home by Attrirtion
SELECT 
    CASE
        WHEN distancefromhome <= 10 THEN "1-10"
        WHEN distancefromhome <= 20 THEN "11-20"
        WHEN distancefromhome <= 30 THEN "21-30"
        ELSE "check_logic"
    END AS distance_range,
    gender,
    COUNT(attrition) AS Employees_left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
FROM hr_analytics
where attrition = "yes"
GROUP BY distance_range,gender
ORDER BY Employees_left DESC;
# Employess who are in the distance of 1 - 10 kms are leaving in more Male - 6.32%, Female - 3.37%.

## Education by Attrirtion
select education,educationfield, count(attrition) Employees_left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
from hr_analytics
where attrition = "yes"
group by educationfield
order by count(attrition) desc;
# Employes with Life Sciences(6.18%) and Medical(4.01%) as there education field are leaving in more number.


## Gender by Attrirtion
select gender, count(attrition) Employees_left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
from hr_analytics
where attrition = "yes"
group by gender
order by count(attrition) desc;
# Male(10.26%) Employees are leaving in more number than compared to female(5.90%) employees.


## Marital Status by Attrirtion
select maritalstatus, count(attrition) Employees_left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
from hr_analytics
where attrition = "yes"
group by maritalstatus
order by count(attrition) desc;
# Employees whose marital staus Single(8.22%) and Married(5.62%) are leaving in more number. 

## Hourly Rate and Job level by Attrirtion
select joblevel, avg(hourlyrate), count(attrition) Employees_left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
from hr_analytics
where attrition = "yes"
group by joblevel
order by count(attrition) desc;

## job level by employees
select joblevel,count(*) employees, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage  
from hr_analytics
group by joblevel;
# Employees in the Job level 1(36.54%) and 2(36.68%) are leaving in more number.  

## salaryslab by Attrirtion
select salaryslab, count(attrition) Employees_left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
from hr_analytics
where attrition = "yes"
group by salaryslab
order by count(attrition) desc;
# Employees in the slary slab upto 5k(11.10%) and 5k - 10k(3.37%) are leaving in more number. 

## NumCompaniesWorked by Attrirtion
select NumCompaniesWorked, count(attrition) Employees_left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
from hr_analytics
where attrition = "yes"
group by NumCompaniesWorked
order by count(attrition) desc;
# Employees who are having 0 - 1 year(6.68%) experience are leaving in more number.

## Jobsatisfaction by Attrirtion
SELECT 
    CASE
        WHEN Jobsatisfaction = 5 THEN "Best"
        WHEN Jobsatisfaction = 4 THEN"Better"
        WHEN Jobsatisfaction = 3 THEN "Good"
        WHEN Jobsatisfaction = 2 THEN "bad"
        WHEN Jobsatisfaction = 1 THEN "Worst"
        ELSE "check_logic"
    END AS Job_Satisfaction,
    gender,
    COUNT(attrition) AS Employees_left,concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
FROM hr_analytics
where attrition = "yes"
GROUP BY Jobsatisfaction,gender
ORDER BY Employees_left DESC;
# Males(5.62%) felt the job satisfaction as best.

## Worklifebalance by Attrirtion.
SELECT 
    CASE
        WHEN Worklifebalance = 5 THEN "Best"
        WHEN Worklifebalance = 4 THEN"Better"
        WHEN Worklifebalance = 3 THEN "Good"
        WHEN Worklifebalance = 2 THEN "bad"
        WHEN Worklifebalance = 1 THEN "Worst"
        ELSE "check_logic"
    END AS Worklifebalance,
    gender,
    COUNT(attrition) AS Employees_left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
FROM hr_analytics
where attrition = "yes"
GROUP BY Worklifebalance,gender
ORDER BY Employees_left DESC;
# Even employees(8.91%) felt Work Life Balnce was good but they are leaving.

## Avg Percent Salary Hike and job level by Attrirtion
select joblevel, avg(percentsalaryhike), count(attrition) Employees_left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
from hr_analytics
where attrition = "yes"
group by joblevel
order by count(attrition) desc;
# 13.35% Employees belongs to low job level are gettibg same hike nearly 15%

## Relationshipsatisfaction by Attrirtion
SELECT 
    CASE
        WHEN Relationshipsatisfaction = 5 THEN "Best"
        WHEN Relationshipsatisfaction = 4 THEN"Better"
        WHEN Relationshipsatisfaction = 3 THEN "Good"
        WHEN Relationshipsatisfaction = 2 THEN "bad"
        WHEN Relationshipsatisfaction = 1 THEN "Worst"
        ELSE "check_logic"
    END AS Relationship_Satisfaction,
    gender,
    COUNT(attrition) AS Employees_left, concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
FROM hr_analytics
where attrition = "yes"
GROUP BY Relationshipsatisfaction,gender
ORDER BY Employees_left DESC;
# Both Male and Female of 6.82% felt the Relationship satisfaction as worst, So need to work on there bonding by arranging team lunches and extra-curicular activities to know them better.


## Jobinvolvement by Attrirtion
SELECT 
    CASE
        WHEN Jobinvolvement = 5 THEN "Best"
        WHEN Jobinvolvement = 4 THEN "Better"
        WHEN Jobinvolvement = 3 THEN "Good"
        WHEN Jobinvolvement = 2 THEN "Bad"
        WHEN Jobinvolvement = 1 THEN "Worst"
        ELSE "Check_logic"
    END AS Jobinvolvement,
    gender,
    COUNT(attrition) AS Employees_left,
    concat(round((COUNT(EmpID) / (SELECT COUNT(*) FROM hr_analytics) * 100),2),"%") AS Attrition_Percentage
FROM hr_analytics
WHERE attrition = "yes"
GROUP BY Jobinvolvement, gender
ORDER BY Employees_left DESC;
# 4.99% Employees are not involving in the job. So, before recruiting the employees check with thee roles and responsibilities twice or thrice*/
