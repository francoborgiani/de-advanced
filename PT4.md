## Practice Test 4 - Results

**Attempt 1**

### Question 1

Which of the following options is not a compression technique for `**AVRO**` file formats?

**Answers:**

* AUTO
* GZIP
* ZSTD
* BZ2 (Correct answer)
* DEFLATE (Your answer is incorrect)

**Overall explanation:**

AVRO compression techniques are very similar to XML, JSON, and CSV; the only difference is that it doesn't accept BZ2 compression. You can see the different compression types for each file format in the following image:

**Resources:**

* None

### Question 2

Which steps are recommended best practices for prioritizing cluster keys in Snowflake? (Select 2)

**Answers:**

* Choose cluster columns that are actively used in the GROUP BY clauses.
* Choose columns that are frequently used in join predicates. (Correct selection)
* Choose lower cardinality columns to support clustering keys and cost-effectiveness. (Your selection is incorrect)
* Choose TIMESTAMP columns with nanoseconds for the highest number of unique rows.
* Choose cluster columns that are most actively used in selective filters. (Your selection is correct)

**Overall explanation:**

**Correct Answer:** `B and E`

A column with very low cardinality might yield only minimal pruning, such as a column named `IS_NEW_CUSTOMER` that contains only Boolean values. At the other extreme, a column with very high cardinality is also typically not a good candidate to use as a clustering key directly.

In some cases, clustering on columns used in `GROUP BY` or `ORDER BY` clauses can be helpful. However, clustering on these columns is usually less helpful than clustering on columns that are heavily used in filter or `JOIN` operations. If you have some columns that are heavily used in filter/join operations and different columns that are used in `ORDER BY` or `GROUP BY` operations, then favor the columns used in the filter and join operations.

**Resources:**

* https://docs.snowflake.com/en/user-guide/tables-clustering-keys

### Question 3

Which pipes are cloned when cloning a database or schema?

**Answers:**

* Pipes that reference internal stages
* Pipes that reference external stages (Correct answer)
* Both A and B
* None of these (Your answer is incorrect)

**Overall explanation:**

**Correct Answer:** `B. Pipes that reference external stages`

**Explanation:**

When you clone a database or schema in Snowflake, only pipes that reference **external stages** are included in the clone. Here's a breakdown of how pipes are handled during cloning:

* **Internal Stages:** Pipes referencing internal stages (i.e., stages residing within the same Snowflake account) are **not cloned**. This is because internal stages already exist in the cloned database or schema, so there's no need to duplicate them.
* **External Stages:** Pipes referencing external stages (e.g., stages in Amazon S3, Google Cloud Storage, or Azure Blob Storage) **are cloned**. This ensures that the cloned database or schema can still access the external data source for loading purposes.

**Incorrect Answers:**

* **A. Pipes that reference internal stages:** As explained above, these pipes are not cloned because the internal stages already exist in the cloned environment.
* **Both A and B:** Only pipes referencing external stages are cloned.
* **None of these:** Pipes referencing external stages are indeed cloned during database or schema cloning.

**Resources:**

* https://docs.snowflake.com/en/user-guide/object-clone

### Question 4

A copy command is executed to load a file. After the file has loaded and the metadata has expired, which options can be used to reload the file? (Select 2)

**Answers:**

* Set the `PRESERVE_SPACE` option to `TRUE`.
* Set the `DISABLE_SNOWFLAKE_DATA` option to `TRUE`.
* Set the `ALLOW_DUPLICATE` option to `TRUE`. (Your selection is incorrect)
* Set the `LOAD_UNCERTAIN_FILES` option to `TRUE`. (Correct selection)
* Set the `FORCE` option to `TRUE`. (Your selection is correct)

**Overall explanation:**

**Correct Answers:**

* D. Set the LOAD_UNCERTAIN_FILES option to TRUE.
* E. Set the FORCE option to TRUE.

**Explanation:**

**E. FORCE (TRUE):**

* Forces Snowflake to load the file regardless of existing metadata (including expired metadata).
* This option is best used with caution as it will definitely overwrite existing data in the table with the new content from the file, even if the file hasn't changed.

**Incorrect Answers:**

* A. PRESERVE_SPACE (TRUE): This option is used to reserve space during a `COPY INTO` operation for potential future growth of the table. It doesn't affect metadata expiration or reloading.
* B. DISABLE_SNOWFLAKE_DATA (TRUE): This option is not valid in the context of `COPY INTO`. Snowflake data refers to data managed by Snowflake internally, not external files.
* C. ALLOW_DUPLICATE (TRUE): While this option doesn't directly address metadata expiration, it allows duplicate rows to be inserted during the `COPY INTO` process, regardless of the file's content (new or existing). However, it wouldn't guarantee reloading an expired file unless explicitly combined with `FORCE` or `LOAD_UNCERTAIN_FILES`.

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/copy-into-table

### Question 5

A Data Engineer is making performance improvements to Snowflake processes and adjusting the sizing of virtual warehouses. What technique does Snowflake recommend for determining which virtual warehouse size to select?

**Answers:**

* Experiment by running the same queries against warehouses of different sizes (Your answer is correct)
* Always start with an X-Small and increase the size if the query does not complete in 2 minutes
* Use X-Large or above for tables larger than 1 GB
* Use the default size Snowflake chooses

**Overall explanation:**

The correct answer is: **A. Experiment by running the same queries against warehouses of different sizes**

Here's a breakdown of each option and why it's correct or incorrect:

**A. Correct:** Snowflake recommends experimenting with different virtual warehouse sizes to determine the optimal size for your workload.

This allows you to find the balance between performance and cost.

Running the same query against different sizes lets you compare execution times and identify the most efficient option.

**B. Incorrect:** While starting with a smaller size (like X-Small) is a good initial approach, the 2-minute completion time is not a definitive benchmark.

Query complexity and data volume play a bigger role.

**C. Incorrect:** Warehouse size isn't solely dependent on table size.

Complex queries on smaller tables can still benefit from larger warehouses.

Consider factors like query complexity, data access patterns, and desired execution time.

**D. Incorrect:** Snowflake doesn't assign a default warehouse size.

You have the flexibility to choose the size that best suits your needs based on workload and performance requirements.

**Resources:**

* https://docs.snowflake.com/en/user-guide/warehouses-considerations

### Question 6

Which are the two limitations of the `insertFiles` API of Snowpipe? (Select 2)

**Answers:**

* The post can contain at most 10000 files.
* Each file path given must be <= 512 bytes long when serialized as UTF-8. (Your selection is incorrect)
* The post can contain at most 5000 files. (Correct selection)
* Each file path given must be <= 1024 bytes long when serialized as UTF-8. (Correct selection)
* The post can contain at most 1000 files. (Your selection is incorrect)

**Overall explanation:**

**Correct Answers:**

* **C. The post can contain at most 5000 files.**
* **D. Each file path given must be <= 1024 bytes long when serialized as UTF-8.**

**Explanation:**

Here's a breakdown of each option and why it's correct or incorrect:

**A. Incorrect:** While there might be limitations on the total data size, the documented limit for the number of files in a single `insertFiles` API request is indeed 5000 (as stated in option C).

**B. Incorrect:** This seems like a potential limitation, but the actual documented limit for file path length is 1024 bytes when serialized as UTF-8 (as stated in option D).

**C. Correct:** Snowpipe has a documented limit of 5000 files per `insertFiles` API request.

Exceeding this limit will require splitting your data into multiple requests.

**D. Correct:** Snowpipe enforces a maximum file path length of 1024 bytes when serialized as UTF-8.

This includes the directory structure leading to the file. Keep your file paths concise to stay within this limit.

**E. Incorrect:** The documented limit for the number of files is 5000, not 1000.

**Resources:**

* https://docs.snowflake.com/en/user-guide/data-load-snowpipe-rest-apis#endpoint-insertfiles

### Question 7

When would you usually consider adding a clustering key to a table? (Select 2)

**Answers:**

* The clustering depth for the table is large. (Your selection is correct)
* The number of users querying the table has increased.
* The table has more than 20 columns.
* The performance of the query has deteriorated over a period of time. (Your selection is correct)

**Overall explanation:**

**Answer:** `A and D`

**Explanation:**

A clustering key is a subset of columns in a table (or expressions on a table) that are explicitly designated to co-locate the data in the table in the same [micro-partitions](https://docs.snowflake.com/en/user-guide/tables-clustering-micropartitions). This is useful for very large tables where the ordering was not ideal (at the time the data was inserted/loaded) or extensive DML has caused the table's natural clustering to degrade.

**Resources:**

* https://docs.snowflake.com/en/user-guide/tables-clustering-keys#what-is-a-clustering-key

### Question 8

How can we add a clustering key to the existing table `**MYTABLE**` in the columns `USER` and `CREATED_AT`?

**Answers:**

* `ALTER TABLE MYTABLE CREATE CLUSTER_KEY (USER, CREATED_AT);`
* `ALTER TABLE MYTABLE ADD CLUSTER_KEY (USER, CREATED_AT);`
* `ALTER TABLE MYTABLE CLUSTER BY (USER, CREATED_AT);` (Your answer is correct)
* `ALTER TABLE MYTABLE CLUSTER BY USER AND CLUSTER BY CREATED_AT;`

**Overall explanation:**

**Correct Answer:** `C. ALTER TABLE MYTABLE CLUSTER BY (USER, CREATED_AT);` 

**Resources:**

* https://docs.snowflake.com/en/user-guide/tables-clustering-keys#changing-the-clustering-key-for-a-table

### Question 9

A company is storing large numbers of small JSON files (ranging from 1-4 bytes) that are received from IoT devices and sent to a cloud provider. In any given hour, 100,000 files are added to the cloud provider.

What is the MOST cost-effective way to bring this data into a Snowflake table?

**Answers:**

* A copy command at regular intervals
* A pipe (Correct answer)
* An external table (Your answer is incorrect)
* A stream

**Overall explanation:**

**The correct answer is:** `B. A pipe`

**Explanation:**

External tables in Snowflake allow querying data that is stored externally, such as in an Amazon S3 bucket.

However, they do not actually load the data into Snowflake, so they are not a cost-effective solution for this use case.

**D. A stream**

A stream in Snowflake is a change data capture (CDC) object that captures changes (inserts, updates, deletes) made to a table.

It is not used for loading data into a table.

**Resources:**

* https://docs.snowflake.com/user-guide/data-load-snowpipe-intro
* https://docs.snowflake.com/en/user-guide/streams

### Question 10

A Data Engineer is building a set of reporting tables to analyze consumer requests by region for each of the Data Exchange offerings annually, as well as click-through rates for each listing. Which views are needed MINIMALLY as data sources?

**Answers:**

* SNOWFLAKE.DATA_SHARING_USAGE.LISTING_CONSUMPTION_DAILY (Your answer is incorrect)
* SNOWFLAKE.DATA_SHARING_USAGE.LISTING_CONSUMPTION_DAILY, SNOWFLAKE.DATA_SHARING_USAGE.LISTINGS
* SNOWFLAKE.DATA_SHARING_USAGE.LISTING_CONSUMPTION_DAILY, SNOWFLAKE.ACCOUNT_USAGE.DATABASE_STORAGE_USAGE_HISTORY
* SNOWFLAKE.DATA_SHARING_USAGE.LISTINGS (Correct answer)

**Overall explanation:**

**Correct Answer:** `D. SNOWFLAKE.DATA_SHARING_USAGE.LISTINGS`

**Explanation:**

The question asks for the **minimum** views needed to analyze consumer requests by region for Data Exchange offerings annually, as well as click-through rates for each listing.

The `SNOWFLAKE.DATA_SHARING_USAGE.LISTINGS` view provides information about data exchange listings, including:

* Listing name
* Provider name
* Consumer count
* Clicks
* Creation date

This information is sufficient to analyze consumer requests by region and click-through rates.

**Incorrect Answers:**

* **A. SNOWFLAKE.DATA_SHARING_USAGE.LISTING_CONSUMPTION_DAILY:** This view provides daily consumption data for listings, but it doesn't include information about clicks or regions.
* **B. SNOWFLAKE.DATA_SHARING_USAGE.LISTING_CONSUMPTION_DAILY, SNOWFLAKE.DATA_SHARING_USAGE.LISTINGS:** While this combination provides all the necessary information, it's not the minimal set of views required.
* **C. SNOWFLAKE.DATA_SHARING_USAGE.LISTING_CONSUMPTION_DAILY, SNOWFLAKE.ACCOUNT_USAGE.DATABASE_STORAGE_USAGE_HISTORY:** This combination is irrelevant to the question as it doesn't provide information about data exchange listings or consumer requests.

**Resources:**

* https://docs.snowflake.com/en/sql-reference/account-usage/database_storage_usage_history
* https://docs.snowflake.com/en/sql-reference/data-sharing-usage/listing_consumption_daily
* https://docs.snowflake.com/en/sql-reference/data-sharing-usage/listings

### Question 11

Which of the following commands will return all the columns and all the rows from the table `MY_TABLE`?

**Answers:**

* `SELECT * FROM MY_TABLE` (Your answer is correct)
* `SELECT ALL FROM MY_TABLE`
* `SELECT TOP 100 PERCENT FROM MY_TABLE`

**Overall explanation:**

**Correct Answer:** `A. SELECT * FROM MY_TABLE`

**Explanation:**

In SQL, the `SELECT` statement is used to retrieve data from a table. The asterisk (*) is a wildcard character that represents all columns in the table. Therefore, `SELECT * FROM MY_TABLE` will return all columns and all rows from the table `MY_TABLE`.

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/select

### Question 12

Which of the following is NOT a valid `MASKING POLICY` command?

**Answers:**

* `CREATE OR REPLACE MASKING POLICY email_mask ON employees ADD MASK employees.email_address (email_mask_func(email_address));` (Your answer is correct)
* `CREATE OR REPLACE MASKING POLICY email_mask ON employees ADD MASK employees.salary (email_mask_func(salary));`
* `CREATE OR REPLACE MASKING POLICY email_mask ON employees ADD MASK employees.email_address (default());`

**Overall explanation:**

**Correct Answer:** `A. CREATE OR REPLACE MASKING POLICY email_mask ON employees ADD MASK employees.email_address (email_mask_func(email_address));`

**Explanation:**

The `CREATE OR REPLACE MASKING POLICY` command is used to create or replace a masking policy in Snowflake. A masking policy defines how to mask sensitive data in a table.

The correct syntax for adding a mask to a column is:

* `sql
CREATE OR REPLACE MASKING POLICY <masking_policy_name> ON <table_name>
    ADD MASK <column_name> (<masking_function_name>(<column_name>));`

In option A, the masking function email_mask_func is called with the column name email_address as an argument. This is incorrect because the masking function should be called with the column value, not the column name.

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/create-masking-policy

### Question 13

Which of the following are valid `SEARCH OPTIMIZATION` commands in Snowflake? (Select 3)

**Answers:**

* `ALTER SEARCH OPTIMIZATION ON TABLE employees SET ENABLED = TRUE;` (Correct selection)
* `ALTER SEARCH OPTIMIZATION ON SCHEMA public SET ENABLED = TRUE;` (Correct selection)
* `ALTER SEARCH OPTIMIZATION ON ACCOUNT SET ENABLED = TRUE;` (Correct selection)
* `ALTER SEARCH OPTIMIZATION ON DATABASE my_database SET ENABLED = TRUE;`
* `ALTER SEARCH OPTIMIZATION ON VIEW my_view SET ENABLED = TRUE;`

**Overall explanation:**

**Correct Answers:**

* **A. ALTER SEARCH OPTIMIZATION ON TABLE employees SET ENABLED = TRUE;**
* **B. ALTER SEARCH OPTIMIZATION ON SCHEMA public SET ENABLED = TRUE;**
* **C. ALTER SEARCH OPTIMIZATION ON ACCOUNT SET ENABLED = TRUE;**

**Explanation:**

Search optimization in Snowflake allows you to improve the performance of queries that use the `SEARCH` clause. You can enable search optimization at the account, schema, or table level.

The `ALTER SEARCH OPTIMIZATION` command is used to enable or disable search optimization. The valid scopes for this command are:

* `ACCOUNT`
* `SCHEMA`
* `TABLE`

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/alter-search-optimization

### Question 14

A Data Engineer is trying to improve the performance of queries that filter on a `TIMESTAMP` column. What is the best way to achieve this?

**Answers:**

* Cluster the table on the `TIMESTAMP` column (Your answer is correct)
* Create an index on the `TIMESTAMP` column
* Partition the table by the `TIMESTAMP` column
* Convert the `TIMESTAMP` column to a `DATE` column

**Overall explanation:**

**Correct Answer:** `A. Cluster the table on the TIMESTAMP column`

**Explanation:**

Clustering a table on a column physically stores related data together, improving the performance of queries that filter on that column.

Since the Data Engineer is trying to improve the performance of queries that filter on a `TIMESTAMP` column, clustering the table on that column is the best way to achieve this.

**Resources:**

* https://docs.snowflake.com/en/user-guide/tables-clustering-keys

### Question 15

Which columns can be included in an external table schema? (Select three)

**Answers:**

* METADATA$FILE_ROW_NUMBER (Correct selection)
* METADATA$ROW_ID (Your selection is incorrect)
* METADATA$ISUPDATE (Your selection is incorrect)
* METADATA$FILENAME (Your selection is correct)
* VALUE (Correct selection)
* METADATA$EXTERNAL_TABLE_PARTITION

**Overall explanation:**

**Answer:** `A, D and E`

**Explanation:**

External table schemas in Snowflake allow you to define the structure of your external data files. You can include these pseudocolumns to provide additional information about the data beyond the actual values:

By incorporating these columns into your schema, you can enrich your understanding of the data and leverage the pseudocolumns for various analytical or data management tasks.

**Resources:**

* https://docs.snowflake.com/en/user-guide/tables-external-intro#schema-on-read

### Question 16

What is the outcome when attempting to `ALTER` a column to `NOT NULL` in Snowflake, if it currently contains `NULL` values?

**Answers:**

* Snowflake returns an error (Your answer is correct)
* NULL values are changed to 0
* Snowflake deletes the rows with NULL values.
* NULL values are changed to an empty string " "

**Overall explanation:**

The answer is: **A. Snowflake returns an error**

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/alter-table-column#usage-notes

### Question 17

Consider the `XML` given below. The XML file is loaded in a User Stage:

Which of the following file format options will be used in the COPY INTO command to  remove the top-level element `&lt;bookshelf/&gt;` and load `&lt;book/&gt;` elements into separate rows in a Snowflake table?

**Answers:**

* STRIP_TOP_ELEMENT
* STRIP_OUTER_ARRAY (Your answer is incorrect)
* STRIP_OUTER_ELEMENT (Correct answer)
* STRIP_FIRST_ELEMENT

**Overall explanation:**

The correct answer is: **C. STRIP_OUTER_ELEMENT**

**Explanation:**

The `STRIP_OUTER_ELEMENT` option proves valuable when dealing with XML data that has a single enclosing element at the top level. It allows Snowflake to treat each `&lt;book&gt;` element within the file as a separate record during the COPY operation, resulting in individual rows within your target table.

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/copy-into-table#type-xml

### Question 18

What are the minimum and the maximum number of clusters in a multi-cluster warehouse?

**Answers:**

* Minimum: 1 Maximum: 99
* Minimum: 1 Maximum: 100 (Your answer is incorrect)
* Minimum: 1 Maximum: unlimited
* Minimum: 1 Maximum: 10 (Correct answer)

**Overall explanation:**

**Answer:** `D.`

**Resources:**

* https://docs.snowflake.com/en/user-guide/warehouses-multicluster

### Question 19

What information does an `API Integration` object store?

**Answers:**

* The cloud platform provider.
* Allowed (and optionally blocked) endpoints and resources on those proxy services.
* The type of proxy service.
* The identifier and access credentials for a cloud platform role with sufficient privileges to use the proxy service.
* All of the above. (Your answer is correct)

**Overall explanation:**

**Answer:** `E. All of the above.`

An *integration* is a Snowflake object that provides an interface between Snowflake and third-party services. An API integration stores information, such as security information, that is needed to work with a proxy service or remote service.

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/create-api-integration

### Question 20

Which feature provides the capability to define an alternate cluster key for a table with an existing cluster key?

**Answers:**

* Result cache
* External table
* Search optimization
* Materialized view (Your answer is correct)

**Overall explanation:**

The correct answer is: **D. Materialized view**

**Explanation:**

**Resources:**

* https://docs.snowflake.com/en/user-guide/views-materialized#materialized-views-and-clustering

### Question 21

Which command allows us to update the schedule of a task?

**Answers:**

* `ALTER TASK SET SCHEDULE` (Your answer is correct)
* `ALTER TASK SET FIXED_TIME`
* `ALTER TASK SET CRON`
* `UPDATE TASK SET SCHEDULE`

**Overall explanation:**

**The correct answer is:** `A. ALTER TASK SET SCHEDULE`

**Explanation:**

In Snowflake, the ALTER TASK command is used to modify the definition of a task. The SET SCHEDULE clause is used to change the schedule of a task.

**Incorrect options:**

**B. ALTER TASK SET FIXED_TIME**

This is incorrect. There is no SET FIXED_TIME clause in the ALTER TASK command in Snowflake.

**C. ALTER TASK SET CRON**

This is incorrect. While the SET SCHEDULE clause of the ALTER TASK command does accept a cron expression to define the schedule, the clause is not called SET CRON.

**D. UPDATE TASK SET SCHEDULE**

This is incorrect. In Snowflake, tasks are modified using the ALTER TASK command, not the UPDATE command.

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/alter-task

### Question 22

Which function can we use to list all the object references of a view?

**Answers:**

* GET_VIEW_REFERENCES
* GET_REFERENCES
* GET_OBJECT_REFERENCES (Correct answer)
* SHOW_OBJECT_REFERENCES (Your answer is incorrect)

**Overall explanation:**

The correct answer is: **C. GET_OBJECT_REFERENCES**

**Explanation:**

The `GET_OBJECT_REFERENCES` function in Snowflake serves the purpose of identifying dependencies within your data schema. It returns a result set that lists the objects referenced by a specified table or view. This helps in managing dependencies and understanding potential impacts when modifying objects.

**Resources:**

* https://docs.snowflake.com/en/sql-reference/functions/get_object_references

### Question 23

What are the possible scaling policies in a multi-cluster warehouse?

**Answers:**

* Standard (Your selection is correct)
* Performance (Your selection is incorrect)
* Snowpark-optimized (Your selection is incorrect)
* Economy (Your selection is correct)

**Overall explanation:**

**Answer:** `A and D`

**Resources:**

* https://docs.snowflake.com/en/user-guide/warehouses-multicluster#setting-the-scaling-policy-for-a-multi-cluster-warehouse

### Question 24

What is true about Sequences? (Select 2)

**Answers:**

* They are schema level objects. (Your selection is correct)
* They are guaranteed to be gap-free.
* The default value for START and INCREMENT are both 1. (Your selection is correct)
* Changing the sequence interval from positive to negative (e.g. from `1` to `-1`), or vice versa doesn't result in duplicates.

**Overall explanation:**

**The correct answers are:** `A and C`

**Explanation:**

**Incorrect options:**

**C. They are guaranteed to be gap-free.**

This is **incorrect**. Sequences in Snowflake are not guaranteed to be gap-free. Gaps can occur if a transaction that consumes a sequence number is rolled back, or if the system crashes. Snowflake does not guarantee generating sequence numbers without gaps. The generated numbers are not necessarily contiguous.

**D. Changing the sequence interval from positive to negative (e.g. from 1 to -1), or vice versa doesn't result in duplicates.**

This is **incorrect**. Changing the sequence interval from positive to negative, or vice versa, can result in duplicates. This is because the sequence generator does not keep track of previously generated values.

**Resources:**

* https://docs.snowflake.com/en/user-guide/querying-sequences

### Question 25

The Cloud Service Layer is not responsible for \_\_\_\_\_ ?

**Answers:**

* Metadata management
* Authentication
* Query Optimization
* Query execution (Your answer is correct)

**Overall explanation:**

The Cloud Service Layer in Snowflake is not responsible for **D. Query execution**.

Here's why the other options are responsibilities of the Cloud Service Layer:

* **A. Metadata management:** The Cloud Service Layer manages information about all data objects in Snowflake, including tables, schemas, and users.
* **B. Authentication:** It handles user authentication and authorization, ensuring only authorized users can access data.
* **C. Query optimization:** The Cloud Service Layer optimizes SQL queries before sending them to the compute layer for execution.
* **D. Query execution:** The Compute Layer in Snowflake is responsible for executing queries on the data stored in the database storage layer.

**Resources:**

* https://docs.snowflake.com/en/user-guide/intro-key-concepts

### Question 26

What sections can be part of a Snowflake Scripting block? (Select 4)

**Answers:**

* EXCEPTION (Your selection is correct)
* BEGIN (Your selection is correct)
* VARIABLES
* END (Your selection is correct)
* START
* DECLARE (Your selection is correct)

**Overall explanation:**

**Answer:** `A, B, D and F`

**Explanation:**

**DECLARE:** This optional section allows you to declare variables, cursors, RESULTSETs, and exceptions for use within the block.

**BEGIN:** This mandatory section marks the start of the executable code within the block. SQL statements and Snowflake Scripting constructs are placed here.

**END:** This mandatory section marks the end of the executable code within the block.

**EXCEPTION:** This optional section allows you to define error handling logic using `RAISE` statements to handle exceptions that might occur during script execution.

Here's a breakdown of the incorrect options:

* **VARIABLES:** While variables are declared within the `DECLARE` section, "VARIABLES" itself is not a separate section.
* **START:** Snowflake Scripting blocks do not have a `START` section.

**Resources:**

* https://docs.snowflake.com/en/developer-guide/snowflake-scripting/blocks

### Question 27

Which statements about **Fail-Safe** are `**True**`? (Select three)

**Answers:**

* Fail Safe is non-configurable (Correct selection)
* There are 0 days of Fail Safe for Transient Tables. (Correct selection)
* Fail Safe adds to the Data Storage cost. (Your selection is correct)
* There is 1 day of Fail Safe for Transient Tables.
* Fail Safe can be used to query data after the retention period of time travel has ended. (Your selection is incorrect)
* Fail Safe is a disaster recovery method that can only recover data by contacting the account admin. (Your selection is incorrect)

**Overall explanation:**

**Correct Answer:** `A,B and C`

**Correct Answers (3):**

* **A. Fail Safe is non-configurable:** Fail-safe provides a (**non-configurable**) 7-day period during which historical data may be recoverable by Snowflake. This period starts immediately after the Time Travel retention period ends. Note, however, that a long-running Time Travel query will delay moving any data and objects (tables, schemas, and databases) in the account into Fail-safe, until the query completes.
* **B. There are 0 days of Fail Safe for Transient Tables:** This statement is True.
* **Fail Safe adds to the Data Storage cost:** This statement is True. The data stored for Fail Safe does count towards your data storage costs. It's a separate, internal backup mechanism maintained by Snowflake at their end.

**Incorrect Answers and Explanations:**

* **D. There is 1 day of Fail Safe for Transient Tables:** As explained earlier, both permanent and transient tables have the same 7-day Fail Safe window.
* **E. Fail Safe can be used to query data after the retention period of time travel has ended:** This statement is false. Fail Safe is not intended for routine access to historical data. It's a recovery mechanism for potentially restoring lost or corrupted data with Snowflake's assistance, not for querying historical data after the Time Travel window has passed.
* **F. Fail Safe is a disaster recovery method that can only be used to recover data by contacting the account admin.** This statement is also False. Snowflake support team needs to be contacted not account admins.

**Resources:**

* https://docs.snowflake.com/en/user-guide/data-failsafe
* https://docs.snowflake.com/en/user-guide/data-cdp-storage-costs#temporary-and-transient-tables
* https://community.snowflake.com/s/article/Fail-safe-data-recovery-steps

### Question 28

What is the default behavior of the `ON_ERROR` option in Snowflake COPY command **for bulk loading**?

**Answers:**

* CONTINUE
* ABORT_TRANSACTION (Your answer is incorrect)
* ABORT_STATEMENT (Correct answer)
* SKIP_FILE

**Overall explanation:**

**Correct Answer:** `C. ABORT_STATEMENT`

**Explanation:**

**Additional Considerations:**

* You can explicitly define the behavior of `ON_ERROR` within the `COPY` statement using any of the following options:
    * `CONTINUE`: Continue loading data, skipping rows with errors.
    * `ABORT_STATEMENT`: The default behavior, aborting the entire statement.
    * `SKIP_FILE`: Write error details to a designated file.

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/copy-into-table

### Question 29

A resource monitor on a warehouse has defined the action “**Notify and Suspend**” when **80%** of the credit quota is reached. What happens when this 80% of the credit quota is reached and the relevant warehouse is currently executing a query?

**Answers:**

* The query will be aborted and the warehouse will be shut down. (Your answer is incorrect)
* The warehouse immediately shuts down and the query will be completed by the cloud service layer.
* The query will be processed by the warehouse and then the warehouse shuts down. (Correct answer)

**Overall explanation:**

**Answer:** `C. The query will be processed by the warehouse and then the warehouse shuts down.`

**Resources:**

* https://docs.snowflake.com/en/user-guide/resource-monitors

### Question 30

What is the behavior of the `VALIDATION_MODE` parameter set to `RETURN_n_ROWS` in the `COPY` command?

**Answers:**

* To load all rows and log any validation errors in the first n rows.
* Validate the first n rows and return them if no error occurs, otherwise return the first error. (Your answer is correct)
* To abort the COPY command if any validation errors occur in the first n rows.
* To skip loading n rows that fail validation checks.

**Overall explanation:**

**Correct Answer:** `B. Validate the first n rows and return them if no error occurs, otherwise return the first error.`

**Explanation:**

When you use `VALIDATION_MODE=RETURN_n_ROWS` in the `COPY` command, Snowflake performs the following actions:

1. It validates the specified number of rows (n) from the source data file.
2. **If no validation errors are encountered in those n rows:**
   * All n rows are returned as output, indicating successful validation.
3. **If any validation errors occur within the n rows:**
   * The COPY command stops processing.
   * The first encountered error message is returned.

This behavior is ideal for scenarios where you want to quickly check the initial portion of the data for potential issues before proceeding with a potentially time-consuming full load.

**Resources:**

* https://docs.snowflake.com/en/sql-reference/sql/copy-into-table#optional-parameters

### Question 31

How are Snowpipe charges calculated?

**Answers:**

* Per-second/per Warehouse size (Your answer is incorrect)
* Per-second/per-core granularity (Correct answer)
* Number of Pipes in account
* Total storage bucket size

**Overall explanation:**

**Correct Answer:** `B. Per-second/per-core granularity`

**Explanation:**

**Incorrect Answers and Explanations:**

* **A. Per-second/per Warehouse size:** While Snowflake does have virtual warehouses used for interactive queries and other operations, Snowpipe itself doesn't use warehouses for billing purposes.
* **C. Number of Pipes in account:** The number of Snowpipes in your account doesn't directly impact billing. You're charged for the compute resources used by each active Snowpipe during data loading.
* **D. Total storage bucket size:** Storage charges are separate from Snowpipe compute usage. You're billed based on the amount of data stored in your Snowflake stages and tables.

**Resources:**

* https://docs.snowflake.com/en/user-guide/data-load-snowpipe-billing#resource-consumption-and-management-overhead

### Question 32

A virtual warehouse was started, used for 45 seconds, and shut down after that. The customer will be charged for how many seconds?

**Answers:**

* 315 seconds
* 45 seconds
* 60 seconds (Your answer is correct)
* 3600 seconds

**Overall explanation:**

The answer is: `C. 60 seconds`

**Explanation:**

Snowflake uses a minimum billing duration of 60 seconds for virtual warehouses, even if the actual usage is less. This is because Snowflake incurs some overhead associated with starting and stopping warehouses, and they want to ensure a minimum level of compensation for those resources.

### Question 33

In Snowsight (Snowflake web user interface), you can execute only one query at a given time (True/False)

**Answers:**

* False (Your answer is correct)
* True

**Overall explanation:**

**Answer:** `False`

**Resources:**

* https://docs.snowflake.com/en/user-guide/ui-snowsight-query

### Question 34

Multi-factor authentication can be enabled for which of the following? (Select three)

**Answers:**

* JDBC (Your selection is correct)
* Snowpipe
* Snowflake WebUI (Your selection is correct)
* SnowSQL (Your selection is correct)

**Overall explanation:**

**Answer:** `A, C and D`

Snowflake supports multi-factor authentication (i.e. MFA) to provide increased login security for users connecting to Snowflake. MFA support is provided as an integrated Snowflake feature, powered by the [Duo Security](http://www.duosecurity.com) service, which is managed completely by Snowflake.

**Resources:**

* https://docs.snowflake.com/en/user-guide/security-mfa