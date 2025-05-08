# Employee Analysis | SQL

<img src="***EmployeeSQL***/sql.png" width=350px align=right>

## Table of Contents
* [Objective](#Objective)
* [Technologies](#Technologies)
* [ETL](#ETL)
* [Visualization](#Visualization)
* [Troubleshooting](#Troubleshooting)

# Objective:
This project demonstrates end-to-end data analysis using SQL and Python. It includes data modeling, database creation, and structured queries to explore employee demographics, salaries, and departmental distributions.

## Key Features:
* Created a relational database from six CSV files
* Defined schemas with primary/foreign keys for normalized tables
* Built an Entity Relationship Diagram (ERD)
* Performed analytical queries on employee data (e.g., salary trends, departmental analysis)
* Designed for extensibility and BI dashboard integration
      
## Use Case:
Ideal for demonstrating SQL fluency, relational data design, and basic Python data engineering in job portfolios or interviews.

# Technologies
* SQL
* SQLAlchemy
* Python
* Pandas

# ETL
## Process Documentation

#### Data Modeling
Inspect the CSVs and sketch out an ERD of the tables. ![ERD Table](***EmployeeSQL***/db_map.pdf) was created in Adobe Illustrator.

#### Data Engineering
* Create a table schema for each of the six CSV files, specifying data types, primary keys, foreign keys, and other constraints.


## E | Extract
* Downloaded CSV datasets
* Import each CSV file into the corresponding SQL table.

## T | Transform

#### Data Analysis

* Query the following details of each employee: employee number, last name, first name, gender, and salary.

```
SELECT employees.emp_no, employees.last_name, employees.first_name, employees.gender, salaries.salary
FROM employees
JOIN salaries
ON employees.emp_no = salaries.emp_no;
```

* Query employees who were hired in 1986.

```
SELECT first_name, last_name, hire_date 
FROM employees
WHERE hire_date BETWEEN '1986-01-01' AND '1987-01-01';
```

* Query the manager of each department with the following information: department number, department name, the manager's employee number, last name, first name, and start and end employment dates.

```
SELECT departments.dept_no, departments.dept_name, dept_manager.emp_no, employees.last_name, employees.first_name, dept_manager.from_date, dept_manager.to_date
FROM departments
JOIN dept_manager
ON departments.dept_no = dept_manager.dept_no
JOIN employees
ON dept_manager.emp_no = employees.emp_no;
```

* Query the department of each employee with the following information: employee number, last name, first name, and department name.

```
SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees
ON dept_emp.emp_no = employees.emp_no
JOIN departments
ON dept_emp.dept_no = departments.dept_no;
```


* Query all employees whose first name is "Hercules" and last names begin with "B."

```
SELECT first_name, last_name
FROM employees
WHERE first_name = 'Hercules'
AND last_name LIKE 'B%';

```

* Query all employees in the Sales department, including their employee number, last name, first name, and department name.

```
SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees
ON dept_emp.emp_no = employees.emp_no
JOIN departments
ON dept_emp.dept_no = departments.dept_no
WHERE departments.dept_name = 'Sales';
```

* Query all employees in the Sales and Development departments, including their employee number, last name, first name, and department name.

```
SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees
ON dept_emp.emp_no = employees.emp_no
JOIN departments
ON dept_emp.dept_no = departments.dept_no
WHERE departments.dept_name = 'Sales' 
OR departments.dept_name = 'Development';
```

* In descending order, list the frequency count of employee last names, i.e., how many employees share each last name.

```
SELECT last_name,
COUNT(last_name) AS "frequency"
FROM employees
GROUP BY last_name
ORDER BY
COUNT(last_name) DESC;
```
## L | Load

* Import the SQL database into Pandas. 

```
from sqlalchemy import create_engine
engine = create_engine('postgresql://localhost:5432/<your_db_name>')
connection = engine.connect()
```

# Visualization

* Create a histogram to visualize the most common salary ranges for employees.

* Create a bar chart of average salary by title.


# Troubleshooting
