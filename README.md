 Employee Attendance Monitoring and Access Control

## Project Description
In this project, I developed a system to monitor employee attendance and manage access permissions using SQL. The goal was to ensure compliance with company policies, track employee activity, and restrict access to sensitive areas based on role and department. By applying SQL filters and queries, I was able to retrieve specific data to support these objectives.

## Language Used
**SQL**

## Project Walk-through

# 1. Retrieve Employees with Late Arrivals
To enforce punctuality, I was tasked with identifying employees who arrived late (after 9:00 AM). The following SQL query demonstrates how I filtered the attendance logs to retrieve late arrivals:

```sql
SELECT * 
FROM attendance 
WHERE arrival_time > '09:00:00';
```
### Query Results:
```sql
+-------------+-----------+--------------+----------------+------------+
| employee_id | username  | arrival_time | departure_time | date       |
+-------------+-----------+--------------+----------------+------------+
| 1001        | bmoreno   | 09:15:00     | 17:30:00       | 2023-10-01 |
| 1003        | jdarosa   | 09:45:00     | 18:00:00       | 2023-10-01 |
| 1005        | tshah     | 09:30:00     | 17:45:00       | 2023-10-02 |
+-------------+-----------+--------------+----------------+------------+
```
## Explanation:

I selected all data from the attendance table.

Used the WHERE clause to filter for employees with an arrival_time after 9:00 AM.

# 2. Retrieve Employees Accessing Restricted Areas
To ensure compliance with security policies, I was asked to identify employees who accessed restricted areas without proper authorization. The following SQL query demonstrates how I filtered the access logs:

```sql
SELECT * 
FROM access_logs 
WHERE area = 'Restricted' AND authorization_status = 'Unauthorized';
```
### Query Results:
```sql
+-------------+-----------+--------------+----------------------+----------------------+
| employee_id | username  | area         | access_time          | authorization_status |
+-------------+-----------+--------------+----------------------+----------------------+
| 1002        | elarson   | Restricted   | 2023-10-01 14:30:00  | Unauthorized         |
| 1004        | fbautist  | Restricted   | 2023-10-02 10:15:00  | Unauthorized         |
+-------------+-----------+--------------+----------------------+----------------------+
```
## Explanation:
I selected all data from the access_logs table.
Used the WHERE clause to filter for entries where the area is "Restricted" and the authorization_status is "Unauthorized".

# 3. Retrieve Employees with Excessive Overtime
To monitor employee workload and ensure compliance with labor laws, I was tasked with identifying employees who worked more than 10 hours in a single day. The following SQL query demonstrates how I calculated and filtered overtime:
```sql
SELECT employee_id, username, date, 
       TIMESTAMPDIFF(HOUR, arrival_time, departure_time) AS hours_worked
FROM attendance 
WHERE TIMESTAMPDIFF(HOUR, arrival_time, departure_time) > 10;
```
### Query Results:  
```sql
+-------------+-----------+------------+--------------+
| employee_id | username  | date       | hours_worked |
+-------------+-----------+------------+--------------+
| 1006        | pwashing  | 2023-10-01 | 11           |
| 1007        | aestrada  | 2023-10-02 | 12           |
+-------------+-----------+------------+--------------+
```
## Explanation:
I selected the employee_id, username, date, and calculated the hours_worked using the TIMESTAMPDIFF function.
Used the WHERE clause to filter for employees who worked more than 10 hours.

# 4. Retrieve Employees with Expired Access Permissions
To maintain security, I was asked to identify employees with expired access permissions. The following SQL query demonstrates how I filtered the access logs:
```sql
SELECT * 
FROM access_permissions 
WHERE expiration_date < CURDATE();
```
### Query Results:
```sql
+-------------+-----------+--------------+-----------------+
| employee_id | username  | area         | expiration_date |
+-------------+-----------+--------------+-----------------+
| 1008        | dkot      | Server Room  | 2023-09-30      |
| 1009        | jrafael   | Data Center  | 2023-09-28      |
+-------------+-----------+--------------+-----------------+
```
## Explanation:
I selected all data from the access_permissions table.
Used the WHERE clause to filter for entries where the expiration_date is before the current date (CURDATE()).

# 5. Retrieve Employees by Department for Security Training
To organize security training sessions, I was asked to retrieve a list of employees by department. The following SQL query demonstrates how I filtered the data:
```sql
SELECT * 
FROM employees 
WHERE department = 'Finance';
```
### Query Results: 
```sql
+-------------+-----------+------------+--------------+
| employee_id | username  | department | office       |
+-------------+-----------+------------+--------------+
| 1010        | tshah     | Finance    | East-170     |
| 1011        | bmoreno   | Finance    | Central-276  |
+-------------+-----------+------------+--------------+
```
## Explanation:
I selected all data from the employees table.
Used the WHERE clause to filter for employees in the "Finance" department.

## Summary
In this project, I applied various SQL filters and queries to monitor employee attendance, manage access permissions, and ensure compliance with company policies. By using operators like WHERE, AND, and functions like TIMESTAMPDIFF, I was able to retrieve specific data to support security and operational objectives. This project highlights the importance of SQL in managing employee activity and maintaining organizational security.
