# Project Name: IT Company Database Management System

## Table of Contents
1. [Introduction](#introduction)
2. [Database Schema](#database-schema)
3. [Integrity Rules](#integrity-rules)
4. [Partitioning](#partitioning)
5. [Access Rights](#access-rights)
6. [Management of Values](#management-of-values)
7. [Triggers and Trigger Graph](#triggers-and-trigger-graph)
8. [Security Issues and Measures](#security-issues-and-measures)
9. [Backup and Recovery Plan](#backup-and-recovery-plan)

---

## Introduction
This document outlines the design and management of a database system for an IT company. The goal is to create a robust and secure system that efficiently handles customers, projects, employees, user groups, roles, and departments for the company. This system will be used by approximately 50 concurrent users and must accommodate the company's 100 employees, multiple projects, various departments, and three office locations within one country.

## Database Schema
The database schema is based on the provided ER model and consists of the following tables:
1. Role
2. User Group
3. Location
4. Customer
5. Project
6. Department
7. Employee
8. Employee_Role
9. Employee_UserGroup
10. Project_Employee

## Integrity Rules
### ON UPDATE and ON DELETE Rules
- **Project Table**: The `CID` field in the Project table is a foreign key referencing the Customer table's primary key. The ON UPDATE rule should be set to Cascade to update project data when a customer's ID changes. The ON DELETE rule should be set to No Action to prevent accidental deletion of projects.

- **Customer Table**: The `LID` field in the Customer table is a foreign key referencing the Location table's primary key. ON UPDATE should be set to Cascade to update customer location data. ON DELETE should be set to Set NULL to retain customer information even if the location is deleted.

- **User Group Table**: While the User Group table doesn't have direct foreign keys, the Employee_UserGroup table facilitates the many-to-many relationship between Employee and User Group. Both ON UPDATE and ON DELETE for Employee_UserGroup should be set to Cascade to maintain consistency.

- **Employee Table**: The `DepID` field in the Employee table is a foreign key referencing the Department table's primary key. ON DELETE should be set to Set NULL to allow employees to remain in the system even if their department is deleted. ON UPDATE should be set to Cascade to propagate department updates.

## Partitioning
Two different partitioning strategies can be employed:
1. **Horizontal Partitioning**: Partition the Employee table as it has the potential to grow significantly with 100 employees. Partition based on criteria like employee ID ranges, departments, or locations.

2. **Vertical Partitioning**: This approach involves splitting a table into subtables with fewer columns. Depending on query patterns, you could split large tables like Project into essential and non-essential data to optimize performance.

## Access Rights
Access rights should be defined using PostgreSQL roles and permissions. Each user group should have access to the projects they work on. Group roles should be created and granted appropriate permissions, ensuring data security.

```sql
-- Example of creating a group role and granting permissions
CREATE ROLE developers;
GRANT SELECT, INSERT, UPDATE, DELETE ON TABLE project TO developers;
```

## Management of Values
### Default Values
- Set a default value for the `Country` field in the Location table since the company has offices in one country. This ensures consistency in data entry.

### Check Constraints
- Add a check constraint to the Project table to ensure that the `StartDate` field is always greater than the current date.

### Handling NULL Values
- Use the PostgreSQL `NULLIF` function to handle NULL values when necessary, ensuring that null values are appropriately managed.

## Triggers and Trigger Graph
Three useful triggers can be implemented in the database:
1. **EmpAuditTrigger**: After an employee is inserted, create an entry in the Employee_Audit table to track employee changes.

2. **Project Deadline Update Trigger**: This trigger should execute when the deadline of a project is updated. It can log changes in a Project_Update table.

3. **Project Audit Trigger**: Implement a trigger to audit project entries. Whenever a project is inserted, record the entry time and project duration in the Project_Audit table.

![Trigger Graph](trigger_graph.png)

## Security Issues and Measures
### Security Issues
1. **Deployment Negligence**: Security breaches can occur due to insufficient testing during deployment. Vulnerabilities may go undetected.

2. **Flaws in Database Features**: Unused or less-tested features can become security risks if exploited by malicious users.

3. **Poor Encryption Standards**: Insufficient data encryption during transmission can lead to data interception.

### Countermeasures
1. **Penetration Testing**: Conduct thorough penetration testing during deployment to identify and rectify security flaws.

2. **Feature Removal**: Remove unnecessary or less-used features to minimize potential attack vectors.

3. **Encryption**: Implement industry-standard encryption schemes (SSL/TLS) to secure data during transmission.

## Backup and Recovery Plan
### Backup Method and Schedule
- Schedule regular complete backups of the database to ensure data reliability and security. Since the storage requirements are not excessively high, complete backups offer comprehensive protection.

### Disaster Scenarios
1. **Data Loss Due to Lack of Backup**: Regular backups mitigate the risk of data loss.

2. **Security Breach**: Proper encryption and access controls reduce the likelihood of security breaches.

3. **Server Downtime**: To address server downtime, consider redundancy and failover solutions.

4. **Extremely Unlikely Disaster**: In the case of a highly unlikely disaster, such as a catastrophic data center failure, having off-site backups is crucial for recovery.

### Recovery Method
- In the event of data loss or server downtime, restore the database from the latest backup. Ensure that off-site backups are available for extreme scenarios. Implement redundancy and failover mechanisms for high availability.

---

This document provides a comprehensive overview of the database management system for the IT company, including schema design, integrity rules, partitioning, access rights, data management, triggers, security measures, and backup and recovery plans. The implementation of these strategies will result in a robust and secure database system that meets the company's needs.
