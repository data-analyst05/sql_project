# Pewlett Hackard Employee Database Project

## Introduction

This project involves the design, creation, and analysis of a relational database using SQL for Pewlett Hackard, a fictional company. The goal of this project is to model the data, engineer the database, and perform data analysis on employee records from the 1980s and 1990s.

## Table of Contents

1. [Data Modeling](#data-modeling)
2. [Data Engineering](#data-engineering)
3. [Data Analysis](#data-analysis)
4. [Requirements](#requirements)
5. [Getting Started](#getting-started)
6. [Dependencies](#dependencies)
7. [Installation](#installation)
8. [SQL Table](#sql_table)


## Data Modeling

- Inspected the provided CSV files.
- Designed an Entity Relationship Diagram (ERD) to visualize table relationships on `https://app.quickdatabasediagrams.com/`.
- Created table schemas specifying data types, primary keys, foreign keys, and constraints.

## Data Engineering

- Implemented the table schemas in an SQL database.
- Imported data from the CSV files into their respective SQL tables.
- Established relationships between tables using foreign keys.
- Ensured correct data types and constraints were applied to columns.

## Data Analysis

- Executed SQL queries to answer various questions about the employee data.
- Generated reports on employee information, department managers, and more.


## Getting Started

To get started with this project, follow these steps:

### Dependencies

- SQL database management system (e.g. PostgreSQL)
- SQL client or interface (e.g., pgAdmin, DBeaver)

### Installation

1. Clone the project repository:

   ```bash
   git clone https://github.com/data-analyst05/sql_project.git

### Sql_table

```sql
-- Create a table to store department information.
CREATE TABLE departments (
    dept_no CHAR(4) PRIMARY KEY, -- Department number (unique identifier)
    dept_name VARCHAR(30) NOT NULL -- Department name (not nullable)
);

-- Create a table to represent the many-to-many relationship between employees and departments.
CREATE TABLE dept_emp (
    emp_no INT NOT NULL, -- Employee number (not nullable)
    dept_no CHAR(4) NOT NULL, -- Department number (not nullable)
    FOREIGN KEY (emp_no) REFERENCES employees(emp_no), -- Reference to employees table
    FOREIGN KEY (dept_no) REFERENCES departments(dept_no) -- Reference to departments table
);

-- Create a table to store department manager assignments.
CREATE TABLE dept_manager (
    dept_no CHAR(4) NOT NULL, -- Department number (not nullable)
    emp_no INT NOT NULL, -- Employee number (not nullable)
    FOREIGN KEY (emp_no) REFERENCES employees(emp_no), -- Reference to employees table
    FOREIGN KEY (dept_no) REFERENCES departments(dept_no) -- Reference to departments table
);

-- Create a table to store employee information.
CREATE TABLE employees (
    emp_no INT PRIMARY KEY, -- Employee number (unique identifier)
    emp_title_id CHAR(5) NOT NULL, -- Employee title identifier (not nullable)
    birth_date DATE NOT NULL, -- Employee's birth date (not nullable)
    first_name VARCHAR(30) NOT NULL, -- First name of the employee (not nullable)
    last_name VARCHAR(30) NOT NULL, -- Last name of the employee (not nullable)
    sex CHAR(1) NOT NULL, -- Gender of the employee (not nullable)
    hire_date DATE NOT NULL, -- Date of hire (not nullable)
    FOREIGN KEY (emp_title_id) REFERENCES titles(title_id) -- Reference to titles table
);

-- Create a table to store salary information for employees.
CREATE TABLE salaries (
    emp_no INT PRIMARY KEY, -- Employee number (unique identifier)
    salary INT NOT NULL, -- Salary amount (not nullable)
    FOREIGN KEY (emp_no) REFERENCES employees(emp_no) -- Reference to employees table
);

-- Create a table to store employee titles.
CREATE TABLE titles (
    title_id CHAR(5) PRIMARY KEY, -- Title identifier (unique identifier)
    title VARCHAR(30) NOT NULL -- Title name (not nullable)
);

