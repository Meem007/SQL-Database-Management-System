# Project Name: IT Company Database Management System

## README

This repository contains the documentation for the design and management of a database system for an IT company. The goal of this project is to create a robust and efficient database system to manage customers, projects, employees, user groups, and roles for the company. This README provides an overview of the project and its key components.

### Project Overview

In this project, we are tasked with designing a comprehensive database system for an IT company. The company has specific requirements and constraints that need to be addressed in the design of the database. Here are some key considerations:

- The company has 100 employees.
- There are approximately 50 concurrent users at a time.
- The company manages dozens of projects.
- The company has departments, including HR, Software, Data, ICT, and Customer support.
- The company has offices in three different locations within one country.

### Task 1: Relational Model

We have implemented a database schema based on the provided ER diagram. The schema consists of 10 tables, including Role, User Group, Location, Customer, Project, Department, Employee, Employee_Role, Employee_UserGroup, and Project_Employee.

### Task 2: Integrity Rules

We have defined ON UPDATE and ON DELETE rules for the Project, Customer, User Group, and Employee tables to maintain data integrity.

### Task 3: Partitioning

We have explored two different ways to partition the data to improve query performance and scalability.

### Task 4: Access Rights

We have defined access rights using PostgreSQL syntax, ensuring that each user group has access to the projects they work on.

### Task 5: Management of Values

We have defined default values, check constraints, and how to manage NULL values in the database schema.

### Task 6: Triggers and Trigger Graph

We have created three useful triggers using PostgreSQL syntax and provided a trigger graph to illustrate their relationships.

### Task 7: Security Issues and Measures

We have identified three security issues related to database design and provided countermeasures to address them.

### Task 8: Backup and Recovery

We have defined the backup method and schedule, along with recovery methods for various disaster scenarios.

### Conclusion

This project aims to create a well-structured and secure database system that meets the needs of the IT company. The documentation provided here outlines the design decisions, integrity rules, access rights, triggers, security measures, and backup strategies employed in the system. Please refer to the full project report for more detailed information and implementation details.

For the complete project report, including SQL scripts, diagrams, and additional details, please refer to the project files in this repository.
