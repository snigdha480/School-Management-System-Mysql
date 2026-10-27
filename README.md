# School Management System (MySQL)

A relational database project that manages students, subjects, exams and marks for a school. It includes the schema, sample data, and 9 analytical SQL queries covering filtering, sorting, joins, aggregation, subqueries and conditional logic.

**Repository:** https://github.com/snigdha480/School-Management-System-Mysql

# Project Overview

The School Management System stores academic records in a normalized MySQL database. Each mark is linked to a student, a subject and an exam, so reports such as subject averages, exam totals, top performers and pass/fail status can be generated with plain SQL.

## Features

- Normalized schema with 4 tables and primary/foreign key relationships
- Data integrity through `NOT NULL`, `UNIQUE`, `CHECK` and foreign key constraints
- Sample dataset: 6 students, 5 subjects, 3 exams, 16 mark entries
- 9 queries demonstrating:
  - Basic retrieval and filtering (`SELECT`, `WHERE`)
  - Sorting (`ORDER BY`)
  - Multi-table joins (`JOIN`)
  - Aggregations (`AVG`, `COUNT`, `SUM`, `MAX`, `GROUP BY`, `HAVING`)
  - Subqueries
  - Conditional logic (`CASE WHEN`) and string functions (`CONCAT`)

# Tech Stack

| Component | Technology |
|-----------|------------|
| Database  | MySQL 8.x |
| Language  | SQL |
| Tools     | MySQL Workbench / MySQL CLI |

## Project Structure

```
School-Management-System-Mysql/
├── school_management.sql   # Schema, sample data and all queries
├── docs/                   # Project report, questions and presentations
└── README.md
```

## Setup and Run

### Prerequisites
- MySQL Server 8.0 or later
- MySQL Workbench or the MySQL command-line client

### Option 1: MySQL CLI
```bash
# 1. Clone the repository
git clone https://github.com/snigdha480/School-Management-System-Mysql.git
cd School-Management-System-Mysql

# 2. Run the script (you will be prompted for your password)
mysql -u root -p < school_management.sql

# 3. Open MySQL and verify
mysql -u root -p
```
```sql
USE schoolmanagement;
SHOW TABLES;
SELECT * FROM students;
```

### Option 2: MySQL Workbench
1. Open MySQL Workbench and connect to your server.
2. Go to **File → Open SQL Script** and select `school_management.sql`.
3. Click the **Execute** (lightning bolt) button.
4. Refresh the schemas panel to see the `schoolmanagement` database.

> **Note:** The script runs `DROP DATABASE IF EXISTS schoolmanagement;` at the start, so any existing database with this name will be replaced.

## Environment Variables

This project is pure SQL and does not need any environment variables or `.env` file.
Only your own MySQL credentials are needed to connect:

| Item | Example |
|------|---------|
| Host | `localhost` |
| Port | `3306` |
| User | `root` |
| Password | your MySQL password |

## API / Query Interface

This project does not include a REST API or application server. The interface to the data is the set of SQL queries in `school_management.sql`. Each query below can be run directly in MySQL after setup.

| # | Query Purpose | Output Columns | Expected Result (sample data) |
|---|---------------|----------------|-------------------------------|
| Q1 | List all students | `first_name`, `last_name` | 6 rows |
| Q2 | Marks with score above 80 | all `marks` columns | 6 rows |
| Q3 | Exams, most recent first | all `exams` columns | Annual 2025, Half-Yearly 2024, Unit Test 1 2024 |
| Q4 | Student, subject and score for every mark | `first_name`, `subject_name`, `score` | 16 rows |
| Q5 | Average score per subject | `subject_name`, `average_score` | 5 rows |
| Q6 | Marks recorded for Aarav Sharma | `total_marks` | 7 |
| Q7 | Student with the highest single score | `first_name`, `last_name` | Ananya Singh (95) |
| Q8 | Exams with total score above 250 | `exam_name`, `total_score` | Half-Yearly 2024 (633 total? see note) |
| Q9 | Pass/Fail status (Pass if score ≥ 70) | `student_name`, `subject_name`, `score`, `status` | 16 rows |

### Usage Example

```sql
USE schoolmanagement;

-- Q5. Subject averages
SELECT sub.subject_name, AVG(m.score) AS average_score
FROM marks m
JOIN subjects sub ON m.subject_id = sub.subject_id
GROUP BY sub.subject_id, sub.subject_name;
```

## Database Notes

### Database Name
`schoolmanagement`

### Entity Relationship

```
Students (1) ────< Marks >──── (1) Subjects
                     │
                     └──── (1) Exams
```

One student can have many marks, one subject can appear in many marks, and one exam can contain many marks. `Marks` is the linking table.

### Tables

| Table | Columns | Description |
|-------|---------|-------------|
| `Students` | `student_id` (PK, auto-increment), `first_name`, `last_name` | Student records |
| `Subjects` | `subject_id` (PK, auto-increment), `subject_name` (unique) | Subjects offered |
| `Exams` | `exam_id` (PK, auto-increment), `exam_name` (unique), `exam_date` | Exams conducted |
| `Marks` | `mark_id` (PK, auto-increment), `student_id` (FK), `subject_id` (FK), `exam_id` (FK), `score` | Score per student, subject and exam |

### Constraints

| Constraint | Applied To | Purpose |
|------------|-----------|---------|
| `PRIMARY KEY` + `AUTO_INCREMENT` | All `*_id` columns | Unique row identification |
| `NOT NULL` | Names, dates, scores and all foreign keys | No missing data |
| `UNIQUE` | `subject_name`, `exam_name` | No duplicate subjects or exams |
| `CHECK (score BETWEEN 0 AND 100)` | `Marks.score` | Valid score range only |
| `FOREIGN KEY` | `Marks.student_id`, `Marks.subject_id`, `Marks.exam_id` | Marks must reference existing records |

### Sample Data
- **Students:** Aarav Sharma, Priya Patel, Rohan Verma, Ananya Singh, Karthik Reddy, Sneha Iyer
- **Subjects:** Mathematics, Science, Hindi, English, Social Studies
- **Exams:** Unit Test 1 2024 (2024-07-15), Half-Yearly 2024 (2024-10-10), Annual 2025 (2025-03-20)
- **Marks:** 16 entries across the 3 exams

## Author

| Name | Role |
|------|------|
| Snigdha | Sole developer: database design, sample data, SQL queries, testing and documentation |

## License

This project was created for educational purposes.
