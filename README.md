# SQL-challenge
As a new data engineer at Pewlett Hackard, I researched employee data from the 1980s and 1990s using six CSV files. I created an ERD, designed table schemas, and imported the CSV data into a SQL database. Then, I performed various queries to analyze the data.

# Creating an ERD with QuickDBD
Building a QuickDBD (Quick Database Diagram) is essential for effectively visualizing a database schema, which significantly enhances understanding by providing a clear view of table structures, relationships, and key constraints. It improves communication with stakeholders by offering a straightforward representation of data models, aiding in design and planning by facilitating rapid adjustments and identifying potential issues early. QuickDBD simplifies troubleshooting by quickly revealing design problems and serves as valuable documentation for future reference. Additionally, it supports design validation, ensuring all requirements are met, and boosts development efficiency by allowing developers to implement and query the database with a better grasp of its structure.

![alt text](https://github.com/biddlebird/sql-challenge/blob/main/Data%20Analysis%20Tables/QuickDBD.jpg)
---

# Design Table Schemas

In pgAdmin 4, you can import a CSV file into a table by following these steps:

1. **Open pgAdmin 4** and connect to your PostgreSQL database.
2. **Navigate to the Table**: In the Object browser, expand your database, schema, and then the "Tables" node to find the table you want to import the CSV data into.
3. **Right-Click on the Table**: Right-click on the table into which you want to import data.
4. **Select "Import/Export Data"**: From the context menu, choose the "Import/Export Data" option.
5. **Configure Import Settings**:
   - **File Format**: Set the format to "CSV".
   - **File Path**: Browse and select your CSV file.
   - **Options**: Adjust delimiter, quote, and other CSV-specific options as needed.
6. **Start the Import**: Click the "OK" or "Import" button to begin importing the data.

The CSV file will be read and its contents will be imported into the selected table.

```sql
CREATE TABLE Departments (
    dept_no VARCHAR(10) NOT NULL,
    dept_name VARCHAR(50) NOT NULL,
    CONSTRAINT pk_Departments PRIMARY KEY (dept_no)
);

CREATE TABLE Titles (
    title_id VARCHAR(10) NOT NULL,
    title VARCHAR(50) NOT NULL,
    CONSTRAINT pk_Titles PRIMARY KEY (title_id)
);

CREATE TABLE Employees (
    emp_no INT NOT NULL,
    emp_title_id VARCHAR(10) NOT NULL,
    birth_date DATE NOT NULL,
    first_name VARCHAR(25) NOT NULL,
    last_name VARCHAR(25) NOT NULL,
    sex CHAR(1) NOT NULL,
    hire_date DATE NOT NULL,
    CONSTRAINT pk_Employees PRIMARY KEY (emp_no)
);

CREATE TABLE Dept_Employees (
    emp_no INT NOT NULL,
    dept_no VARCHAR(10) NOT NULL,
    CONSTRAINT pk_Dept_Employees PRIMARY KEY (emp_no, dept_no)
);

CREATE TABLE Salaries (
    emp_no INT NOT NULL,
    salary INT NOT NULL,
    CONSTRAINT pk_Salaries PRIMARY KEY (emp_no)
);

CREATE TABLE Dept_Managers (
    dept_no VARCHAR(10) NOT NULL,
    emp_no INT NOT NULL,
    CONSTRAINT pk_Dept_Managers PRIMARY KEY (emp_no, dept_no)
);
```
## Tasks

Below are the tasks that need to be completed along with a brief description of what each task entails.

### 1. List the Employee Number, Last Name, First Name, Sex, and Salary of Each Employee
- **Objective:** Retrieve basic employee details including their salary.
- **Required Tables:** `Employees`, `Salaries`
- **Query:** Write a query that joins the `Employees` table with the `Salaries` table based on the employee number.

![alt text](https://github.com/biddlebird/sql-challenge/blob/main/Data%20Analysis%20Tables/1.empno.lname.fname.sex.salary.jpg)

### 2. List the First Name, Last Name, and Hire Date for the Employees Who Were Hired in 1986
- **Objective:** Retrieve details of employees who were hired in the year 1986.
- **Required Table:** `Employees`
- **Query:** Filter the `Employees` table based on the `hire_date` column to include only those records from 1986.

![alt text](https://github.com/biddlebird/sql-challenge/blob/main/Data%20Analysis%20Tables/2.1986.jpg)

### 3. List the Manager of Each Department Along with Their Department Number, Department Name, Employee Number, Last Name, and First Name
- **Objective:** Identify the managers of each department and list their details along with the department information.
- **Required Tables:** `Departments`, `Dept_Managers`, `Employees`
- **Query:** Join the `Departments`, `Dept_Managers`, and `Employees` tables to match department managers with their respective departments.

![alt text](https://github.com/biddlebird/sql-challenge/blob/main/Data%20Analysis%20Tables/3.deptnum.deptname.emno.last.first.jpg)

### 4. List the Department Number for Each Employee Along with That Employee’s Employee Number, Last Name, First Name, and Department Name
- **Objective:** Retrieve department and employee details for each employee.
- **Required Tables:** `Departments`, `Dept_Employees`, `Employees`
- **Query:** Join the `Departments`, `Dept_Employees`, and `Employees` tables to list employees along with their department details.

![alt text](https://github.com/biddlebird/sql-challenge/blob/main/Data%20Analysis%20Tables/4.deptnum.empnumlas.first.deptname.jpg)

### 5. List First Name, Last Name, and Sex of Each Employee Whose First Name Is Hercules and Whose Last Name Begins with the Letter B
- **Objective:** Find specific employees with the first name "Hercules" and last names starting with "B".
- **Required Table:** `Employees`
- **Query:** Filter the `Employees` table based on the `first_name` and `last_name` columns.

![alt text](https://github.com/biddlebird/sql-challenge/blob/main/Data%20Analysis%20Tables/5.first.last.sex.Hercules.B.jpg)

### 6. List Each Employee in the Sales Department, Including Their Employee Number, Last Name, and First Name
- **Objective:** Identify all employees who work in the Sales department.
- **Required Tables:** `Employees`, `Departments`, `Dept_Employees`
- **Query:** Join the necessary tables to retrieve employees who are part of the Sales department.

![alt text](https://github.com/biddlebird/sql-challenge/blob/main/Data%20Analysis%20Tables/6.Sales.jpg)

### 7. List Each Employee in the Sales and Development Departments, Including Their Employee Number, Last Name, First Name, and Department Name
- **Objective:** Retrieve details of employees who work in either the Sales or Development departments.
- **Required Tables:** `Employees`, `Departments`, `Dept_Employees`
- **Query:** Filter the joined tables to include employees in the Sales and Development departments.


![alt text](https://github.com/biddlebird/sql-challenge/blob/main/Data%20Analysis%20Tables/7.Sales.Development.jpg)

### 8. List the Frequency Counts, in Descending Order, of All the Employee Last Names
- **Objective:** Determine how many employees share each last name and sort the results in descending order of frequency.
- **Required Table:** `Employees`
- **Query:** Use a `GROUP BY` clause on the `last_name` column and sort the result by the count of last names.

![alt text](https://github.com/biddlebird/sql-challenge/blob/main/Data%20Analysis%20Tables/8.frequencycount.jpg)


Full code can be found [Here :)](https://github.com/biddlebird/sql-challenge/blob/main/Coding.sql)

## How to Run the Queries

1. **Set Up the Database:** Ensure you have access to a SQL environment where the database schema is set up with the required tables (`Employees`, `Salaries`, `Departments`, `Dept_Managers`, `Dept_Employees`).

2. **Execute the Queries:** Run each SQL query sequentially to retrieve the required data for each task.

3. **Review the Results:** The results should provide the necessary data as described in each task. If any adjustments are needed based on the results, modify the queries accordingly.

## Conclusion

This assignment involves applying SQL skills to extract and analyze employee data from a database. The tasks are designed to practice joining tables, filtering data, and performing aggregations. Successful completion of these tasks will demonstrate proficiency in SQL and the ability to handle real-world data analysis scenarios.
