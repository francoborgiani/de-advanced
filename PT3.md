## Practice Test 3 - Results

**Attempt 1**

### Question 1

**Prompt:** What is the purpose of external functions in Snowflake?

**Answer Choices:**

* A. Download executable code maintained outside Snowflake.
* B. Connect to a repository of functions outside Snowflake.
* C. Call executable code developed, maintained, stored, and executed outside Snowflake.

**Correct Answer:** C

**Overall Explanation:**

The correct answer for the purpose of external functions in Snowflake is: `C. Call executable code developed, maintained, stored, and executed outside Snowflake`.

**Explanation:** External functions allow you to leverage code that resides outside of Snowflake's environment, expanding the capabilities of your SQL queries and procedures.

**Resources:**

* [External Functions Introduction](https://docs.snowflake.com/en/sql-reference/external-functions-introduction)

### Question 2

**Prompt:** When are materialized views NOT recommended?

**Answer Choices:**

* A. Query results contain results that require significant processing.
* B. The query is on an external table.
* C. The view's base table does not change frequently.
* D. The view's base table changes frequently.

**Correct Answer:** D

**Overall Explanation:**

Correct Answer: `D. The view's base table changes frequently`.

**Explanation:** Materialized views are not recommended when the underlying data changes frequently because the view needs to be refreshed to reflect the latest data, which can become inefficient.

**Resources:**

* [Materialized Views](https://docs.snowflake.com/en/user-guide/views-materialized)

### Question 3

**Prompt:** Micro-partitions can be modified once they have been created! True or false?

**Answer Choices:**

* A. False
* B. True

**Correct Answer:** A

**Overall Explanation:**

The statement is: `False`.

**Explanation:** Micro-partitions are automatically managed by Snowflake and cannot be directly modified by users.

**Resources:**

* [How does micro-partition and clusters works at time of delete statement, update and insert statement in Snowflake](https://community.snowflake.com/s/question/0D5Do00000yPTnvKAG/how-does-micro-partition-and-clusters-works-at-time-of-delete-statement-update-and-insert-statement-in-snowflake)
* [Tables Clustering Micropartitions](https://docs.snowflake.com/en/user-guide/tables-clustering-micropartitions)

### Question 4

**Prompt:** What is the function of a row access policy?

**Answer Choices:**

* A. Giving read access to a table to non-ownership roles.
* B. Restricting which rows are returned in a query.
* C. Restricting users from inserting rows into certain tables.
* D. Giving access to table data to non-snowflake users.

**Correct Answer:** B

**Overall Explanation:**

The correct answer for the function of a row access policy in Snowflake is: `B. Restricting which rows are returned in a query`.

**Resources:**

* [Row Access Policies](https://docs.snowflake.com/en/user-guide/security-row-intro)

### Question 5

**Prompt:** `Virtual warehouses` are billed on a per-second basis. What is the minimum number of seconds a virtual warehouse is billed for? Choose one correct value.

**Answer Choices:**

* A. 60
* B. 120
* C. 30
* D. 10
* E. 600

**Correct Answer:** A

**Overall Explanation:**

Correct Answer: `A. 60`

**Explanation:** Virtual warehouses in Snowflake are billed for a minimum of 60 seconds, even if the warehouse is suspended or no queries are running.

**Resources:**

* [How are credits charged for warehouses](https://docs.snowflake.com/en/user-guide/warehouses-considerations#how-are-credits-charged-for-warehouses)

### Question 6

**Prompt:** Which queries would not require the use of a Virtual Warehouse and instead would make use of the metadata cache? [Select two]

**Answer Choices:**

* A. `SELECT * FROM TABLE(FLATTEN(INPUT => PARSE_JSON('[1, ,77]'))) F;`
* B. `DESCRIBE TABLE EMPLOYEE;`
* C. `SELECT COUNT(*) FROM EMPLOYEE;`
* D. `SELECT EMP_ID, NAME, ADDRESS FROM EMPLOYEE;`

**Correct Answer:** B and C

**Overall Explanation:**

Correct Answer: `B and C`

**Explanation:**

* **A. `SELECT * FROM TABLE(FLATTEN(INPUT => PARSE_JSON('[1, ,77]'))) F;`**
  * **Incorrect:** This query uses the `FLATTEN` and `PARSE_JSON` functions, which require processing data and thus necessitate a virtual warehouse.
* **B. `DESCRIBE TABLE EMPLOYEE;`**
  * **Correct:** The `DESCRIBE` statement retrieves information about the table schema, which is stored in the metadata cache. No virtual warehouse is needed.
* **C. `SELECT COUNT(*) FROM EMPLOYEE;`**
  * **Correct:** Counting the number of rows in a table (using `COUNT(*)`) can often be retrieved from the metadata cache, especially for smaller tables. However, for very large tables, Snowflake might need to scan some data to get an accurate count, potentially using a virtual warehouse.
* **D. `SELECT EMP_ID, NAME, ADDRESS FROM EMPLOYEE;`**
  * **Incorrect:** Selecting specific columns from a table requires reading data from storage, which necessitates a virtual warehouse.

**Resources:**

* [Difference between metadata cache and result cache](https://community.snowflake.com/s/question/0D5Do00000IaCZlKAN/what-is-the-difference-between-metadata-cache-and-result-cache?__cf_chl_tk=OZBTAjj10vO6THmpy_kSUTZgNMaTOB._6X07EtyvUXA-1717931340-0.0.1.1-5844)

### Question 7

**Prompt:** Which queries are examples of selective point lookups? [Select two]

**Answer Choices:**

* A. `SELECT NAME, ADDRESS FROM EMPLOYEES WHERE EMP_ID IN ('7348738',9892492);`
* B. `SELECT * FROM EMPLOYEES;`
* C. `SELECT NAME, ADDRESS FROM EMPLOYEES WHERE EMP_EMAIL ='binni@udemy.com';`
* D. `SELECT NAME, ADDRESS, COUNT(FLAG) FROM EMPLOYEES GROUP BY NAME, ADDRESS;`

**Correct Answer:** A and C

**Overall Explanation:**

Correct Answer: `A and C`

**Explanation:**

* A. `SELECT NAME, ADDRESS FROM EMPLOYEES WHERE EMP_ID IN ('7348738',9892492);`
    * Correct: This query retrieves specific records based on their unique identifiers (`EMP_ID`), which aligns with the concept of selective point lookups.
* B. `SELECT * FROM EMPLOYEES;`
    * Incorrect: This query retrieves all columns and rows from the `EMPLOYEES` table, indicating a full table scan rather than a selective point lookup.
* C. `SELECT NAME, ADDRESS FROM EMPLOYEES WHERE EMP_EMAIL ='binni@udemy.com';`
    * Correct: Assuming `EMP_EMAIL` is unique or has a limited number of duplicates, this query effectively performs a selective lookup based on a specific email address.
* D. `SELECT NAME, ADDRESS, COUNT(FLAG) FROM EMPLOYEES GROUP BY NAME, ADDRESS;`
    * Incorrect: This query involves grouping and aggregation (`COUNT(FLAG)`), suggesting a broader data retrieval operation rather than selective point lookups.

**Resources:**

* [Search Optimization Service](https://docs.snowflake.com/en/user-guide/search-optimization-service)

### Question 8

**Prompt:** What is the process of eliminating unrequired micro-partitions called during a query?

**Answer Choices:**

* A. Limiting
* B. Narrowing
* C. Pruning
* D. Sharding

**Correct Answer:** C

**Overall Explanation:**

The correct answer is: `C. Pruning`

**Explanation:** Pruning is the process of eliminating micro-partitions that are not required to satisfy a query.

**Resources:**

* [Tables Clustering Micropartitions](https://docs.snowflake.com/en/user-guide/tables-clustering-micropartitions)

### Question 9

**Prompt:** What is meant by Tri-secret secure in Snowflake?

**Answer Choices:**

* A. The use of three passwords to log-in.
* B. A composite encryption key to encrypt data files made up of a user-provided key and a Snowflake key.
* C. Rotating a key 3 times in a month.
* D. The use of a hardware module to store a customer-managed key.

**Correct Answer:** B

**Overall Explanation:**

The correct answer is: `B. A composite encryption key to encrypt data files made up of a user-provided key and a Snowflake key`.

**Explanation:** Tri-secret secure refers to a composite encryption key comprising a user-provided key and a Snowflake key, enhancing data protection.

**Resources:**

* [Tri-Secret Secure](https://docs.snowflake.com/en/user-guide/security-encryption-tss)

### Question 10

**Prompt:** A Data Engineer is building a set of reporting tables to analyze consumer requests by region for each of the Data Exchange listings annually, as well as click-through rates for each listing. Which views are needed MINIMALLY as data sources?

**Answer Choices:**

* A. SNOWFLAKE.DATA_SHARING_USAGE.LISTING_CONSUMPTION_DAILY
* B. SNOWFLAKE.DATA_SHARING_USAGE.LISTING_CONSUMPTION_HOURLY
* C. SNOWFLAKE.DATA_SHARING_USAGE.LISTINGS
* D. SNOWFLAKE.DATA_SHARING_USAGE.SHARE_HISTORY
* E. SNOWFLAKE.ACCOUNT_USAGE.DATABASE_STORAGE_USAGE_HISTORY

**Correct Answer:** A and C

**Overall Explanation:**

Correct Answer: `A and C`

**Explanation:**

To analyze consumer requests by region for each Data Exchange listing annually, as well as click-through rates, the following views are minimally needed:

* `SNOWFLAKE.DATA_SHARING_USAGE.LISTING_CONSUMPTION_DAILY`: This view provides information about consumer consumption of listings on a daily basis, including details like region and consumer account. This data can be aggregated to analyze annual trends.
* `SNOWFLAKE.DATA_SHARING_USAGE.LISTINGS`: This view provides information about the listings themselves, such as the listing name, creation date, and provider account. This information is necessary to identify and analyze individual listings.

**Resources:**

* [Data Sharing Usage](https://docs.snowflake.com/en/sql-reference/account-usage/data-sharing-usage)

### Question 11

**Prompt:** A Data Engineer wants to create a secure view that allows analysts to access specific columns from a table without granting them access to the underlying table. What is the correct object to create?

**Answer Choices:**

* A. Secure View
* B. Materialized View
* C. External Table
* D. Secure Materialized View

**Correct Answer:** A

**Overall Explanation:**

The correct answer is: `A. Secure View`

**Explanation:** A secure view in Snowflake allows you to control access to specific columns and rows of a base table without granting users direct access to the table itself.

**Resources:**

* [Secure Views](https://docs.snowflake.com/en/sql-reference/sql/create-secure-view)

### Question 12

**Prompt:** What is the correct syntax to unload data from a Snowflake table named MY_TABLE in the schema MY_SCHEMA in the database MY_DATABASE to an internal stage named MY_STAGE?

**Answer Choices:**

* A. `COPY INTO @MY_STAGE FROM MY_DATABASE.MY_SCHEMA.MY_TABLE;`
* B. `COPY INTO @MY_DATABASE.MY_SCHEMA.MY_TABLE FROM MY_STAGE;`
* C. `COPY INTO MY_STAGE FROM MY_DATABASE.MY_SCHEMA.MY_TABLE;`
* D. `COPY INTO MY_DATABASE.MY_SCHEMA.MY_TABLE FROM @MY_STAGE;`

**Correct Answer:** A

**Overall Explanation:**

The correct syntax to unload data from a Snowflake table to an internal stage is: `COPY INTO @MY_STAGE FROM MY_DATABASE.MY_SCHEMA.MY_TABLE;`

**Explanation:**

The `COPY INTO <stage>` command is used to unload data from a Snowflake table to a stage. The `@` symbol denotes an internal stage.

**Resources:**

* [COPY INTO <location>](https://docs.snowflake.com/en/sql-reference/sql/copy-into-location)

### Question 13

**Prompt:** What are the valid data types for the return value of a Snowflake user-defined function (UDF)? [Select all that apply]

**Answer Choices:**

* A. TABLE
* B. VARIANT
* C. CURSOR
* D. OBJECT

**Correct Answer:** B and D

**Overall Explanation:**

Correct Answer: `B and D`

**Explanation:**

* **B. VARIANT:** This data type can hold any data type, making it suitable for flexible return values from UDFs.
* **D. OBJECT:** This data type represents a complex structure containing key-value pairs, allowing UDFs to return structured data.

**Resources:**

* [Supported Data Types for User Defined Functions](https://docs.snowflake.com/en/developer-guide/udf/python/udf-python-designing#supported-data-types-for-user-defined-functions)

### Question 14

**Prompt:** A Data Engineer needs to grant ownership of a newly created table to another role. Which command should they use?

**Answer Choices:**

* A. `GRANT OWNERSHIP ON TABLE <table_name> TO ROLE <role_name>;`
* B. `GRANT OWNERSHIP ON <table_name> TO ROLE <role_name>;`
* C. `GRANT ROLE <role_name> TO TABLE <table_name>;`
* D. `GRANT OWNERSHIP <table_name> TO ROLE <role_name>;`

**Correct Answer:** A

**Overall Explanation:**

The correct command to grant ownership of a table to another role is: `GRANT OWNERSHIP ON TABLE <table_name> TO ROLE <role_name>;`

**Resources:**

* [Granting Ownership of a Securable Object](https://docs.snowflake.com/en/sql-reference/sql/grant-ownership)

### Question 15

**Prompt:** After creating the table `MY_TABLE`, a data engineer executes the following commands:

`sql
CREATE STREAM MYSTREAM ON TABLE MYTABLE;
INSERT INTO MYTABLE VALUES (20);
Use code with caution.

What will be the output of executing the following command?

SQL
SELECT SYSTEM$STREAM_HAS_DATA('MYSTREAM');
Use code with caution.`

**Answer Choices:**

* A. It will return "Null".
* B. It will return "False".
* C. It will return "True".
* D. It will return "15".

**Correct Answer:** C

**Overall Explanation:**

**Correct Answer:**  C. It will return "True"

**Explanation:**

The SYSTEM$STREAM_HAS_DATA('MYSTREAM') command checks if there is any unread data in the MYSTREAM stream. Since the INSERT INTO MYTABLE command added a row to the MYTABLE table after the stream MYSTREAM was created on the table MYTABLE, the stream will contain data that has not yet been consumed. Therefore, the SYSTEM$STREAM_HAS_DATA('MYSTREAM') will return TRUE.

**Resources:**

* [SYSTEM$STREAM_HAS_DATA](https://www.google.com/url?sa=E&source=gmail&q=https://docs.snowflake.com/en/sql-reference/functions/system_stream_has_data)


### Question 16

**Prompt:** Which command can we use to convert **JSON** `NULL` values to **SQL** `NULL` values?

**Answer Choices:**

* A. JSON\_TO\_SQL
* B. TRANSCRIPT\_NULL
* C. STRIP\_NULL\_VALUE
* D. STRIP\_OUTER\_ARRAY

**Correct Answer:** C

**Overall Explanation:**

Correct Answer: `C. STRIP_NULL_VALUE`

**Explanation:**

The `STRIP_NULL_VALUE` function can be used to convert JSON `NULL` values to SQL `NULL` values. This can be useful when you want to ensure that your data is consistent and that you are not accidentally introducing null values into your database.

**Example:**

`sql
SELECT
    STRIP_NULL_VALUE(PARSE_JSON('{"a": null}'))
;
Query the data, using TRY_PARSE_JSON. Note that the value for the third line is NULL. If the query had used PARSE_JSON rather than TRY_PARSE_JSON, the query would have failed.   

+----+-------------------+
| ID | TRY_PARSE_JSON(V) |
|----+-------------------|
|  1 | [                 |
|    | -1,               |
|    | 12,               |
|    | 289,              |
|    | 2188,             |
|    | false,            |
|    | undefined         |
|    | ]                 |
|  2 | {                 |
|    | "x": "abc",       |
|    | "y": false,       |
|    | "z": 10           |
|    | }                 |
|  3 | NULL              |
+----+-------------------+

`

**Resources:**

* [STRIP_NULL_VALUE](https://www.google.com/url?sa=E&source=gmail&q=https://docs.snowflake.com/en/sql-reference/functions/strip_null_value)



### Question 17

**Prompt:** Which of these is NOT a valid `Snowflake Object Type`?

**Answer Choices:**

* A. VIEW
* B. TASK
* C. FUNCTION
* D. PROCEDURE
* E. INBOUND SHARE

**Correct Answer:** E

**Overall Explanation:**

Correct Answer: `E. INBOUND SHARE`

**Explanation:**

While `INBOUND SHARE` is a concept within Snowflake related to data sharing, it's not classified as a primary Snowflake object type like views, tasks, functions, and procedures.

Here's a breakdown of the valid object types:

* **VIEW:** A virtual table based on the result-set of an SQL statement.
* **TASK:**  A scheduled object that executes SQL statements or stored procedures on a recurring basis.
* **FUNCTION:** A named, reusable set of SQL statements that return a single value or a result set.
* **PROCEDURE:** A named, reusable set of SQL statements that perform a specific action.

**Resources:**

* [Object Types](https://docs.snowflake.com/en/user-guide/object-types)

### Question 18

**Prompt:** What is the correct syntax to create a `Java UDF` named `my_java_udf` that takes a single `VARCHAR` argument and returns an `INTEGER` value?

**Answer Choices:**

* A. 
`sql
CREATE FUNCTION my_java_udf(VARCHAR)
RETURNS INTEGER
AS
$$
// Java code here
$$
;
Use code with caution.

B.
SQL
CREATE OR REPLACE FUNCTION my_java_udf(str VARCHAR)
RETURNS INTEGER
LANGUAGE JAVA
AS
$$
// Java code here
$$
;
Use code with caution.

C.
SQL
CREATE FUNCTION my_java_udf(str VARCHAR)
RETURNS INTEGER
LANGUAGE JAVA
AS
$$
// Java code here
$$
;
Use code with caution.

D.
SQL
CREATE FUNCTION my_java_udf(VARCHAR)
RETURNS INTEGER
LANGUAGE JAVA
HANDLER='MyClass.my_method'
AS
$$
// Java code here
$$
;
`


**Correct Answer:** `C or D`

**Overall Explanation:**

Both options C and D are correct ways to create a Java UDF in Snowflake.

**Explanation:**

Option C: This is the most basic syntax for creating a Java UDF. It specifies the function name (my_java_udf), input parameter type (VARCHAR), return type (INTEGER), and the LANGUAGE JAVA clause. The Java code is placed within the $$ delimiters.

Option D: This syntax is similar to option C, but it also includes the HANDLER clause. The HANDLER clause specifies the Java class and method that will be called when the UDF is executed. This is useful if you want to organize your Java code into multiple classes and methods.

Why other options are incorrect:

Option A: This syntax is missing the LANGUAGE JAVA clause, which is required for Java UDFs.
Option B: While CREATE OR REPLACE is often used, it's not strictly necessary for creating a new UDF. CREATE FUNCTION is sufficient.
Resources:

**Resources:**

* [Java UDFs](https://docs.snowflake.com/en/sql-reference/udf-java)

### Question 19

**Prompt:** Which of the following are the correct ways to create a stage? (Select 3)

**Answer Choices:**

* A. `CREATE STAGE my_stage;`
* B. `CREATE OR REPLACE STAGE my_stage;`
* C. `CREATE TEMP STAGE my_stage;`
* D. `CREATE STAGE IF NOT EXISTS my_stage;`
* E. `CREATE OR REPLACE TEMP STAGE my_stage;`

**Correct Answer:** A, B and D

**Overall Explanation:**

The correct answers are A, B, and D. These options represent valid syntax variations for creating a stage in Snowflake.

**Explanation:**

* **A. `CREATE STAGE my_stage;`** - This is the most basic form for creating a stage.
* **B. `CREATE OR REPLACE STAGE my_stage;`** - This option creates a new stage or replaces an existing one with the same name.
* **D. `CREATE STAGE IF NOT EXISTS my_stage;`** - This creates a stage only if a stage with the same name doesn't already exist.

**Why other options are incorrect:**

* **C. `CREATE TEMP STAGE my_stage;`** -  While you can create temporary tables, the concept of a "temporary stage" doesn't exist in Snowflake. Stages are persistent storage locations.
* **E. `CREATE OR REPLACE TEMP STAGE my_stage;`** - Similar to option C, this combines `CREATE OR REPLACE` with `TEMP STAGE`, which is not valid.

**Resources:**

* [CREATE STAGE](https://docs.snowflake.com/en/sql-reference/sql/create-stage)

### Question 20

**Prompt:** Which of the following Snowflake editions supports using a customer-managed key (CMK) with Tri-Secret Secure?

**Answer Choices:**

* A. Enterprise Edition and above
* B. Business Critical Edition and above
* C. All Editions

**Correct Answer:** B

**Overall Explanation:**

The correct answer is: `B. Business Critical Edition and above`.

**Explanation:**  The Business Critical Edition (and higher editions like Virtual Private Snowflake) in Snowflake supports the use of customer-managed keys (CMKs) with Tri-Secret Secure. This allows for greater control and security over your data encryption keys.

**Resources:**

* [Tri-Secret Secure](https://docs.snowflake.com/en/user-guide/security-encryption-tss)


### Question 21

**Prompt:** A Data Engineer wants to create a function that accepts an array of integers and returns the sum of all the even numbers in the array. Which type of UDF should be used?

**Answer Choices:**

* A. SQL UDF
* B. Java UDF
* C. Python UDF

**Correct Answer:** A, B, or C

**Overall Explanation:**

Correct Answer: `A, B, or C`

**Explanation:**

All three types of UDFs (SQL, Java, and Python) are capable of performing the task of summing even numbers from an array. The choice depends on the developer's preference and expertise.

**Resources:**

* [User-Defined Functions (UDFs)](https://docs.snowflake.com/en/sql-reference/user-defined-functions)


### Question 22

**Prompt:** What is the correct syntax to refresh a materialized view named MY_MVIEW?

**Answer Choices:**

* A. `REFRESH MATERIALIZED VIEW MY_MVIEW;`
* B. `ALTER MATERIALIZED VIEW MY_MVIEW REFRESH;`
* C. `REFRESH VIEW MY_MVIEW;`
* D. `ALTER VIEW MY_MVIEW REFRESH;`

**Correct Answer:** A

**Overall Explanation:**

The correct syntax to refresh a materialized view is: `A. REFRESH MATERIALIZED VIEW MY_MVIEW;`

**Resources:**

* [Refreshing Materialized Views](https://docs.snowflake.com/en/sql-reference/sql/refresh-materialized-view)


### Question 23

**Prompt:** Which command should a Data Engineer use to decrease the size of a virtual warehouse named MY_WAREHOUSE from LARGE to SMALL?

**Answer Choices:**

* A. `ALTER WAREHOUSE MY_WAREHOUSE SET SIZE = 'SMALL';`
* B. `ALTER WAREHOUSE MY_WAREHOUSE RESIZE = 'SMALL';`
* C. `ALTER WAREHOUSE SET MY_WAREHOUSE SIZE = 'SMALL';`
* D. `ALTER MY_WAREHOUSE SET SIZE = 'SMALL';`

**Correct Answer:** A

**Overall Explanation:**

Correct Answer: `A. ALTER WAREHOUSE MY_WAREHOUSE SET SIZE = 'SMALL';`

**Explanation:** This command correctly uses the `ALTER WAREHOUSE` statement to modify the `MY_WAREHOUSE` virtual warehouse and sets its size to `'SMALL'`.

**Resources:**

* [ALTER WAREHOUSE](https://docs.snowflake.com/en/sql-reference/sql/alter-warehouse)


### Question 24

**Prompt:** What is the correct syntax to grant the role `LOADER` usage privileges on the database `MY_DATABASE`?

**Answer Choices:**

* A. `GRANT USAGE ON DATABASE MY_DATABASE TO ROLE LOADER;`
* B. `GRANT ROLE LOADER TO DATABASE MY_DATABASE;`
* C. `GRANT USAGE ON LOADER TO ROLE MY_DATABASE;`
* D. `GRANT USAGE TO ROLE LOADER ON DATABASE MY_DATABASE;`

**Correct Answer:** A

**Overall Explanation:**

The correct syntax to grant usage privileges on a database to a role is: `A. GRANT USAGE ON DATABASE MY_DATABASE TO ROLE LOADER;`

**Resources:**

* [Granting Privileges on a Database](https://docs.snowflake.com/en/sql-reference/sql/grant-on-database)

### Question 25

**Prompt:** A company has a table with corrupted data, named `Customer_Data`. The company wants to recover the data as it was 5 minutes ago using cloning and Time Travel into a table named `Recovered_customer_data`.

What command will accomplish this?

**Answer Choices:**

`
* A. 
sql
CREATE TABLE Recovered_customer_data
Customer_Data CLONE Data AT(TIME => -60*5);
Use code with caution.

* B.
SQL
CREATE TABLE Recovered_customer_data
CLONE Customer_Data AT(OFFSET => -60*5);
Use code with caution.

* C.
SQL
CREATE CLONE TABLE Recovered_customer_data
FROM Customer_Data AT(OFFSET => -60*5);
Use code with caution.

* D.
SQL
CREATE CLONE Recovered_customer_data
FROM Customer_Data AT(OFFSET => -60*5);
Use code with caution.`

**Correct Answer:** B

**Overall Explanation:**

Correct Answer: `B. CREATE TABLE Recovered_customer_data CLONE Customer_Data AT(OFFSET => -60*5);`

**Explanation:**
`
A. CREATE TABLE Recovered_customer_data Customer_Data CLONE Data AT(TIME => -60*5):
Data is likely a typo or a placeholder. The correct syntax involves specifying the existing table to clone (Customer_Data).
C. CREATE CLONE TABLE Recovered_customer_data FROM Customer_Data AT(OFFSET => -60*5):
While CREATE CLONE TABLE might be encountered in some contexts, Snowflake's recommended approach is CREATE TABLE ... CLONE ... for clarity.
Additionally, FROM is not typically used with CLONE.
D. CREATE CLONE Recovered_customer_data FROM Customer_Data AT(OFFSET => -60*5):
Similar to option C, CREATE CLONE without TABLE is less common. Also, FROM is not necessary here.`

**Resources:**


* [CREATE CLONE](https://docs.snowflake.com/en/sql-reference/sql/create-clone)

### Question 26

**Prompt:** What is true about Internal Stages? (Select 2)

**Answer Choices:**

  * A. A table stage can access all tables in a database.
  * B. The data will be automatically compressed.
  * C. Unused data will be purged after 61 days.
  * D. The data will be automatically encrypted.

**Correct Answer:** B and D

**Overall Explanation:**

The correct answers are: `B and D`

**Explanation:**

  * **B. The data will be automatically compressed:** This is true. Snowflake automatically compresses all data that is loaded into internal stages.
  * **D. The data will be automatically encrypted:** This is true. Snowflake automatically encrypts all data that is loaded into internal stages, using strong encryption methods.

**Resources:**

  * [Loading data into Snowflake](https://www.google.com/url?sa=E&source=gmail&q=https://docs.snowflake.com/en/user-guide/intro-summary-loading)

### Question 27

**Prompt:** Which type of objects can be shared?

**Answer Choices:**

  * A. Standard views
  * B. Secure UDFs
  * C. External Tables
  * D. Tasks
  * E. Secure views

**Correct Answer:** B, C and E

**Overall Explanation:**

Correct Answer: `B, C and E`

**Explanation:**

Secure UDFs, External Tables, and Secure Views can be shared.

**Resources:**

  * [Data Sharing Introduction](https://www.google.com/url?sa=E&source=gmail&q=https://docs.snowflake.com/en/user-guide/data-sharing-intro)

### Question 28

**Prompt:** What is true about Snowflake Scripting blocks?

**Answer Choices:**

  * A. Variables created in a block can be used outside the block.
  * B. DECLARE is always a section of a block.
  * C. Doesn't support EXCEPTION handling.
  * D. Objects created in a block can be used outside the block.

**Correct Answer:** D

**Overall Explanation:**

Correct Answer: `D. Objects created in a block can be used outside the block.`

**Explanation:**

Objects created in a block can be used outside the block.

Here's why the other options are incorrect:

  * B. `DECLARE` is always a section of a block. This is incorrect. The `DECLARE` section is optional within a block and allows you to define variables for use within the block.
  * C. Doesn't support `EXCEPTION` handling. This is incorrect.
  * A. Variables created in a block can be used outside the block. Variables declared within a block are local to that block and cannot be accessed outside of it.

**Resources:**

  * [Blocks](https://www.google.com/url?sa=E&source=gmail&q=https://docs.snowflake.com/en/developer-guide/snowflake-scripting/blocks)

### Question 29

**Prompt:** Which statements on `ACCOUNT_USAGE` schema and `INFORMATION_SCHEMA` are `True`? (Select 2)

**Answer Choices:**

  * A. The INFORMATION\_SCHEMA has no information about dropped objects.
  * B. Querying table functions in the INFORMATION\_SCHEMA can give different results depending on the privileges of the role that executes the query.
  * C. The ACCOUNT\_USAGE schema has no latency.
  * D. The INFORMATION\_SCHEMA only contains database-level information.
  * E. The ACCOUNT\_USAGE schema retains data for 7 days.

**Correct Answer:** A and B

**Overall Explanation:**

Correct Answer: `A and B`

**Explanation:**

  * A. The INFORMATION\_SCHEMA has no information about dropped objects.
  * B. Querying table functions in the INFORMATION\_SCHEMA can give different results depending on the privileges of the role that executes the query.

Incorrect options:

  * C. The ACCOUNT\_USAGE\_SCHEMA has no latency. This is incorrect. The ACCOUNT\_USAGE schema can have a latency of up to 3 hours. This means that the data you see might be up to 3 hours old.
  * D. The INFORMATION\_SCHEMA only contains database-level information. This is incorrect. The views in INFORMATION\_SCHEMA display metadata about objects defined in the database, as well as metadata for non-database, account-level objects that are common across all databases.
  * E. The ACCOUNT\_USAGE schema retains data for 7 days. This is incorrect. The ACCOUNT\_USAGE schema retains data for 365 days (1 year), not 7 days.

**Resources:**

  * [Information Schema](https://www.google.com/url?sa=E&source=gmail&q=https://docs.snowflake.com/en/sql-reference/info-schema)
  * [Account Usage](https://www.google.com/url?sa=E&source=gmail&q=https://docs.snowflake.com/en/sql-reference/account-usage)

### Question 30

**Prompt:** Which of the following are true about Snowflake's Fail-safe feature? (Select 2)

**Answer Choices:**

* A. It is a free service offered to all Snowflake users.
* B. It provides an additional layer of data protection beyond Time Travel.
* C. It allows for the recovery of data even after the Time Travel retention period has expired.
* D. It is a paid feature that requires manual configuration.

**Correct Answer:** B and C

**Overall Explanation:**

Correct Answer: `B and C`

**Explanation:**

* **B. It provides an additional layer of data protection beyond Time Travel.** Fail-safe is designed to recover data that may be lost even after the Time Travel retention period expires, offering an extra layer of protection.
* **C. It allows for the recovery of data even after the Time Travel retention period has expired.** This is the primary purpose of Fail-safe.

**Resources:**

* [Fail-safe](https://docs.snowflake.com/en/user-guide/fail-safe)


### Question 31

**Prompt:** A Data Engineer wants to create a pipe that automatically loads data from an Azure Blob Storage container to a Snowflake table whenever new data files are added to the container. What type of pipe should they create?

**Answer Choices:**

* A. Continuous pipe
* B. External pipe
* C. Auto-ingest pipe
* D. Cloud storage pipe

**Correct Answer:** A

**Overall Explanation:**

Correct Answer: `A. Continuous pipe`

**Explanation:** Continuous pipes in Snowflake are designed to automatically monitor cloud storage locations (like Azure Blob Storage) and ingest new data files as they arrive.

**Resources:**

* [Continuous Data Ingestion using Snowpipe](https://docs.snowflake.com/en/user-guide/data-load-snowpipe-intro)


### Question 32

**Prompt:** What is the correct syntax to create a clone of a table named `ORDERS` at the current point in time with a new name `ORDERS_CLONE`?

**Answer Choices:**

* A. `CREATE TABLE ORDERS_CLONE CLONE ORDERS;`
* B. `CREATE TABLE ORDERS_CLONE LIKE ORDERS;`
* C. `CREATE TABLE ORDERS_CLONE AS SELECT * FROM ORDERS;`
* D. `CREATE OR REPLACE TABLE ORDERS_CLONE COPY ORDERS;`

**Correct Answer:** A

**Overall Explanation:**

Correct Answer: `A. CREATE TABLE ORDERS_CLONE CLONE ORDERS;`

**Explanation:** This command correctly uses the `CLONE` keyword to create a new table (`ORDERS_CLONE`) that is an exact copy of the `ORDERS` table at the current point in time.

**Resources:**

* [Creating a Clone of a Table](https://docs.snowflake.com/en/sql-reference/sql/create-table-cloning)


### Question 33

**Prompt:** Which of the following statements about Snowflake tasks are true? (Select 2)

**Answer Choices:**

* A. Tasks can be scheduled to run on a recurring basis, such as daily or hourly.
* B. Tasks can only be created by users with the `ACCOUNTADMIN` role.
* C. Tasks can be used to automate various actions, such as data loading, transformations, and query execution.
* D. Tasks can only execute SQL statements and cannot call stored procedures.

**Correct Answer:** A and C

**Overall Explanation:**

Correct Answer: `A and C`

**Explanation:**

* **A. Tasks can be scheduled to run on a recurring basis, such as daily or hourly.** This is a key feature of tasks, allowing for automation of recurring processes.
* **C. Tasks can be used to automate various actions, such as data loading, transformations, and query execution.** Tasks are versatile and can execute a variety of actions, including stored procedure calls.

**Resources:**

* [Tasks](https://docs.snowflake.com/en/sql-reference/sql/create-task)


### Question 34

**Prompt:** A Data Engineer wants to create a user-defined function (UDF) that performs complex calculations involving multiple steps and conditional logic. Which type of UDF is best suited for this scenario?

**Answer Choices:**

* A. SQL UDF
* B. JavaScript UDF
* C. Java UDF

**Correct Answer:** B or C

**Overall Explanation:**

Correct Answer: `B or C`

**Explanation:**

While SQL UDFs are suitable for simpler functions, JavaScript and Java UDFs offer greater flexibility and control flow for complex calculations and logic.

**Resources:**

* [Java UDFs](https://docs.snowflake.com/en/sql-reference/udf-java)
* [JavaScript UDFs](https://docs.snowflake.com/en/sql-reference/udf-javascript)


### Question 35

**Prompt:** Which of the following are valid ways to unload data from a Snowflake table to a stage? (Select 2)

**Answer Choices:**

* A. `COPY INTO <stage>`
* B. `UNLOAD INTO <stage>`
* C. `EXPORT TO <stage>`
* D. `PUT INTO <stage>`

**Correct Answer:** A

**Overall Explanation:**

Correct Answer: `A. COPY INTO <stage>`

**Explanation:** The `COPY INTO <stage>` command is used to unload data from a Snowflake table to a stage.

**Resources:**

* [COPY INTO <location>](https://docs.snowflake.com/en/sql-reference/sql/copy-into-location)
