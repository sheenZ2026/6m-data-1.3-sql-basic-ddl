# **Pre-Study Material: Introduction to SQL Data Definition Language (DDL)**

Welcome to the Data Science Bootcamp\! To make the most of our 3-hour live session, please review this material beforehand. This "flipped classroom" approach allows us to focus our live time on hands-on practice and troubleshooting.

## **1\. Core Concepts: What is a Database?**

Think of a database as a highly organized digital filing cabinet. In Data Science, we primarily use **Relational Databases (RDBMS)**.

* **Database:** The container for everything (e.g., "School\_System").  
* **Schema:** A folder inside the database used to group related items (e.g., "Enrollment\_Data").  
* **Table:** A specific spreadsheet within a schema (e.g., "Students").  
* **Columns (Fields):** The categories of data (e.g., Name, Age, Email).  
* **Rows (Records):** Individual entries (e.g., "John Doe, 25, john@example.com").

### **What is DDL?**

**Data Definition Language (DDL)** is the subset of SQL used to **build and modify the structure** of the database. While other SQL parts handle data entry, DDL creates the "skeleton."

### Video introduction
- [SQL DDL - The Blueprint for Data](https://youtu.be/adACCuMFjac)

## **2\. Our Toolkit**

We will be using two modern, lightweight tools:

1. **DuckDB:** A fast, "in-process" database engine. Unlike traditional databases (like MySQL), DuckDB doesn't require a complex server setup. It stores everything in a single file on your computer, making it perfect for data science.  
2. **DbGate:** A user-friendly database manager. It provides a visual interface to see your tables, run queries, and manage your data.

## **3\. Basic SQL Syntax to Know**

You don't need to memorize these yet, but try to understand what they do:

### **Creating Structure**

* CREATE SCHEMA: Creates a new "folder" in the database.  
* CREATE TABLE: Defines a new table and its columns.  
* INTEGER, VARCHAR, DATE: These are **Data Types**. They tell the database if a column should store numbers, text, or dates.

### **Managing Structure**

* ALTER TABLE: Used to add or change columns in an existing table.  
* DROP TABLE: Deletes a table entirely. **(Be careful: this cannot be undone\!)**

## **4\. Setup Instructions (Action Required)**

Please complete these steps before the live session:

1. **Install DbGate:** Download and install the version for your operating system from [dbgate.org](https://dbgate.org/).  
2. **Download the Database File:** Ensure you have the file db/unit-1-3.db saved on your machine (provided in the course portal).  
3. **Watch (Optional/5 mins):** Search YouTube for "What is a Primary Key vs Foreign Key" to get a head start on Section 2 of our lesson.

## **5\. Check Your Understanding**

Try to answer these questions mentally:

1. If I want to add a "Phone Number" column to an existing table, which command would I use?  
2. What is the difference between a Schema and a Table?  
3. Why might a Data Scientist prefer DuckDB over a heavy database server?

**Questions?** Bring them to the Q\&A session at the start of our live class\!
