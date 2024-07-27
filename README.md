# Hands-on-Project-Working-with-a-real-world-data-set-using-SQL-in-PgAdmin

This is a Hands-on Project working with a real world data-set using SQL in PgAdmin

# Software Used in this Lab

PgAdmin 4 (PostgreSQL 15)

# Database Used in this Lab

The Three (3) datasets used in this project were gotten from the city of Chicago’s Data Portal:

Dataset 1 - Socioeconomic Indicators in Chicago

Dataset 2 - Chicago Public Schools

Dataset 3 - Chicago Crime Data

# Objectives

The objectives of this project were to:

1. Create the Chicago database and the 3 datasets as tables in PgAdmin.
2. Tackle real problem using SQL queries. 

# Task A: Creating the Chicago database and the 3 datasets as tables in PgAdmin.

a. The new database named "ChicagoDB" was created in PgAdmin and the 3 tables were created by executing the following scripts rather than creating each table manually by typing the DDL commands in the SQL editor.

1.Chicago_public_schools_create_query_script: https://drive.google.com/file/d/114CoSCeFcSDzOLuS9FWUeIdY3iLKoN8A/view?usp=sharing

2.Chicago_crime_create_query_script: https://drive.google.com/file/d/1C3O8Aa47rka9L2LK0mQF5eQLvz3fXY7Z/view?usp=sharing

3.Chicago_socioeconomic_create_query_script: https://drive.google.com/file/d/1AoLeFsOOvERw1PNYBHmXUJQ18DxCqtx9/view?usp=sharing

b. After the 3 tables had been successfully created within the Chicago database, The 3 datasets were downloaded and imported into the already created tables as CSV files.

1. Chicago_public_schools_data - file can be downloaded here: https://drive.google.com/file/d/1vUT6RHg869rMTiy0ML-vWuyPW7fRu2m9/view?usp=sharing

2. Chicago_crime_data - file can be downloaded here: https://drive.google.com/file/d/1o30Anam0IZXfAFVZQwdxMDIKeW87YES_/view?usp=sharing

3. Chicago_socioeconomic_data - file can be downloaded here: https://drive.google.com/file/d/1FLKT0IhsQzxL89PIsRGv10bHCCl0qbVj/view?usp=sharing

To load each table, the following steps were taken:

1. Right-click on each table and select Import tab.

2. ChoOse the csv file and click OK 

3. The dataset was loaded

4. The above steps were repeated to load the other 2 datasets 

# Task B: Exploring the Tables

In exploring the tables within the database, the table was selected to view the First 100 Rows.

1. Chicago_public_schools_table

![image](https://github.com/user-attachments/assets/43cf21df-46b3-4075-bf29-d506438b351b)

3. Chicago_crime_table

![image](https://github.com/user-attachments/assets/ffdbaa69-b85e-415e-9f61-1c1cfb8314cc)

5. Chicago_socioeconomic_table

![image](https://github.com/user-attachments/assets/1bb622f2-b7ee-49ce-b0be-048f991b918b)

# Task C: Tackling real problem using SQL queries. 

- Problem 1: How many Elementary Schools are in the dataset?

In tackling this problem, I issued the following query:

          SELECT COUNT(*) AS number_of_elementary_schools 
          FROM chicago_public_schools 
          WHERE elementary_middle_or_high_school ='ES';

![image](https://github.com/user-attachments/assets/394e694d-0288-440b-8eb4-f8ae95632555)

- Problem 2: What is the highest Safety Score?

In tackling this problem, I issued the following query:

          SELECT MAX(safety_score) AS highest_safety_score
          FROM chicago_public_schools; 

![image](https://github.com/user-attachments/assets/858fdff8-e6f8-401a-a85a-0a9c2e96afd5)

- Problem 3: Which schools have highest Safety Score?

In tackling this problem, I issued the following query:

         SELECT name_of_school, safety_score
         FROM chicago_public_schools
         ORDER BY safety_score DESC;

![image](https://github.com/user-attachments/assets/17e6a4a5-2082-4c91-b75d-d22a85ecfbb9)

Alternatively, with the query below, I was able to retrieve schools with highest saftey score:

         SELECT name_of_school, safety_score
         FROM chicago_public_schools
         WHERE safety_score = (SELECT MAX(safety_score) FROM chicago_public_schools);

![image](https://github.com/user-attachments/assets/59ad5859-b53c-496d-a3cc-cdde94326e16)

- Problem 4: What are the top 10 schools with the highest “Average Student Attendance”?
   
In tackling this problem, I issued the following query:
      
        SELECT name_of_school, average_student_attendance
        FROM chicago_public_schools
        ORDER BY average_student_attendance DESC
        LIMIT 10;

![image](https://github.com/user-attachments/assets/db4bdc75-a69f-4f67-ad82-fecf2c732d72)

- Problem 5: Retrieve the list of 5 Schools with the lowest Average Student Attendance sorted in ascending order based on attendance
   
In tackling this problem, I issued the following query:

         SELECT name_of_school, average_student_attendance
         FROM chicago_public_schools
         ORDER BY average_student_attendance ASC
         LIMIT 5;

![image](https://github.com/user-attachments/assets/cefdbe36-5df8-4963-9945-b46201e7aac5)

- Problem 6: Remove the ‘%’ sign from the above result set for Average Student Attendance column
   
In tackling this problem, I issued the following query:
   
         SELECT name_of_school, REPLACE(average_student_attendance, '%', '')
         FROM chicago_public_schools
         ORDER BY average_student_attendance ASC
         LIMIT 5;
      
![image](https://github.com/user-attachments/assets/c6bde3f7-3ec0-4f21-86d8-54e05132c0af)

    
- Problem 7: Which Schools have Average Student Attendance lower than 70%?

In tackling this problem, I issued the following query:

        SELECT name_of_school, average_student_attendance
        FROM chicago_public_schools
        WHERE average_student_attendance < '70%';

![image](https://github.com/user-attachments/assets/44c24341-5214-4269-bb68-86c7df45e6e6)

- Problem 8: Get the total College Enrollment for each Community Area

In tackling this problem, I issued the following query:

          SELECT community_area_name, SUM (college_enrollment) AS total_college_enrollment
          FROM chicago_public_schools
          GROUP BY community_area_name

![image](https://github.com/user-attachments/assets/9c178e96-353d-4695-8d46-32c889c2a63d)

- Problem 9: Get the 5 Community Areas with the least total College Enrollment sorted in ascending order
       
In tackling this problem, I issued the following query:

          SELECT community_area_name, SUM (college_enrollment) AS total_college_enrollment
          FROM chicago_public_schools
          GROUP BY community_area_name
          ORDER BY total_college_enrollment ASC
          LIMIT 5;

  ![image](https://github.com/user-attachments/assets/e8ffa4c1-40f8-41e5-90d0-4a1b36da6bdb)

- Problem 10: List 5 schools with lowest safety score.

In tackling this problem, I issued the following query:

            SELECT name_of_school, safety_score
            FROM chicago_public_schools
            ORDER BY safety_score ASC
            LIMIT 5;

  ![image](https://github.com/user-attachments/assets/0007d610-d28b-4ab0-8312-cc15a2d2f0cc)

- Problem 11: Get the hardship index for the community area which has College Enrollment of 4368

  In tackling this problem, I issued the following query:
  
       SELECT community_area_number, community_area_name, hardship_index 
       FROM chicago_socioeconomic_data
       WHERE community_area_number = (
                                  SELECT community_area_number::character varying
                                  FROM chicago_public_schools
                                  WHERE college_enrollment = 4368
      );

  ![image](https://github.com/user-attachments/assets/8194d817-efe6-4e45-9570-2188cfd12f63)

- Problem 12: Get the hardship index for the community area which has the school with the highest enrollment.

In tackling this problem, I issued the following query:
  
      SELECT community_area_number, community_area_name, hardship_index
      FROM chicago_socioeconomic_data
      WHERE community_area_number = (
                                  SELECT community_area_number::character varying
                                  FROM chicago_public_schools
                                  WHERE college_enrollment = (
                                                              SELECT MAX(college_enrollment)
                                                              FROM chicago_public_schools
      )
      );

  ![image](https://github.com/user-attachments/assets/00d9437e-a488-46f2-ae25-3fe2bc6c3ff0)

- Problem 13: Find the total number of crimes recorded in the CRIME table.

In tackling this problem, I issued the following query:

          SELECT COUNT(*)AS total_number_of_crime
          FROM chicago_crime
          WHERE primary_type IS NOT NULL;
         
![image](https://github.com/user-attachments/assets/2ee096b6-d1ba-44b6-9718-d2cd9f36448d)

- Problem 14: Retrieve first 10 rows from the CRIME table.

In tackling this problem, I issued the following query:

          SELECT * FROM chicago_crime
          LIMIT 10;

![image](https://github.com/user-attachments/assets/30da3c05-0564-455e-8342-42c3b16390e6)

- Problem 15: How many crimes involve an arrest?

In tackling this problem, I issued the following query:

            SELECT COUNT(arrest) AS number_of_arrest FROM chicago_crime
            WHERE arrest = 'TRUE';

  ![image](https://github.com/user-attachments/assets/9ebf4af5-0462-4edb-a059-0ac0c50e57a3) 

- Problem 16: Which unique types of crimes have been recorded at GAS STATION locations?

In tackling this problem, I issued the following query:

          SELECT DISTINCT(primary_type), location_description
          FROM chicago_crime
          WHERE location_description = 'GAS STATION';

![image](https://github.com/user-attachments/assets/e0f7897a-68e8-48c7-b973-8e47ff2b0b44)

- Problem 17: In the chicago_socioeconomic_data list all Community Areas whose names start with the letter ‘B’.

In tackling this problem, I issued the following query:

          SELECT community_area_name FROM chicago_socioeconomic_data
          WHERE community_area_name LIKE 'B%';

![image](https://github.com/user-attachments/assets/873767c5-b402-427b-a46c-5140cf202d65)

- Problem 18: Which schools in Community Areas 10 to 15 are healthy school certified?

In tackling this problem, I issued the following query:

          SELECT name_of_school, community_area_number
          FROM chicago_public_schools
          WHERE community_area_number BETWEEN 10 AND 15 AND (healthy_school_certified = 'Yes');

![image](https://github.com/user-attachments/assets/4448b0dd-9f22-4ae1-9990-e5b2d46817da)


- Problem 19: What is the average school Safety Score?

In tackling this problem, I issued the following query:

          SELECT AVG(CAST(safety_score AS NUMERIC)) AS average_safety_score
          FROM chicago_public_schools;

![image](https://github.com/user-attachments/assets/ff07469a-367b-4281-a376-581ea87e980e)

- Problem 20: List the top 5 Community Areas by average College Enrollment [number of students]

In tackling this problem, I issued the following query:

          SELECT community_area_name, AVG(college_enrollment) AS average_college_enrollment
          FROM chicago_public_schools
          GROUP BY community_area_name
          ORDER BY average_college_enrollment DESC
          LIMIT 5;

![image](https://github.com/user-attachments/assets/70e948c2-aa76-476e-87fe-fb83c77e35cb)

- Problem 21: Use a sub-query to determine which Community Area has the least value for school Safety Score?

In tackling this problem, I issued the following query:

          SELECT community_area_name 
          FROM chicago_public_schools 
          WHERE safety_score = (SELECT MIN(safety_score)
                               FROM chicago_public_schools);

![image](https://github.com/user-attachments/assets/abf96ec9-4376-4d8f-9111-b8db3b65c102)

- Problem 22:[Without using an explicit JOIN operator] Find the Per Capita Income of the Community Area which has a school Safety Score of 1.

In tackling this problem, I issued the following query:

          SELECT 
          
          
      






