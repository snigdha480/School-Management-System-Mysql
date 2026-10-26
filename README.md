# 🏫 School Management System - MySQL Mini Project

## 📌 Project Overview
The **School Management System** is a relational database mini-project designed to replace manual paper mark registers with a structured, queryable database. It manages academic records efficiently, capturing student details, subjects, exam schedules, and performance metrics.

---

## 🎯 Project Objectives
* Maintain centralized and secure records of students, subjects, exams, and individual scores.
* Ensure strict data validity using Primary Keys, Foreign Keys, `NOT NULL`, `UNIQUE`, and `CHECK` constraints (scoring between 0 and 100).
* Execute fast retrievals, sorting, multi-table joins, aggregations, and subqueries.
* Generate actionable academic reports, including subject averages, top-performer rankings, and automated Pass/Fail classifications.

---

## 📊 Database Schema & ERD
The database consists of **4 normalized tables**:
1. **Students:** Stores student identity (`student_id`, `first_name`, `last_name`).
2. **Subjects:** Stores unique subject names.
3. **Exams:** Tracks individual exam events and dates.
4. **Marks:** The central transaction table linking students, subjects, and exams with score values.

---

## 🛠️ Tools & Technologies Used
* **Database Management System:** MySQL
* **Environment:** MySQL Workbench
* **Language:** Structured Query Language (SQL - DDL, DML, DQL)
