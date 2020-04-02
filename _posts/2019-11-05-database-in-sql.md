---
title: "SQL Database Design and Queries"
dateL: 2019-11-05
tags: [datbase, sql, query, relational database, erd, entity relational database, paranthetical]
header:
  image: 
excerpt: "Build a relational sql database."
mathjax: "true"
---
The Marcus Company is requiring a database that is scalable as the company exands. Although, the company has many concerns, the immediate objective is to develop a database for the company to store important informations that would allow them to generate payroll. Once the system is in place and running, other modules can be easily add on. 

Disclaimer: For the purpose of demonstration, the Marcus Company is a fictional company and all the data used are fictional. 

After gathering the data, sort them into subject-based tables and specify primary keys. Next, create relationships among tables and normalize the database architecture.

The parenthetical form of the entity relational database:

COMPANY(__ContractorNumber__, Name, Address1, Address2, City, State, ZIP, County, Phone, Fax)
PROJECT(__ProjectId__, ProjectLocation, Description, JOb, Stage)
EEO_CODE(__EEOCode__, Description, Minority)
JOBCODE(__JobCode__, JobClassification)
EMPLOYEE(__EmployeeID__, FirstName, LastName, MI, SocialSecurity, UnionStatus, Gender, *EEOCode*, Address 1, Address2, City, State, ZIP, Phone, BirthDate, MaritalStatus, *Manager*)
OVERTIME_RATE(__*ProjectId*__, OTRate)
PAY_SCALE(__*ProjectId*__, __*JobCode*__, Rate, FringeBenefits)
TIMECARD(__*ProjectID*__, __*EmployeeId*__, __*JobCode*__, WorkDate, PayPeriodEndDate, RegHours, OT_Hours)

The entity relational database schema:

<img src="{{ site.url }}{{ site.baseurl }}/images/sql/sql-ERD.png" alt="linearly separable data" height="48">

The next phase is to contruct the database with SQLdeveloper. First, create tables with Create statments. Next, input data into the tables with Insert statments.

Here is an sql example:
```sql
CREATE TABLE COMPANY
                (
             	ContractorNumber   char(20)       NOT NULL,
                Name             varchar(100)   NOT NULL,
              	Address1         varchar(50)    NOT NULL,
               	Address2         varchar(50)    NULL,
              	City             varchar(50)    NOT NULL,
              	State            char(2)        NOT NULL,
              	ZIP              char(5)        NOT NULL,
               	County           varchar(50)    NOT NULL,
                Phone		         char(12)       NOT NULL,
                Fax		           char(12)       NOT NULL,
              	CONSTRAINT PK_COMPANY PRIMARY KEY (ContractorNumber)
                );
 INSERT INTO COMPANY VALUES
                (
                '310646843', 'Marcus Company', '8088 Baron St.', NULL,   
                'Lillydale', 'CA', '80286', 'Baker County', '6145550386', '6145550486'
                );
 ```
Now you can qeury information from the database. Use JOIN statements to combine tables. Here is example:

```sql
select EMPLOYEE.EmployeeId, JOBCODE.JobCode, PAY_SCALE.Rate, PAY_SCALE.FringeBenefits, Rate + FringeBenefits as "Total", TIMECARD.RegHours, (Rate + FringeBenefits) * RegHours as "Gross"
From  PAY_SCALE
JOIN JOBCODE
ON PAY_SCALE.JobCode = JOBCODE.JobCode
JOIN TIMECARD
ON PAY_SCALE.ProjectId = TIMECARD.ProjectId AND PAY_SCALE.JobCode = TIMECARD.JobCode
JOIN EMPLOYEE
ON TIMECARD.EmployeeId = EMPLOYEE.EmployeeId
where TIMECARD.ProjectId = 'WA-PIN-335-005'
and TIMECARD.PayPeriodEndDate = '13-DEC-19'
and TIMECARD.RegHours is not null;
```
The query will generate the detailed pay breakdown:

<img src="{{ site.url }}{{ site.baseurl }}/images/sql/sql-gross.png" alt="linearly separable data" height="48">

You can view the enitre codes at this [link](https://https://github.com/youavang/Database-Design-SQL).
