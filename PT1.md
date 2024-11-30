# Practice Test 1 - Results

## Question 1

**A Data Engineer is building a set of reporting tables to analyze consumer requests by region for each of the Data Exchange offerings annually, as well as click-through rates for each listing. Which views are needed MINIMALLY as data sources?**

**Answers:**

* A. SNOWFLAKE.DATA_SHARING_USAGE.LISTING_EVENTS_DAILY
* B. SNOWFLAKE.DATA_SHARING_USAGE.LISTING_CONSUMPTION_DAILY
* C. SNOWFLAKE.DATA_SHARING_USAGE.LISTING_TELEMETRY_DAILY
* D. SNOWFLAKE.ACCOUNT_USAGE.DATA_TRANSFER_HISTORY

**Correct Answer:** B and C

**Overall Explanation:**

Answer: `B and C`

Explanation

**Resources:**

* https://docs.snowflake.com/en/sql-reference/data-sharing-usage

## Question 2

**Assuming that the session parameter `USE_CACHED_RESULT` is set to false, what are characteristics of Snowflake virtual warehouses in terms of the use of Snowpark?**

**Answers:**

* A. Creating a DataFrame from a table will start a virtual warehouse.
* B. Creating a DataFrame from a staged file with the read() method will start a virtual warehouse.
* C. Transforming a DataFrame with methods like replace() will start a virtual warehouse.
* D. Calling a Snowpark stored procedure to query the database with session.call() will start a virtual warehouse.

**Correct Answer:** D

**Overall Explanation:**

Correct Option: `D. Calling a Snowpark stored procedure to query the database with session.call() will start a virtual warehouse`.

**Resources:**

* https://docs.snowflake.com/en/sql-reference/parameters

## Question 3

**A Data Engineer needs to know the details regarding the micro-partition layout for a table named `Orders` using a built-in function. Which query will provide this information?**

**Answers:**

* A. `SELECT SYSTEM$CLUSTERING_INFORMATION('Orders')`
* B. `SELECT $CLUSTERING_INFORMATION('Orders')`
* C. `CALL SYSTEM$CLUSTERING_INFORMATION('Orders')`
* D. `CALL $CLUSTERING_INFORMATION('Orders')`

**Correct Answer:** A

**Overall Explanation:**

Correct Option: `A. SELECT SYSTEM$CLUSTERING_INFORMATION('Orders')`

**Resources:**

* https://docs.snowflake.com/en/sql-reference/functions/system_clustering_information

## Question 4

**Which callback function is required within a JavaScript User-Defined Function (UDF) for it to execute successfully?**

**Answers:**

* A. initialize()
* B. processRow()
* C. handler()
* D. finalize()

**Correct Answer:** B

**Overall Explanation:**

Correct Option: `B. processRow()`

Explanation:

In Snowflake's Tabular JavaScript UDFs (UDTFs), the `processRow()` callback function is essential for processing individual rows of data passed to the UDF.

It's invoked for each row within the input relation.

**Resources:**

* https://docs.snowflake.com/en/developer-guide/udf/javascript/udf-javascript-tabular-functions

## Question 5

**A Data Engineer is building a pipeline to transform a 1 TB table by joining it with supplemental tables. The Engineer is applying filters and several aggregations leveraging Common Table Expressions (CTEs) using a size Medium virtual warehouse in a single query in Snowflake. After checking the Query Profile, what is the recommended approach to Maximize performance of this query if the Profile shows data spillage?**

**Answers:**

* A. Enable clustering on the table.
* B. Increase the warehouse size.
* C. Rewrite the query to remove the CTEs.
* D. Switch to a multi-cluster virtual warehouse.

**Correct Answer:** B

**Overall Explanation:**

Correct Answer: `B. Increase the warehouse size.`

Explanation:

* Data spillage occurs when the Snowflake virtual warehouse's in-memory resources are insufficient to hold all the intermediate data during the query execution. Increasing the warehouse size (e.g., from Medium to Large or XLarge) provides more memory, potentially eliminating or reducing spillage and leading to faster query execution.

**Resources:**

* https://select.dev/posts/snowflake-query-profile

## Question 6

**A company built a sales reporting system with Python, connecting to Snowflake using the Python Connector. Based on the user's selections, the system generates the SQL queries needed to fetch the data for the report. First it gets the customers that meet the given query parameters (on average 1000 customer records for each report run), and then it loops the customer records sequentially. Inside that loop it runs the generated SQL clause for the current customer to get the detailed data for that customer number from the sales data table. When the Data Engineer tested the individual SQL clauses, they were fast enough (1 second to get the customers, 0.5 second to get the sales data for one customer), but the total runtime of the report is too long. How can this situation be improved?**

**Answers:**

* A. Increase the size of the virtual warehouse.
* B. Increase the number of maximum clusters of the virtual warehouse.
* C. Define a clustering key for the sales data table.
* D. Rewrite the report to eliminate the use of the loop construct.

**Correct Answer:** D

**Overall Explanation:**

Correct Answer: `D. Rewrite the report to eliminate the use of the loop construct`.

Explanation:

**Resources:**

* https://docs.snowflake.com/en/developer-guide/python-connector/python-connector-distributed-fetch

## Question 7

**While running an external function, the following error message is received: `Error: Function received the wrong number of rows` What is causing this to occur?**

**Answers:**

* A. External functions do not support multiple rows.
* B. Nested arrays are not supported in the JSON response.
* C. The JSON returned by the remote service is not constructed correctly.
* D. The return message did not produce the same number of rows that it received.

**Correct Answer:** D

**Overall Explanation:**

Answer: `D. The return message did not produce the same number of rows that it received.`

Explanation:

**Resources:**

* https://docs.snowflake.com/en/sql-reference/external-functions-creating-aws-troubleshooting

## Question 8

**A CSV file, around 1 TB in size, is generated daily on an on-premise server. A corresponding table, internal stage, and file format have already been created in Snowflake to facilitate the data loading process. How can the process of bringing the CSV file into Snowflake be automated using the LEAST amount of operational overhead?**

**Answers:**

* A. Create a task in Snowflake that executes once a day and runs a COPY INTO statement that references the internal stage. The internal stage will read the files directly from the on-premise server and copy the newest file into the table from the on-premise server to the Snowflake table.
* B. On the on-premise server, schedule a SQL file to run using SnowSQL that executes a PUT to push a specific file to the internal stage. Create a task that executes once a day in Snowflake and runs a COPY INTO statement that references the internal stage. Schedule the task to start after the file lands in the internal stage.
* C. On the on-premise server, schedule a SQL file to run using SnowSQL that executes a PUT to push a specific file to the internal stage. Create a pipe that runs a COPY INTO statement that references the internal stage. Snowpipe auto-ingest will automatically load the file from the internal stage when the new file lands in the internal stage.
* D. On the on-premise server, schedule a Python file that uses the Snowpark Python library. The Python script will read the CSV data into a DataFrame and generate an INSERT INTO statement that will directly load into the table. The script will bypass the need to move a file into an internal stage.

**Correct Answer:** B

**Overall Explanation:**

The most efficient approach with minimal operational overhead is `B`.

**Resources:**

* https://docs.snowflake.com/en/user-guide/snowsql
* https://docs.snowflake.com/en/user-guide/data-load-snowpipe-intro

## Question 9

**A Data Engineer is writing a Python script using the Snowflake Connector for Python. The Engineer will use the snowflake.connector.connect function to connect to Snowflake.**

**The requirements are:**

* Raise an exception if the specified database, schema, or warehouse does not exist
* Improve download performance

**Which parameters of the connect function should be used? (Choose two)**

**Answers:**

* A. authenticator
* B. arrow_number_to_decimal
* C. client_prefetch_threads
* D. client_session_keep_alive
* E. validate_default_parameters

**Correct Answer:** C and E

**Overall Explanation:**

**Answer:** `C. client_prefetch_threads, E. validate_default_parameters`

**Explanation:**

* `validate_default_parameters`: When set to True, this parameter will force validation of the parameters provided in the `connect()` function, including the database, schema, and warehouse. If any of these do not exist, it will raise an exception, satisfying the first requirement.
* `client_prefetch_threads`: This parameter controls the number of threads used for prefetching data in the background. Increasing the number of threads can improve the performance of large downloads, addressing the second requirement.

**Resources:**

* https://docs.snowflake.com/developer-guide/python-connector/python-connector-api#label-python-connector-api-connect

## Question 10

**At what isolation level are Snowflake streams?**

**Answers:**

* A. Snapshot
* B. Repeatable read
* C. Read committed
* D. Read uncommitted

**Correct Answer:** B

**Overall Explanation:**

The correct answer for the isolation level of Snowflake streams is: `B. Repeatable read`

## Question 11

**Which use case would be best suited for the search optimization service?**

**Answers:**

* A. Analysts who need to perform aggregates over high-cardinality columns.
* B. Business users who need fast response times using highly selective filters.
* C. Data Scientists who seek specific JOIN statements with large volumes of data.
* D. Data Engineers who create clustered tables with frequent reads against clustering keys.

**Correct Answer:** B

**Overall Explanation:**

The BEST suited use case for the Snowflake Search Optimization Service is: `B. Business users who need fast response times using highly selective filters`.

## Question 12

**A Data Engineer has written a stored procedure that will run with caller's rights. The Engineer has granted a role named "ROLEA", the right to use this stored procedure. What is a characteristic of the stored procedure being called using "ROLEA"?**

**Answers:**

* A. The stored procedure must run with caller's rights; it cannot be converted later to run with owner's rights.
* B. If the stored procedure accesses an object that ROLEA does not have access to, the stored procedure will fail.
* C. The stored procedure will run in the context (database and schema) where the owner created the stored procedure
* D. ROLEA will not be able to see the source code for the stored procedure, even though the role has usage privileges on the stored procedure.

**Correct Answer:** B

**Overall Explanation:**

The correct characteristic of the stored procedure being called using ROLEA is: `B. If the stored procedure accesses an object that ROLEA does not have access to, the stored procedure will fail`.

## Question 13

**Within a Snowflake account, permissions have been defined with custom roles and role hierarchies. To set up column-level masking using a role in the hierarchy of the current user, what command would be used?**

**Answers:**

* A. CURRENT_ROLE
* B. INVOKER_ROLE
* C. IS_ROLE_IN_SESSION
* D. IS_GRANTED_TO_INVOKER_ROLE

**Correct Answer:** D

**Overall Explanation:**

The correct command to set up column-level masking using a role in the hierarchy of the current user within a Snowflake account is: `D. IS_GRANTED_TO_INVOKER_ROLE`

## Question 14

**A Data Engineer is trying to load the following rows from a CSV file into a table in Snowflake with the following structure

**Answers:**

* A. ESCAPE_UNENCLOSED FIELD = '\\\\'
* B. ERROR_ON_COLUMN_COUNT_MISMATCH = FALSE
* C. FIELD_DELIMITER = ','
* D. FIELD_OPTIONALLY_ENCLOSED_BY = '"'

**Correct Answer:** D

**Overall Explanation:**

Answer: `D. FIELD_OPTIONALLY_ENCLOSED_BY = '"'`

## Question 15

**A Data Engineer wants to check the status of a pipe named `myPipe` (case-sensitive). The pipe is inside a database named `test` and a schema named `extract`. Which query will provide the status of the pipe?**

**Answers:**

* A. SELECT SYSTEM$PIPE_STATUS("test.extract.myPipe")
* B. SELECT SYSTEM$PIPE_STATUS('test.extract."myPipe"')
* C. SELECT * FROM SYSTEM$PIPE_STATUS('test.extract."mypipe"')
* D. SELECT * FROM SYSTEM$PIPE_STATUS("test.extract.'myPipe'")

**Correct Answer:** B

**Overall Explanation:**

The correct option to check the status of the pipe named `my_pipe` in the database `test` and schema `Extract` is:  `B. SELECT SYSTEM$PIPE_STATUS('test.extract."myPipe"')`

## Question 15

**A Data Engineer wants to check the status of a pipe named `myPipe` (case-sensitive). The pipe is inside a database named `test` and a schema named `extract`. Which query will provide the status of the pipe?**

**Answers:**

* A. SELECT SYSTEM$PIPE_STATUS("test.extract.myPipe")
* B. SELECT SYSTEM$PIPE_STATUS('test.extract."myPipe"')
* C. SELECT * FROM SYSTEM$PIPE_STATUS('test.extract."mypipe"')
* D. SELECT * FROM SYSTEM$PIPE_STATUS("test.extract.'myPipe'")

**Correct Answer:** B

**Overall Explanation:**

The correct option to check the status of the pipe named `my_pipe` in the database `test` and schema `Extract` is:  `B. SELECT SYSTEM$PIPE_STATUS('test.extract."myPipe"')`

## Question 16

**A secure function returns data coming through an inbound share. What will happen if a Data Engineer tries to assign USAGE privileges on this function to an outbound share?**

**Answers:**

* A. An error will be returned because the Engineer cannot share data that has already been shared.
* B. An error will be returned because only views and secure stored procedures can be shared.
* C. An error will be returned because only secure functions can be shared with inbound shares.
* D. The Engineer will be able to share the secure function with other accounts.

**Correct Answer:** A

**Overall Explanation:**

Answer: `A`

Explanation:

**Resources:**

* https://www.snowflake.com/wp-content/uploads/2017/08/Enriching-your-analytics-with-data-shared-through-Snowflake.pdf

## Question 17

**A Data Engineer is implementing a near real-time ingestion pipeline to load data into Snowflake using the Snowflake Kafka connector. There will be three Kafka topics created. Which Snowflake objects are created automatically when the Kafka connector starts? (Choose three)**

**Answers:**

* A. tables
* B. tasks
* C. pipes
* D. Internal stages
* E. External stages
* F. Materialized views

**Correct Answer:** A, C, and D

**Overall Explanation:**

Correct Answers:

* **A. Tables** (One table for each Kafka topic)
* **C. Pipes** (One pipe for each Kafka topic partition)
* **D. Internal stages** (One internal stage for each Kafka topic)

Explanation:

**Resources:**

* https://docs.snowflake.com/en/user-guide/kafka-connector-overview

## Question 18

**A Data Engineer has created table `t1` with one column `c1` with datatype `VARIANT`: The Engineer has loaded the following JSON data set, which has information about 4 laptop models, into the table. The Engineer now wants to query that data set so that results are shown as normal structured data. The result should be 4 rows and 4 columns, without the double quotes surrounding the data elements in the JSON data. Which select command will produce the correct results?**

**Answers:**

* A. `select value:model_id::string , value:model::string , value:manufacturer::string , value:model_name::string from t1, lateral flatten(input =&gt; c1);`
* B. `select value:model_id::string , value:model::string , value:manufacturer::string , value:model_name::string from t1, lateral flatten(input =&gt; c1:device_model);`
* C. `select model_id::string, model::string , manufacturer::string , model_name::string from t1, lateral flatten (input =&gt; c1:device_model);`
* D. `select value:model_id, value:model, value:manufacturer, value:model_name from t1, lateral flatten (input =&gt; c1:device_model);`

**Correct Answer:** B

**Overall Explanation:**

The correct answer is: `B`

`select value:model_id::string , value:model::string , value:manufacturer::string , value:model_name::string from t1, lateral flatten(input =&gt; c1:device_model);`

Explanation:

**Resources:**

* https://docs.snowflake.com/user-guide/tutorials/json-basics-tutorial#flatten-data
* https://docs.snowflake.com/en/sql-reference/data-type-conversion

## Question 19

**Which methods will trigger an action that will evaluate a DataFrame? (Choose two)**

**Answers:**

* A. DataFrame.random_split()
* B. DataFrame.collect()
* C. DataFrame.select()
* D. DataFrame.col()
* E. DataFrame.show()

**Correct Answer:** B and E

**Overall Explanation:**

The correct answers are: `B. DataFrame.collect() and E. DataFrame.show()`

Explanation:

**Resources:**

* https://docs.snowflake.com/en/developer-guide/snowpark/reference/python/1.3.0/api/snowflake.snowpark.DataFrame

## Question 20

**A table is loaded using Snowpipe and truncated afterwards. Later, a Data Engineer finds that the table needs to be reloaded, but the metadata of the pipe will not allow the same files to be loaded again. How can this issue be solved using the LEAST amount of operational overhead ?**

**Answers:**

* A. Wait until the metadata expires and then reload the file using Snowpipe.
* B. Modify the file by adding a blank row to the bottom and re-stage the file.
* C. Set the `FORCE=TRUE` option in the Snowpipe `COPY INTO` command.
* D. Recreate the pipe by using the `CREATE OR REPLACE PIPE` command.

**Correct Answer:** D

**Overall Explanation:**

The correct answer is: `D. Recreate the pipe by using the CREATE OR REPLACE PIPE command.`

Explanation:

**Resources:**

* https://docs.snowflake.com/en/user-guide/data-load-snowpipe-ts#unable-to-reload-modified-data-modified-data-loaded-unintentionally
* https://docs.snowflake.com/en/sql-reference/sql/create-pipe#usage-notes

## Question 21

**A Data Engineer enables a result cache at the session level with the following command:**

`sql
ALTER SESSION SET USE_CACHED_RESULT = TRUE;
Use code with caution.

The Engineer then runs the following SELECT query twice without delay:

SQL
SELECT *
FROM SNOWFLAKE_SAMPLE_DATA.binni_udemy.CUSTOMERS
SAMPLE(100) SEED (95);
`

The underlying table does not change between executions.

What are the results of both runs ?

Answers:

A. The first and second run returned the same results, because SAMPLE is deterministic.
B. The first and second run returned the same results, because the specific SEED value was provided.
C. The first and second run returned different results, because the query is evaluated each time it is run.
D. The first and second run returned different results, because the query uses * instead of an explicit column list.
**Correct Answer:** B

**Overall Explanation:**

The correct answer is: B. The first and second run will return the same results, because the specific SEED value was provided..

**Resources:**

https://docs.snowflake.com/en/user-guide/querying-persisted-results
https://docs.snowflake.com/en/sql-reference/constructs/sample

## Question 22

**When would a Data Engineer use TABLE with the `FLATTEN` function instead of the `LATERAL FLATTEN` combination ?**

**Answers:**

* A. When TABLE with FLATTEN requires another source in the FROM clause to refer to
* B. When TABLE with FLATTEN requires no additional source in the FROM clause to refer to.
* C. When the LATERAL FLATTEN combination requires no other source in the FROM clause to refer to.
* D. When TABLE with FLATTEN is acting like a sub-query executed for each returned row.

**Correct Answer:** B

**Overall Explanation:**

The correct answer is: `B. When TABLE with FLATTEN requires no additional source in the FROM clause to refer to.`

**Resources:**

* https://docs.snowflake.com/en/sql-reference/functions/flatten

## Question 23

**A Data Engineer ran a stored procedure containing various transactions. During the execution, the session abruptly disconnected, preventing one transaction from committing or rolling back. The transaction was left in a detached state and created a lock on resources.**

**What step must the Engineer take to immediately run a new transaction ?**

**Answers:**

* A. Call the system function `SYSTEM$ABORT_TRANSACTION`
* B. Call the system function `SYSTEM$CANCEL_TRANSACTION`
* C. Set the `LOCK_TIMEOUT` to `FALSE` in the stored procedure.
* D. Set the `TRANSACTION_ABORT_ON_ERROR` to `TRUE` in the stored procedure.

**Correct Answer:** A

**Overall Explanation:**

The correct answer to resolve the detached transaction and allow running a new transaction immediately is: `A. Call the system function SYSTEM$ABORT_TRANSACTION`

**Resources:**

* https://docs.snowflake.com/en/sql-reference/functions/system_abort_transaction

## Question 24

**A company is building a dashboard for thousands of Analysts. The dashboard presents the results of a few summary queries on tables that are regularly updated. The query conditions vary by topic according to what data each Analyst needs. Responsiveness of the dashboard queries is a top priority, and the data cache should be preserved.**

**How should the Data Engineer configure the compute resources to support this dashboard ?**

**Answers:**

* A. Assign queries to a multi-cluster virtual warehouse with economy auto-scaling. Allow the system to automatically start and stop clusters according to demand
* B. Assign all queries to a multi-cluster virtual warehouse set to maximized mode. Monitor to determine the smallest suitable number of clusters.
* C. Create a virtual warehouse for every 250 Analysts. Monitor to determine how many of these virtual warehouses are being utilized at capacity
* D. Create a size XL virtual warehouse to support all the dashboard queries. Monitor query runtimes to determine whether the virtual warehouse should be resized.

**Correct Answer:** B

**Overall Explanation:**

**Correct Answer:** `B. Assign all queries to a multi-cluster virtual warehouse set to maximized mode. Monitor to determine the smallest suitable number of clusters.`

**Resources:**

* https://docs.snowflake.com/en/user-guide/warehouses-multicluster

## Question 25

**A company has an extensive script in Scala that transforms data by leveraging DataFrames. A Data Engineer needs to move these transformations to Snowpark.**

**What characteristics of data transformations in Snowpark should be considered to meet this requirement ? (Choose two)**

**Answers:**

* A. It is possible to join multiple tables using DataFrames.
* B. Snowpark operations are executed lazily on the server.
* C. User-Defined Functions (UDFs) are not pushed down to Snowflake.
* D. Snowpark requires a separate cluster outside of Snowflake for computations.
* E. Columns in different DataFrames with the same name should be referred to with squared brackets.

**Correct Answer:** A and B

**Overall Explanation:**

**Correct Answers:**

* A. It is possible to join multiple tables using DataFrames.
* B. Snowpark operations are executed lazily on the server.

**Resources:**

* https://docs.snowflake.com/en/developer-guide/snowpark/python/working-with-dataframes

## Question 26

**A new CUSTOMER table is created by a data pipeline in a Snowflake schema where MANAGED ACCESS is enabled.**

**Which roles can grant access to the CUSTOMER table? (Choose three)**

**Answers:**

* A. The role that owns the schema
* B. The role that owns the database
* C. The role that owns the CUSTOMER table
* D. The SYSADMIN role
* E. The SECURITYADMIN role
* F. The USERADMIN role with the MANAGE GRANTS privilege

**Correct Answer:** A, E & F

**Overall Explanation:**

**Correct Options: **`A, E` & `F`

**Resources:**

* https://docs.snowflake.com/user-guide/security-access-control-overview#securable-objects
* https://docs.snowflake.com/en/user-guide/security-access-control-overview#system-defined-roles

## Question 27

**Which query will show a list of the 30 most recent executions of a specified task named '`MYTASK`' that have been scheduled within the last hour and have ended or are still running ?**

**Answers:**

* A. `select * from table (information_schema.task_history (scheduled_time_range_start => dateadd('hour', -1, current_timestamp()),result_limit => 30, task_name => 'MYTASK'));`
* B. `select * from table (information_schema.task_history (scheduled_time_range_start => dateadd('hour', -1, current_timestamp()),result_limit => 30, task_name => 'MYTASK')) where query_id IS NOT NULL;`
* C. `select * from table (information_schema.task_history (scheduled_time_range_start => dateadd('hour', -1, current_timestamp()),result_limit => 30, task_name => 'MYTASK')) where STATE IN ('EXECUTING', 'SUCCEEDED', 'FAILED');`
* D. `select * from table (information_schema.task_history (scheduled_time_range_end => dateadd('hour', -1, current_timestamp()),result_limit => 30, task_name => 'MYTASK')) where STATE IN ('EXECUTING', 'SUCCEEDED')`

**Correct Answer:** B

**Overall Explanation:**

**Correct Option: **`B`

**Resources:**

* https://docs.snowflake.com/en/sql-reference/functions/task_history#arguments

## Question 28

**A Data Engineer is working on a Snowflake deployment in AWS eu-west-1 (Ireland). The Engineer is planning to load data from staged files into target tables using the COPY INTO command.**

**Which sources are valid ? (Choose three.)**

**Answers:**

* A. Internal stage on GCP us-central1 (Iowa)
* B. Internal stage on AWS eu-central-1 (Frankfurt)
* C. External stage on GCP us-central1 (Iowa)
* D. External stage in an Amazon S3 bucket on AWS eu-west-1 (Ireland)
* E. External stage in an Amazon S3 bucket on AWS eu-central-1 (Frankfurt)
* F. SSD attached to an Amazon EC2 instance on AWS eu-west-1 (Ireland)

**Correct Answer:** C, D and E

**Overall Explanation:**

**Correct Options:**

* **C. External stage on GCP us-central1 (Iowa)**
* **D. External stage in an Amazon S3 bucket on AWS eu-west-1 (Ireland)**
* **E. External stage in an Amazon S3 bucket on AWS eu-central-1 (Frankfurt)**

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/copy-into-table

## Question 29

**Given the table `Sales` which has a clustering key of column `Closed_date`, which table function will return the average clustering depth for the `sales_representative` column for the `North America` region ?**

**Answers:**

* A. `select system$clustering_information('Sales', 'sales_representative', 'region = "North America"')`
* B. `select system$clustering_depth('Sales', 'sales_representative', 'region = "North America"')`
* C. `select system$clustering_depth('Sales', 'sales_representative') where region = 'North America'`
* D. `select system$clustering_information('Sales', 'sales_representative') where region = 'North America'`

**Correct Answer:** B

**Overall Explanation:**

**Correct Option: **`B. select system$clustering_depth('Sales', 'sales_representative', 'region = "North America"')`

**Resources:**

* https://docs.snowflake.com/en/sql-reference/functions/system_clustering_depth
* https://docs.snowflake.com/en/sql-reference/functions/system_clustering_information

## Question 30

**A Data Engineer needs to load JSON output from some software into Snowflake using Snowpipe.**

**Which recommendations apply to this scenario ? (Choose three.)**

**Answers:**

* A. Load large files (1 GB or larger).
* B. Ensure that data files are 100-250 MB (or larger) in size, compressed.
* C. Load a single huge array containing multiple records into a single table row.
* D. Verify each value of each unique element stores a single native data type (string or number).
* E. Extract semi-structured data elements containing null values into relational columns before loading.
* F. Create data files that are less than 100 MB and stage them in cloud storage at a sequence greater than once each minute.

**Correct Answer:** B, D and E

**Overall Explanation:**

**Correct Options:**

* `B. Ensure that data files are 100-250 MB (or larger) in size, compressed.`
* `D. Verify each value of each unique element stores a single native data type (string or number).`
* `E. Extract semi-structured data elements containing null values into relational columns before loading.`

**Resources:**

* https://docs.snowflake.com/en/user-guide/data-load-considerations-prepare#label-snowpipe-file-size

## Question 31

**A Data Engineer is determining how to cluster the following table, which is used to record orders from a food delivery service application:**

`sql
CREATE TABLE orders_dashboard (
    id NUMBER, 
    driver_id NUMBER, 
    customer_id NUMBER, 
    restaurant_ id NUMBER, 
    ordered_at TIMESTAMP, 
    item_count INTEGER, 
    total_cost NUMBER, 
    order_location_state CHAR (2), 
    order_comments TEXT
);
`

The purpose of this table is to provide metrics for regional sales managers to understand how deliveries in each region are performing over various timeframes.

Given that queries will be run against this table, what would be the MOST efficient clustering statement for this table ?

**Answers:**

* A. alter table orders_dashboard cluster by (order_location_state, DATE (ordered_at));
* B. alter table orders_dashboard cluster by (order_location_state, ordered_at);
* C. alter table orders_dashboard cluster by (ordered_at, order_location_state);
* D. alter table orders_dashboard cluster by (DATE (ordered_at), order_location_state);
Correct Answer: A

**Overall Explanation:**

**The correct answer is: ** A. alter table orders_dashboard cluster by (order_location_state, DATE (ordered_at));

**Explanation:**

Snowflake recommends ordering the columns from lowest cardinality to highest cardinality.
Putting a higher cardinality column before a lower cardinality column will generally reduce the effectiveness of clustering on the latter column.   

**Resources:**

https://docs.snowflake.com/en/user-guide/tables-clustering-keys

## Question 32

**What is the purpose of the `VALIDATE` function ?**

**Answers:**

* A. Allows a user to perform a dry-run of the load process to expose errors.
* B. Outputs a pdf to a configured stage of all the errors of a past execution.
* C. Allows a user to view all errors encountered during a previous COPY INTO execution.
* D. Allows a user to view all errors encountered during all previous runs of a COPY INTO execution.

**Correct Answer:** C

**Overall Explanation:**

The correct answer for the purpose of the `VALIDATE` function in Snowflake is: `C. Allows a user to view all errors encountered during a previous COPY INTO execution.`

**Resources:**

* https://docs.snowflake.com/en/sql-reference/functions/validate

## Question 33

**What does it meant by overloading a User Defined Function (UDF) ?**

**Answers:**

* A. The ability for multiple UDFs to exist with the same identifier but different input arguments.
* B. The ability of a UDF to accept more than one argument.
* C. A UDF can returning more than one row.
* D. The ability to call a UDF from within another UDF.

**Correct Answer:** A

**Overall Explanation:**

The correct answer is: `A. The ability for multiple UDFs to exist with the same identifier but different input arguments.`

**Resources:**

* https://docs.snowflake.com/en/developer-guide/udf-stored-procedure-naming-conventions#overloading-procedures-and-functions

## Question 34

**A data engineer is running some transformation jobs using a virtual warehouse. The virtual warehouse seems to be suspending between the jobs, making subsequent jobs take longer.**

**What could be the issue ?**

**Answers:**

* A. The Virtual Warehouse `INITIALLY_SUSPEND` property is set to `TRUE`.
* B. The Virtual Warehouse is too small for the workload they're running.
* C. The Virtual Warehouse `AUTO_SUSPEND` property (in seconds) is set too low.
* D. The Virtual Warehouse `AUTO_RESUME` property is set to `FALSE`.

**Correct Answer:** C

**Overall Explanation:**

The correct answer is: `C. The Virtual Warehouse AUTO_SUSPEND property (in seconds) is set too low.`

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/alter-warehouse

## Question 35

**You have below table:**

**Which `ALTER` commands might impact a column's availability in Time Travel ?**

**Answers:**

* A. `ALTER TABLE t1 ALTER COLUMN c1 DROP NOT NULL;`
* B. `ALTER TABLE t1 MODIFY c2 DROP DEFAULT;`
* C. `ALTER TABLE t1 ALTER c4 SET DATA TYPE VARCHAR(50);`
* D. `ALTER TABLE t1 ALTER c2 SET DATA TYPE NUMBER(10,2);`
* E. `ALTER TABLE t1 ALTER c5 COMMENT '50 character column';`

**Correct Answer:** D

**Overall Explanation:**

**Correct Answer: **`D`

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/alter-table-column

## Question 36

**You have two tables have been created in the same schema with the same information.**

**One is a Secure View; the second one is a standard View.**

**When executing a query, the profiler doesn\'92t show the same information.**

**How is this possible ?**

**Answers:**

* A. The underlying table is corrupted
* B. Secure views do not expose the underlying tables or internal structural details
* C. The user role doesn\'92t have access to the view
* D. The Secure View is encrypted while the standard View is not

**Correct Answer:** B

**Overall Explanation:**

**Correct Answer: **`B. Secure views do not expose the underlying tables or internal structural details.`

**Resources:**

* https://docs.snowflake.com/en/user-guide/views-secure

## Question 37

**When data is transferred from a Snowflake primary account to another target account using database replication, which account is billed for the data transfer and compute charges ?**

**Answers:**

* A. The primary account is charged for the compute charges and the target account is charged for the data transfer charges.
* B. The primary account is charged for both the data transfer and compute charges.
* C. The primary account is charged for the data transfer charges and the target account is charged for the compute charges.
* D. The target account is charged for both the data transfer and compute charges.

**Correct Answer:** D

**Overall Explanation:**

**Answer: **`D. The target account is charged for both the data transfer and compute charges.`

**Resources:**

* https://docs.snowflake.com/en/user-guide/account-replication-cost

## Question 38

**How does Snowflake handle the transition due to daylight savings time in scheduled tasks ?**

**(Select 2)**

**Answers:**

* A. A task scheduled based on UTC time will remain unaffected by daylight savings time changes.
* B. A task's schedule strictly adheres to the specified time, failing to account for hours lost or duplicated due to daylight savings time.
* C. Schedules that execute tasks frequently, such as every minute, may not encounter issues, but the task history could be affected.
* D. During the transition to daylight savings time, a task will enter a suspended state.
* E. Snowflake tasks automatically adjust their schedules to match the local daylight savings time changes.

**Correct Answer:** A and B

**Overall Explanation:**

**The correct answers are: **`A and B`

**Resources:**

* https://docs.snowflake.com/en/user-guide/tasks-intro#task-scheduling-and-daylight-saving-time

## Question 39

**A Data Engineer is tasked with creating a Snowflake task that executes a stored procedure named `sprocA`. The stored procedure is owned by the role `analyst`. The task should execute daily at 8:00 AM UTC using the `analyst` role's privileges.**

**Which command will accomplish this ?**

**Answers:**

* A. 

`sql
CREATE TASK mytask
    WAREHOUSE = COMPUTE_WH
    SCHEDULE = 'USING CRON 0 8 * * * UTC'
    AS
    EXECUTE PROCEDURE analyst.sprocA();
Use code with caution.

B.
SQL
CREATE TASK mytask
    WAREHOUSE = COMPUTE_WH
    SCHEDULE = 'USING CRON 0 8 * * * UTC'
    USER TASK_ADMIN
    AS
    EXECUTE PROCEDURE analyst.sprocA();
Use code with caution.

C.
SQL
CREATE TASK mytask
    WAREHOUSE = COMPUTE_WH
    SCHEDULE = '8:00 UTC'
    AS
    CALL sprocA();
Use code with caution.

D.
SQL
CREATE TASK mytask
    WAREHOUSE = COMPUTE_WH
    SCHEDULE = '0 8 * * * UTC'
    AS
    EXECUTE PROCEDURE sprocA();
`

**Correct Answer:** A

**Overall Explanation:**

**Correct Option: **A

**Resources:**

https://docs.snowflake.com/en/sql-reference/sql/create-task



## Question 40

**Which Snowpark operations can be performed on a DataFrame?**

**Answers:**

* A. `select`, `filter`, `sort`
* B. `create`, `insert`, `delete`
* C. `grant`, `revoke`, `describe`
* D. `merge`, `update`, `drop`

**Correct Answer:** A

**Overall Explanation:**

**Correct Answer:** `A. select, filter, sort`

**Resources:**

* https://docs.snowflake.com/en/developer-guide/snowpark/python/working-with-dataframes