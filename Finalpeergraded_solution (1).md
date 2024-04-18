<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/labs/Lab%20-%20Create%20Tables%20and%20Load%20Data%20in%20MySQL%20using%20phpMyAdmin/images/IDSNlogo.png" width="200" height="200">

# Hands-on Lab:Peer graded assignment using SQL in MySQL using phpMyAdmin

**Estimated time needed:** 20 minutes

In this lab, you will learn how to create tables and load data in the MySQL database service using the phpMyAdmin graphical user interface (GUI) tool.

# 

## Software Used in this Lab

In this lab, you will use <a href="https://www.mysql.com/?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDB0110ENSkillsNetwork24601058-2021-01-01">MySQL</a>. MySQL is a Relational Database Management System (RDBMS) designed to efficiently store, manipulate, and retrieve data.

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/labs/Lab%20-%20Create%20Tables%20and%20Load%20Data%20in%20MySQL%20using%20phpMyAdmin/images/mysql.png" width="100" height="100">
<p></p>

To complete this lab you will utilize MySQL relational database service available as part of IBM Skills Network Labs (SN Labs) Cloud IDE. SN Labs is a virtual lab environment used in this course.

# 

## Database Used in this Lab

**Mysql_learners** database has been used in this lab.

Here you will be creating  and inserting data into the below mentioned 3 tables

1.chicago_public_schools
2.chicago_socioeconomic_data
3.chicago_crime

Here you will be using 3 dump files for this purpose.

<a href="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/MySQL/week5/chicago_public_schools.sql">chicago_public_schools</a>

<a href ="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/MySQL/week5/chicago_crime.sql">chicago_crime</a>

<a href="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/MySQL/week5/chicago_socioeconomic_data.sql">chicago_socioeconomic_data</a>

### Task A: Create a database

1.  Go to **Terminal > New Terminal** to open a terminal from the side by side launched Cloud IDE.

    ![image](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/labs/Lab%20-%20Create%20Tables%20and%20Load%20Data%20in%20MySQL%20using%20phpMyAdmin/images/2.1.png)

<br>

2.  Start MySQL service session in the Cloud IDE using the command below in the terminal. Find your MySQL service session password from the highlighted location of the terminal shown in the image below. Note down your MySQL service session password because you may need to use it later in the lab.

    ```
    start_mysql
    ```

    {: codeblock}

    ![image](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/labs/Lab%20-%20Create%20Tables%20and%20Load%20Data%20in%20MySQL%20using%20phpMyAdmin/images/2.2.png)

<br>

3.  Copy your phpMyAdmin weblink from the highlighted location of the terminal shown in the image below. Past it into the address bar in a new tab of your web browser. This will open the phpMyAdmin tool.

    ![image](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/labs/Lab%20-%20Create%20Tables%20and%20Load%20Data%20in%20MySQL%20using%20phpMyAdmin/images/2.3.png)

<br>

4.  You will see the phpMyAdmin GUI tool.

    ![image](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/labs/Lab%20-%20Create%20Tables%20and%20Load%20Data%20in%20MySQL%20using%20phpMyAdmin/images/2.4.png)

<br>

5.  In the tree-view, click **New** to create a new empty database. Then enter **Mysql_Learners** as the name of the database and click **Create**.

    The encoding will be left as **utf8mb4\_0900\_ai_ci**. UTF-8 is the most commonly used character encoding for content or data.

    Proceed to Task B.

    ![image](images/db1.png)


Load the dump files one by one into the database **Mysql_learners**  by clicking the **Import** tab and choose the file.
Click on **Go** button.

   ![image](images/dump1.png)

   ![image](images/dump2.png)


The  tables are created  and the data is loaded successfully. Repeat the same operation with the other 2 dump files to create and load the tables.

You will see a screen as below

![image](images/dump3.png)



![image](images/4G.png)


## Problems

Now write and execute SQL queries to solve assignment problems

### Problem 1

##### Find the total number of crimes recorded in the CRIME table.


```
select COUNT(*) from chicago_crime;

```

![image](images/F1.png)


### Problem 2

##### List community areas with per capita income less than 11000.


```
select community_area_name,PER_CAPITA_INCOME from chicago_socioeconomic_data where PER_CAPITA_INCOME < 11000

```
![image](images/f2.png)


### Problem 3

##### List all case numbers for crimes  involving minors?(children are not considered minors for the purposes of crime analysis)

```
select case_number from chicago_crime where description like '%MINOR%'

```
![image](images/F3.png)


### Problem 4

##### List all kidnapping crimes involving a child?


```

select * from chicago_crime  where description like '%child%'  and  PRIMARY_TYPE='KIDNAPPING'


```

![image](images/F4.png)

### Problem 5

##### What kinds of crimes were recorded at schools?


```
select DISTINCT(primary_type) from chicago_crime  where location_description like '%SCHOOL%'


```
![image](images/F5.png)

### Problem 6

##### List the average safety score for all types of schools.


```

select `Elementary, Middle, or High School`, AVG(SAFETY_SCORE) from chicago_public_schools GROUP BY `Elementary, Middle, or High School`;

```

![image](images/F6.png)


### Problem 7

##### List 5 community areas with highest % of households below poverty line

```
SELECT COMMUNITY_AREA_NAME, PERCENT_HOUSEHOLDS_BELOW_POVERTY 
FROM chicago_socioeconomic_data ORDER BY PERCENT_HOUSEHOLDS_BELOW_POVERTY DESC LIMIT 5;

```


![image](images/F7.png)


### Problem 8

##### Which community area is most crime prone?


```

SELECT COMMUNITY_AREA_NUMBER, COUNT(COMMUNITY_AREA_NUMBER) FROM chicago_crime GROUP BY COMMUNITY_AREA_NUMBER
ORDER BY COUNT(COMMUNITY_AREA_NUMBER) DESC LIMIT 1;

```


![image](images/F8.png)


### Problem 9

##### Use a sub-query to find the name of the community area with highest hardship index

```

SELECT DISTINCT(COMMUNITY_AREA_NAME) FROM chicago_socioeconomic_data WHERE HARDSHIP_INDEX = (SELECT MAX(HARDSHIP_INDEX) FROM chicago_socioeconomic_data);
```
![image](images/F9.png)

### Problem 10

##### Use a sub-query to determine the Community Area Name with most number of crimes?


```

select DISTINCT(COMMUNITY_AREA_NAME) FROM chicago_socioeconomic_data WHERE COMMUNITY_AREA_NUMBER=(SELECT COMMUNITY_AREA_NUMBER from chicago_crime GROUP BY COMMUNITY_AREA_NUMBER ORDER BY COUNT(*) DESC LIMIT 1)

```
![image](images/F10.png)



# Author(s)

[Lakshmi Holla](https://www.linkedin.com/in/lakshmi-holla-b39062149/) 


[Malika Singla](https://www.linkedin.com/in/malika-goyal-04798622/)




## Changelog

| Date       | Version | Changed by | Change Description                   |
| ---------- | ------- | ---------- | ------------------------------------ |
| 2021-11-01 | 0.1  | Lakshmi Holla, Malika Singla | Initial Version       |


## <h3 align="center"> © IBM Corporation 2021. All rights reserved. <h3/>
