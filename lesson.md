# **In data science, data is the new oil. DDL is how we build the refinery.**

## **SQL Data Definition Language (DDL) with DuckDB**


**Tools:** [DbGate](https://dbgate.org/), [DuckDB](https://duckdb.org/)



---
## **Section 1: Fundamentals of Database Structure & Connections**

**Learning Objective:** By the end of this section, learners will be able to connect to a DuckDB database using DbGate and perform basic schema and table creation, alter table and drop (delete) table.

* **Theory Summary/Recap:**  
  * What is an RDBMS? Understanding the relationship between databases, schemas, and tables.
  * What is the Difference between Excel and a Relational Database?

---
<details>
  <summary>Introduction to DuckDB: Why we use an in-process engine for data science.</summary>
  
### DuckDB is an in-process, analytical database management system (DBMS) specifically designed to address the needs of data scientists by bringing the database closer to the data itself. This approach is favored in data science for several key reasons: 
#### Why an In-Process Engine is Beneficial for Data Science
  * Zero-Copy Data Transfer: Data science often involves rapidly iterating on large datasets. DuckDB runs within the same process as the application (e.g., a Python script or R session), eliminating the overhead of inter-process communication or network transfers. This "zero-copy" data transfer drastically improves performance and efficiency when working with local data.
  * Ease of Deployment and No Server Management: As an in-process system, DuckDB does not require a separate server to be installed, configured, or managed. This simplifies the setup, making it an excellent tool for local analysis, laptop use, and environments where users lack administrative privileges or the need for a dedicated data warehouse team.
  * High Performance for Analytical Workloads: DuckDB is optimized for Online Analytical Processing (OLAP) queries, which are common in data science. It employs columnar storage and advanced query optimization techniques, enabling it to efficiently handle the large, complex, and often ad-hoc queries characteristic of data analysis.
  * Seamless Integration with Data Science Ecosystems: DuckDB offers robust and native integrations with popular data science tools and languages, such as Python (via the duckdb library), R, and Java. It can directly query data frames in memory and read from various file formats (like CSV, Parquet, and JSON), streamlining data ingestion and manipulation within existing workflows.
  * Portability and Reproducibility: Because the database runs within the application and the data can be stored in a single file, analyses conducted with DuckDB are highly portable. This simplifies sharing reproducible research and results, as the entire environment and data can be easily packaged and moved. 
  * In summary, DuckDB's design as an in-process, analytical database provides data scientists with a fast, easy-to-use, and highly integrated tool that removes common bottlenecks associated with traditional client-server database architectures. Users can learn more about its features and get started with the official DuckDB documentation and explore its capabilities. 

</details>

<details>
  <summary>Introduction to DbGate: A cross-platform database manager.</summary>
  
### DbGate is a free, cross-platform database manager and data editor for SQL and NoSQL databases (MySQL, PostgreSQL, MongoDB, etc.), available as a desktop app (Win/Mac/Linux) or a web app, offering features like data browsing/editing (Excel-like), visual query design, schema comparison, data visualization, and AI-powered SQL chat for simplified database management. It's designed for ease of use, allowing quick data interaction in the browser or desktop with powerful tools for developers and DBAs. 
#### Key Features
  * Unified Interface: Manage various databases (SQL, NoSQL) from one tool.
  * Data Editing: Edit data directly in tables with Excel-like features (copy/paste, sorting, filtering).
  * Querying: Includes a query console with auto-completion, visual query designer, and AI chat for generating SQL.
  * Data Visualization: Create charts and ER diagrams from your data.
  * Import/Export: Supports multiple formats (CSV, JSON, XML, Excel, etc.).
  * Cross-Platform: Works on Windows, macOS, Linux, and in a web browser.
  * Open Source: Free under GPL-3.0 license for most uses, with premium options available. 
#### How it Works
  * Desktop App: A native application for your computer.
  * Web App: Can run in a browser (via Docker or NPM) or be self-hosted as an ASP.NET Core application for browser access. 
</details>


---
* **Demo & Hands-on Workshop:**
   
1. **Connecting to the Database:**
  
  * You can connect to any database using an SQL client or IDE like DbGate, which supports a broad range of popular SQL and NoSQL databases, including MySQL, PostgreSQL, SQL Server, MongoDB, SQLite, Oracle, Redis, CockroachDB, MariaDB, Amazon Redshift, ClickHouse, Cassandra, DuckDB, Firebird, and Firestore, with some premium features for cloud databases like Azure. It acts as a universal manager, allowing you to connect to and work with multiple database types from a single application.

  * For this lesson, we'll use DuckDB, a lightweight, in-process SQL database engine.

  * Open **DbGate**.  
  
  * Create a new connection to the DuckDB file provided in this repo.
     
```
   db/unit-1-3.db
```

> If you expand on the `unit-1-3.db`, you should see a few predefined schemas.  
> * The default schema is `main`.  
> * Any tables you create without specifying a schema will be in `main`.  
> * You can also create additional schemas to organize your tables.



2. **Creating a Schema:**

   We start by creating a new schema `lesson` to organise our tables.

```sql
CREATE SCHEMA lesson;
```

  * alternatively, we can also use the following to create a schema if it does not exist yet

```sql
CREATE SCHEMA IF NOT EXISTS lesson;
```


3. **Creating your first Table:**

  * We will be creating a table `users` in the `lesson` schema. The table will have the following columns:

- `id` - integer
- `name` - varchar
- `email` - varchar
  
```sql
CREATE TABLE lesson.users (  
  id INTEGER,  
  name VARCHAR,  
  email VARCHAR  
);
```

> If you just want to create tables in the default (`main`) schema, you can omit the `lesson.` prefix.


4. **Basic Data Entry (DML basics for testing DDL):**

  * We can insert data into the table using the `INSERT INTO` statement.
   
```sql
INSERT INTO lesson.users (id, name, email)  
VALUES (1, 'John Doe', 'john.doe@gmail.com');
```

  * This will insert a new row / record into the `users` table. You can insert multiple rows at once.

```sql
INSERT INTO lesson.users (id, name, email)
VALUES (2, 'Jane Doe', 'jane.doe@gmail.com'),
       (3, 'John Smith', 'john.smith@gmail.com');
```

> Insert two more rows with contiguously increasing `id` values, random `name`s and `email`s.

5. **Alter Tables**

  * We can alter the tables to add, rename or remove columns.

  * Add column 'start_date' to table users.

```sql
ALTER TABLE lesson.users ADD COLUMN start_date DATE;
```

Rename column 'id' to 'uid' in table classes.

```sql
ALTER TABLE lesson.users RENAME id TO uid;
```

6. **TRUNCATE (Emptying the table) vs. DROP (Deleting the table):**



```sql
ALTER TABLE lesson.users
DROP COLUMN email;
```

```sql
TRUNCATE TABLE lesson.users;
```

```sql
DROP TABLE lesson.users;
```
> **Tip: "Always run a SELECT before a DROP. Double-check your table name. It’s better to be slow and correct than fast and sorry."**

* **Q\&A:** Addressing connection issues and terminology (Database vs. Schema).  
* **Reflection:** Why is organizing data into schemas important in a production environment?

---
## **Section 2: Building Relationships & Constraints**

**Learning Objective:** By the end of this section, learners will be able to translate an Entity Relationship Diagram (ERD) into SQL tables using primary keys, foreign keys, and data constraints.

* **Theory Summary/Recap:**  
  * Constraints: Primary Keys (Uniqueness), Foreign Keys (Relationships), NOT NULL, CHECK, and DEFAULT.  
  * Understanding the School System ERD (Students, Teachers, Classes).

<details>
  <summary>Primary Keys, Foreign Keys, NOT NULL, CHECK, and DEFAULT</summary>
  
  * `primary key` or `unique` define a column, or set of columns, that are a unique identifier for a row in the table.
  * `primary key` constraints and unique constraints are identical except that a table can only have one primary key constraint defined, but many unique constraints and a primary key constraint also enforces the keys to not be NULL.
  * `foreign key` defines a column, or set of columns, that refer to a primary key or unique constraint from another table. The constraint enforces that the key exists in the other table.
  * `not null` specifies that the column cannot contain any NULL values. By default, all columns in tables are nullable.
  * `default` specifies a default value for the column when no value is specified.
  * `check` constraint allows you to specify an arbitrary boolean expression. Any columns that do not satisfy this expression violate the constraint.
</details>

* **Demo & Hands-on Workshop:**
 
1. **Creating Tables with Constraints:**  
```sql
CREATE TABLE lesson.teachers (
  id INTEGER PRIMARY KEY, -- primary key
  name VARCHAR NOT NULL, -- not null
  age INTEGER CHECK(age > 18 AND age < 70), -- check
  address VARCHAR,
  phone VARCHAR,
  email VARCHAR CHECK(CONTAINS(email, '@')) -- check
);

CREATE TABLE lesson.classes (
  id INTEGER PRIMARY KEY, -- primary key
  name VARCHAR NOT NULL, -- not null
  teacher_id INTEGER REFERENCES lesson.teachers(id) -- foreign key
);
```

2. **Exercise:** Complete the CREATE TABLE statement for the students table based on the ERD (Entity-Relationship Diagram) below.

> In a school system whose classes have students and teachers. Each student belongs to a single class. Each teacher may teach more than one class, but each class only has one teacher.

```dbml
Table students {
  id int [pk]
  name varchar
  address varchar
  phone varchar
  email varchar
  class_id int
}

Table teachers {
  id int [pk]
  name varchar
  age int
  address varchar
  phone varchar
  email varchar
}

Table classes {
  id int [pk]
  name varchar
  teacher_id int
}

Ref: students.class_id > classes.id // many-to-one

Ref: classes.teacher_id > teachers.id // many-to-one
```

* **Q\&A:** Troubleshooting foreign key errors and understanding "CHECK" logic.  
* **Reflection:** How do constraints prevent "bad data" from entering your analysis pipeline?


---
## **Section 3: Data Management & Performance**

**Learning Objective:** By the end of this section, learners will be able to import, update and export data, improve query performance with indexes, explain differences between tables and views. 

* **Theory Summary/Recap:**
  * The COPY command for CSV/JSON handling.
  * What are Indexes? (Think of a book index for speed).  
  * Tables vs. Views (Physical storage vs. Virtual queries).  
  

<details>
  <summary>What are Indexes?</summary>
  
  * Indexes are used to improve the performance of queries. They are not required but are recommended for tables with many rows. They are used to _retrieve data from the database more quickly than otherwise_. Indexes are created using one or more columns of a database table. The users cannot see the indexes, they are just used to speed up searches/queries.
</details>

<details>
  <summary>Tables vs. Views</summary>
  
  * Tables and views are both ways to store data. What is the difference between them? A table is a physical copy of the data (materialized), while a view is a virtual copy of the data. A view is a query that is run on the fly when you access the view. A view is not stored in the database, but the query that defines the view is stored in the database.
</details>



* **Demo & Hands-on Workshop:**

1. **Importing Data:**

  * We can import data from a CSV file into a table.

```sql
COPY lesson.teachers FROM '<full directory path>' (AUTO_DETECT TRUE);
```

> **Note:** For data import, use the full directory path to the CSV files, e.g. `/Users/fengfeng/Dev/6m-data-1.3-sql-basic-ddl/data/teachers.csv`

2. **Exercise:**

  * Import data for `classes` and `students` tables. 


3. **Updating Data:**

  * We can update the data in the table using the `UPDATE` statement.

  * Let's say `Linda Garcia` changed her email to `linda.g@example.com`, we can update the `email` of the student with id 4 (her id) to `linda.g@example.com`. The `WHERE` clause is used to specify which rows to update.

```sql
UPDATE lesson.students
SET email = 'linda.g@example.com'
WHERE id = 4;
```
  > This is DML, we will learn more in next lesson. 

4. **Exporting Data:**

  * Let's export the data from the student table into a CSV file delimited with `|`.       Remember to prepend the full directory path to the CSV file.

```sql
COPY (SELECT * FROM lesson.students) TO '<full directory path>' WITH (HEADER 1, DELIMITER '|');

-- example <full directory path>: /Users/fengfeng/Dev/6m-data-1.3-sql-basic-ddl/data/students_new.csv
```

  * We can also export the data into a JSON file (you will learn more about JSON in Module 2).

```sql
COPY (SELECT * FROM lesson.students) TO '<full directory path>';

-- example <full directory path>:  /Users/fengfeng/Dev/6m-data-1.3-sql-basic-ddl/data/students.json
```

5. **Exercise:**

  * Repeat the above steps for the `teachers` & `classes` tables.



6. **Creating Indexes:**

   <details>
   <summary>Indexes</summary>
  
   * Indexes are used to improve the performance of queries. They are not required but are recommended for tables with many rows. They are used to _retrieve data from the database more quickly than otherwise_. Indexes are created using one or more columns of a database table. The users cannot see the indexes, they are just used to speed up searches/queries.
   </details>


  

```sql
-- Create a unique index 'teachers_name_idx' on the column name of table teachers.

CREATE UNIQUE INDEX teachers_name_idx ON lesson.teachers(name);
```


```sql
-- Create index 'students_name_idx' that allows for duplicate values on the column name of table students.

CREATE INDEX students_name_idx ON lesson.students(name);
```

```sql
-- View indexes for a specific table
SELECT index_name, sql 
FROM duckdb_indexes 
WHERE table_name = 'students';
```

7. **Tables vs Views:**

   <details>
   <summary>Tables and Views</summary>
  
   * Tables and views are both ways to store data. What is the difference between them? A table is a physical copy of the data (materialized), while a view is a virtual copy of the data. A view is a query that is run on the fly when you access the view. A view is not stored in the database, but the query that defines the view is stored in the database.
   </details>

  * We will be creating a view `students_view` in the `lesson` schema. The view will have the following columns:

  - `id` - integer
  - `name` - varchar
  - `email` - varchar

```sql
CREATE VIEW lesson.students_view AS
SELECT id, name, email
FROM lesson.students;
```

8. **Exercise:**

  * Create a view `teachers_view` with the same columns as `students_view` but for the `teachers` table.
   


* **Q\&A:** When should you *not* use an index? Difference between dropping a table vs. deleting data.  
* **Reflection:** How does using a View simplify the work for a Data Analyst who only needs specific columns?




---

## **Self-Study & Advanced Parts (Optional)**
### **Local Environment Setup**

If you want to create the database file from scratch:

1. Create a new conda environment from `environment.yml`
```
  conda env create -f environment.yml
```
2. Activate the conda environment
```
  conda activate ddb
```   
3. Run [create_duckdb.py](./db/create_duckdb.py) to create the database file.
```
  python db/create_duckdb.py
```

