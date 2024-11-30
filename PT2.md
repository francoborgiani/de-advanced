# Practice Test 2 - Results

## Attempt 1

### Question 1

Database `xyz` has the `data_retention_time_in_days` parameter set to `7 days` and table `XYZ.public.ABC` has the `data_retention_time_in_days` set to `10 days`. A Developer accidentally dropped the database containing this single table `8 days ago` and just discovered the mistake. How can the table be recovered?

**Answers**

A. undrop database xyz;

B. create table abc_restore as select \* from xyz.public.abc at (offset => -60\*60\*24\*8);

C. create table abc_restore clone xyz.public.abc at (offset => -3600\*24\*8)

D. Create a Snowflake Support case to restore the database and table from Fail-safe.

**Correct Answer**

D

**Overall Explanation**

Recovery Option: `D. Create a Snowflake Support case to restore the database and table from Fail-safe`.

Explanation:
(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_06-29-02-5d815d7dd3f233322143f362556c0719.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/data-time-travel#dropped-containers-and-object-retention-inheritance
* https://docs.snowflake.com/en/user-guide/data-failsafe

### Question 2

A Data Engineer would like to define a file structure for loading and unloading data. Where can the file structure be defined? **(Choose three)**

**Answers**

A. COPY command

B. MERGE command

C. FILE FORMAT object

D. PIPE object

E. STAGE object

F. insert command

**Correct Answer**

A, C and E

**Overall Explanation**

The correct answers are: `A, C and E`

Explanation:
(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_06-47-37-b2d2fddf08b8987d51ee65ebe6a72e43.png)

*A. Correct* - The COPY command in Snowflake can be used to define a file structure for loading data. It allows you to specify the file format, field delimiter, error handling, and other options.

*B. Incorrect* - The MERGE command in Snowflake is used to perform UPSERT operations (a combination of UPDATE and INSERT). It does not allow you to define a file structure.

*C. Correct* - The FILE FORMAT object in Snowflake allows you to define a named file format that can be used for loading and unloading data. It includes options for specifying the type of file, field delimiter, date format, error handling, and more.

*D. Incorrect* - The PIPE object in Snowflake is used for continuous data loading using Snowpipe. While it does use a FILE FORMAT object, it does not itself allow you to define a file structure.

*E. Correct* - The STAGE object in Snowflake can be used to define a file structure for unloading data. When you create a stage, you can specify a file format that defines the structure of the unloaded data.

*F. Incorrect* - The INSERT command in Snowflake is used to insert rows into a table. It does not allow you to define a file structure.

**Resources**

* https://docs.snowflake.com/en/user-guide/data-unload-prepare

### Question 3

Which Snowflake feature facilitates access to external API services such as geocoders, data transformation, machine learning models, and other custom code?

**Answers**

A. Security integration

B. External tables

C. External functions

D. Java User-Defined Functions (UDFs)

**Correct Answer**

C

**Overall Explanation**

The correct option for accessing external API services in Snowflake is: `C. External functions`

Explanation:

* External functions are a powerful feature in Snowflake that allows you to call code that resides outside of Snowflake's environment. This code could be written in various languages like Python, Scala, or Java and can perform tasks such as:
    * Geocoding addresses
    * Transforming data
    * Utilizing machine learning models
    * Interacting with custom code running on external servers

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_06-50-51-0b42fd1584b5462a079a077e47d49e23.png)

By creating an external function, you define the parameters it takes and the data type it returns. You then specify the URL of a proxy service that interacts with the external code and relays data between Snowflake and the external service.

**Incorrect Options and Explanations:**

* **A. Security integration:** While security integration is crucial for managing access to Snowflake resources, it doesn't directly facilitate accessing external APIs.

* **B. External tables:** External tables allow you to query data residing in external data warehouses or databases, but not to execute external code.

* **D. Java User-Defined Functions (UDFs):** While Snowflake supports UDFs written in Java, they are user-defined functions that execute within Snowflake, not external APIs.

**Resources**

* https://docs.snowflake.com/en/sql-reference/external-functions

### Question 4

Which system role is recommended for a custom role hierarchy to be ultimately assigned to?

**Answers**

A. ACCOUNTADMIN

B. SECURITYADMIN

C. SYSADMIN

D. USERADMIN

**Correct Answer**

C

**Overall Explanation**

The recommended system role for the top level of a custom role hierarchy in Snowflake is: `C. SYSADMIN`

Explanation:

* SYSADMIN is the most privileged system role in Snowflake. It grants the ability to manage all aspects of the account, including:

    * Creating and managing users and roles
    * Creating and managing databases and schemas
    * Configuring warehouses and virtual warehouses
    * Granting and revoking privileges

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_06-56-48-f2813fb616587c85bfa3358bd21c2506.png)

By assigning the top-level custom role to SYSADMIN, you ensure that all roles within the hierarchy inherit the necessary permissions to manage objects within the Snowflake account.
(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_06-30-48-5ce6eeea298663ead9fa62ff7b358b8a.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/security-access-control-overview#custom-roles

### Question 5

A company is using Snowpipe to bring in millions of rows every day of Change Data Capture (CDC) into a Snowflake staging table on a real-time basis. The CDC needs to get processed and combined with other data in Snowflake and land in a final table as part of the full data pipeline. How can a Data Engineer MOST efficiently process the incoming CDC on an ongoing basis?

**Answers**

A. Create a stream on the staging table and schedule a task that transforms data from the stream, only when the stream has data.

B. Transform the data during the data load with Snowpipe by modifying the related COPY INTO statement to include transformation steps such as CASE statements and JOINS.

C. Schedule a task that dynamically retrieves the last time the task was run from information_schema.task_history and use that timestamp to process the delta of the new rows since the last time the task was run.

D. Use a CREATE OR REPLACE TABLE AS statement that references the staging table and includes all the transformation SQL. Use a task to run the full CREATE OR REPLACE TABLE AS statement on a scheduled basis.

**Correct Answer**

A

**Overall Explanation**

The most efficient approach for processing the incoming CDC data in Snowflake on an ongoing basis is: `A. Create a stream on the staging table and schedule a task that transforms data from the stream, only when the stream has data`.

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_08-41-02-84829ffdd9ef93bcde1f10b5275bf07e.png)

Explanation:
(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_

### Question 5

A company is using Snowpipe to bring in millions of rows every day of Change Data Capture (CDC) into a Snowflake staging table on a real-time basis. The CDC needs to get processed and combined with other data in Snowflake and land in a final table as part of the full data pipeline. How can a Data Engineer MOST efficiently process the incoming CDC on an ongoing basis?

**Answers**

A. Create a stream on the staging table and schedule a task that transforms data from the stream, only when the stream has data.

B. Transform the data during the data load with Snowpipe by modifying the related COPY INTO statement to include transformation steps such as CASE statements and JOINS.

C. Schedule a task that dynamically retrieves the last time the task was run from information_schema.task_history and use that timestamp to process the delta of the new rows since the last time the task was run.

D. Use a CREATE OR REPLACE TABLE AS statement that references the staging table and includes all the transformation SQL. Use a task to run the full CREATE OR REPLACE TABLE AS statement on a scheduled basis.

**Correct Answer**

A

**Overall Explanation**

The most efficient approach for processing the incoming CDC data in Snowflake on an ongoing basis is: `A. Create a stream on the staging table and schedule a task that transforms data from the stream, only when the stream has data`.

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_08-41-02-84829ffdd9ef93bcde1f10b5275bf07e.png)

Explanation:
(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_06-32-47-e8590505e7401fedac3bfb98b32bfac2.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/tasks-intro
* https://docs.snowflake.com/en/user-guide/streams

### Question 6

What are characteristics of Snowpark Python packages? **(Choose three)**

**Answers**

A. Third-party packages can be registered as a dependency to the Snowpark session using the session.import() method.

B. Python packages can access any external endpoints.

C. Python packages can only be loaded in a local environment

D. Third-party supported Python packages are locked down to prevent hitting.

E. The SQL command DESCRIBE FUNCTION will list the imported Python packages of the Python User-Defined Function (UDF).

F. Querying information_schema.packages will provide a list of supported Python packages and versions.

**Correct Answer**

A, E and F

**Overall Explanation**

Correct Options:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_06-34-13-043e1ee249a5c25a27c62fac0166d89d.png)

Incorrect Options and Explanations:

* **B. Python packages can access any external endpoints.**

    * While Snowpark provides capabilities for making requests to external APIs, there might be restrictions on outbound network access depending on your Snowflake account configuration. It's essential to consult your administrator and security policies.

* **C. Python packages can only be loaded in a local environment.**

    * Snowpark Python packages are designed to be used within Snowflake. You can install and manage them in a virtual environment or Snowflake's environment. Local environments are typically used for development purposes, but execution happens within Snowflake.

* **D. Third-party supported Python packages are locked down to prevent hitting.**

    * Snowflake does manage versions of supported third-party packages, but this primarily ensures compatibility and stability. You can still encounter errors or resource exhaustion limits if your code utilizes packages in an inefficient manner.

**Resources**

* https://docs.snowflake.com/en/release-notes/bcr-bundles/2023_04/bcr-1094
* https://docs.snowflake.com/en/sql-reference/sql/desc-function
* https://pypi.org/project/snowflake-snowpark-python/

### Question 7

A Data Engineer wants to centralize grant management to maximize security. A user needs ownership on a table in a new schema. However, this user should not have the ability to make grant decisions. What is the correct way to do this?

**Answers**

A. Grant OWNERSHIP to the user on the table.

B. Revoke grant decisions from the user on the table.

C. Revoke grant decisions from the user on the schema.

D. Add the WITH MANAGED ACCESS parameter on the schema.

**Correct Answer**

D

**Overall Explanation**

The correct way to centralize grant management and provide OWNERSHIP to a user on a table without granting them the ability to make grant decisions is: `D. Add the WITH MANAGED ACCESS parameter on the schema`.

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_09-01-46-34072d6029404f234749498ecf8f4682.png)

Explanation:

* WITH MANAGED ACCESS is a powerful feature in Snowflake that allows you to restrict grant capabilities within a schema. With this parameter enabled on a schema, users with OWNERSHIP on objects within that schema cannot grant any privileges on those objects.

Here's a breakdown of the other options and why they're not recommended:

* **A. Grant OWNERSHIP to the user on the table:** This would allow the user to not only own the table but potentially grant access to others, which contradicts the goal of centralized control.

* **B. Revoke grant decisions from the user on the table:** There's no specific privilege for "grant decisions" on individual tables. OWNERSHIP inherently includes the ability to grant access on that specific object.

* **C. Revoke grant decisions from the user on the schema:** While this might seem logical, revoking grant decisions at the schema level isn't possible in Snowflake. OWNERSHIP on objects within the schema would still allow granting privileges on those objects.

**Resources**

* https://docs.snowflake.com/en/user-guide/security-access-control-configure

### Question 8

What kind of Snowflake integration is required when defining an external function in Snowflake?

**Answers**

A. API integration

B. HTTP integration

C. Notification integration

D. Security integration

**Correct Answer**

A

**Overall Explanation**

The correct Snowflake integration type required when defining an external function is: `API integration`.

(Image: https://docs.snowflake.com/en/_images/external-functions-overview-07.png)
(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_06-39-08-93d0f9ea1f5abf67d39c31b0c3fb73a8.png)

**Resources**

* https://docs.snowflake.com/en/sql-reference/external-functions-introduction

### Question 9

What is a characteristic of the operations of streams in Snowflake?

**Answers**

A. Whenever a stream is queried, the offset is automatically advanced.

B. When a stream is used to update a target table, the offset is advanced to the current time.

C. Querying a stream returns all change records and table rows from the current offset to the current time.

D. Each committed and uncommitted transaction on the source table automatically puts a change record in the stream

**Correct Answer**

B

**Overall Explanation**

Correct Answer: `B. When a stream is used to update a target table, the offset is advanced to the current time.`

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_09-15-04-47ac327aa175ba11803ed933d992e66e.png)

Explanation on incorrect Options:

### Question 10

What is a characteristic of the use of binding variables in JavaScript stored procedures in Snowflake?

**Answers**

A. All types of JavaScript variables can be bound.

B. All Snowflake first-class objects can be bound.

C. Only JavaScript variables of type number, string, and SfDate can be bound.

D. Users are restricted from binding JavaScript variables because they create SQL injection attack vulnerabilities.

**Correct Answer**

C

**Overall Explanation**

The correct answer is: `C. Only JavaScript variables of type number, string, and SfDate can be bound.`

Explanation:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_09-20-00-f55a335a676bd6ba93a7d177590212a7.png)

*A. Incorrect* - Not all types of JavaScript variables can be bound in Snowflake. Only certain types are supported.

*B. Incorrect* - Not all Snowflake first-class objects can be bound. Binding is limited to certain types of JavaScript variables.

*C. Correct* - Only JavaScript variables of type number, string, and SfDate can be bound in Snowflake. These types correspond to the Snowflake data types NUMBER, STRING, and TIMESTAMP_LTZ respectively.

*D. Incorrect* - Users are not restricted from binding JavaScript variables because they create SQL injection attack vulnerabilities. In fact, using binding variables can help prevent SQL injection attacks because they ensure that data is properly escaped.

**Resources**

* https://docs.snowflake.com/en/developer-guide/stored-procedure/stored-procedures-javascript#binding-variables

### Question 10

What is a characteristic of the use of binding variables in JavaScript stored procedures in Snowflake?

**Answers**

A. All types of JavaScript variables can be bound.

B. All Snowflake first-class objects can be bound.

C. Only JavaScript variables of type number, string, and SfDate can be bound.

D. Users are restricted from binding JavaScript variables because they create SQL injection attack vulnerabilities.

**Correct Answer**

C

**Overall Explanation**

The correct answer is: `C. Only JavaScript variables of type number, string, and SfDate can be bound.`

Explanation:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_09-20-00-f55a335a676bd6ba93a7d177590212a7.png)

*A. Incorrect* - Not all types of JavaScript variables can be bound in Snowflake. Only certain types are supported.

*B. Incorrect* - Not all Snowflake first-class objects can be bound. Binding is limited to certain types of JavaScript variables.

*C. Correct* - Only JavaScript variables of type number, string, and SfDate can be bound in Snowflake. These types correspond to the Snowflake data types NUMBER, STRING, and TIMESTAMP_LTZ respectively.

*D. Incorrect* - Users are not restricted from binding JavaScript variables because they create SQL injection attack vulnerabilities. In fact, using binding variables can help prevent SQL injection attacks because they ensure that data is properly escaped.

**Resources**

* https://docs.snowflake.com/en/developer-guide/stored-procedure/stored-procedures-javascript#binding-variables

### Question 11

Assuming a Data Engineer has all appropriate privileges and context, which statements would be used to assess whether the User-Defined Function (UDF)  named `BINNY_UDEMY.SALES.REVENUE_BY_REGION` exists and is secure? **(Choose two)**

**Answers**

A. SHOW USER FUNCTIONS LIKE 'REVENUE_BY_REGION' IN SCHEMA SALES;

B. SELECT IS_SECURE FROM SNOWFLAKE.INFORMATION_SCHEMA.FUNCTIONS WHERE FUNCTION_SCHEMA = 'SALES' AND FUNCTION_NAME = 'REVENUE_BY_REGION';

C. SELECT IS_SECURE FROM INFORMATION_SCHEMA.FUNCTIONS WHERE FUNCTION_SCHEMA = 'SALES' AND FUNCTION_NAME = 'REVENUE_BY_REGION';

D. SHOW EXTERNAL FUNCTIONS LIKE 'REVENUE_BY_REGION' IN SCHEMA SALES;

E. SHOW SECURE FUNCTIONS LIKE 'REVENUE_BY_REGION' IN SCHEMA SALES;

**Correct Answer**

A and C

**Overall Explanation**

The two correct statements to assess whether the UDF exists and is secure are: `A and C`

Here's a breakdown of each option and why it's correct or incorrect:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_06-40-42-fd2a2affc7e4f28f33bb30bdf2cab3e9.png)

Incorrect Options:

*B. SELECT IS_SECURE FROM SNOWFLAKE.INFORMATION_SCHEMA.FUNCTIONS WHERE FUNCTION_SCHEMA = 'SALES' AND FUNCTION_NAME = 'REVENUE_BY_REGION';: This statement uses the correct view but might require omitting the `SNOWFLAKE.` prefix depending on the Snowflake version. Omitting the prefix is generally recommended.

*D. SHOW EXTERNAL FUNCTIONS LIKE 'REVENUE_BY_REGION' IN SCHEMA SALES;: This command is for external functions, which reside outside of Snowflake. The UDF in question seems to be a user-defined function within Snowflake.

*E. SHOW SECURE FUNCTIONS LIKE 'REVENUE_BY_REGION' IN SCHEMA SALES;: While Snowflake can define secure UDFs, there's no specific `SHOW SECURE FUNCTIONS` command. You can use `SHOW USER FUNCTIONS` combined with `IS_SECURE` from the `INFORMATION_SCHEMA.FUNCTIONS` view for verification.

**Resources**

* https://docs.snowflake.com/en/sql-reference/sql/show-user-functions
* https://docs.snowflake.com/en/sql-reference/info-schema/functions

### Question 12

A Data Engineer is working on a continuous data pipeline which receives data from Amazon Kinesis Firehose and loads the data into a staging table which will later be used in the data transformation process. The average file size is 400-500 MB. The Engineer needs to ensure that Snowpipe is performant while minimizing costs. How can this be achieved?

**Answers**

A. Increase the size of the virtual warehouse used by Snowpipe.

B. Split the files before loading them and set the SIZE_LIMIT option to 250 MB.

C. Change the file compression size and increase the frequency of the Snowpipe loads.

D. Decrease the buffer size to trigger delivery of files sized between 100 to 250 MB in Kinesis Firehose

**Correct Answer**

D

**Overall Explanation**

The correct answer is: `D. Decrease the buffer size to trigger delivery of files sized between 100 to 250 MB in Kinesis Firehose`

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_09-40-19-949787487ee432f2f89c75cf2ba68cf3.png)

Explanation:

*A. Incorrect* - Increasing the size of the virtual warehouse used by Snowpipe may increase performance, but it will also increase costs. This does not meet the requirement to minimize costs.

*B. Incorrect* - Splitting the files before loading them and setting the SIZE_LIMIT option to 250 MB may improve performance, but it will also increase costs due to the additional processing required to split the files.

*C. Incorrect* - Changing the file compression size and increasing the frequency of the Snowpipe loads may improve performance, but it will also increase costs due to the additional processing and storage required.

*D. Correct* - Decreasing the buffer size to trigger delivery of files sized between 100 to 250 MB in Kinesis Firehose can improve Snowpipe performance by reducing the size of the files that need to be loaded. This can also help to minimize costs by reducing the amount of data that needs to be processed and stored.

**Resources**

* https://docs.snowflake.com/en/user-guide/data-load-considerations-prepare#continuous-data-loads-i-e-snowpipe-and-file-sizing

### Question 13

Company A and Company B both have Snowflake accounts. Company A's account is hosted on a different cloud provider and region than Company B's account. Companies A and B are not in the same Snowflake organization. How can Company A share data with Company B? **(Choose two)**

**Answers**

A. Create a share within Company A's account and add Company B's account as a recipient of that share.

B. Create a share within Company A's account, and create a reader account that is a recipient of the share. Grant Company B access to the reader account.

C. Use database replication to replicate Company A's data into Company B's account. Create a share within Company B's account and grant users within Company B's account access to the share.

D. Use database replication to replicate Company A's data into Company B's account. Create a share within Company B's account and grant users within Company B's account access to the share.

E. Create a separate database within Company A's account to contain only those data sets they wish to share with Company B. Create a share within Company A's account and add all the objects within this separate database to the share. Add Company B's account as a recipient of the share.

**Correct Answer**

A and B

**Overall Explanation**

The correct answers are: `A and B`

Explanation:

*A. Correct* - Snowflake allows secure data sharing across different accounts, even if they are hosted on different cloud providers or regions. Company A can create a share within their account and add Company B's account as a recipient of that share.

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_09-58-45-0e8b015cea2ac884af8843cd33335f6f.png)

*B. Correct* - Creating a reader account is another way to share data between two Snowflake accounts. Company A can create a share within their account, create a reader account that is a recipient of the share, and then grant Company B access to the reader account.

*C. Incorrect* - Database replication is used to create a copy of a database in the same or different Snowflake account. However, it is not necessary for sharing data between

### Question 14

Which functions will compute a 'fingerprint' over an entire table, query result, or window to quickly detect changes to table contents or query results? **(Choose two)**

**Answers**

A. HASH(*)

B. HASH_AGG(*)

C. HASH_AGG(<expr>, <expr>)

D. HASH_AGG_COMPARE(*)

E. HASH_COMPARE(*)

**Correct Answer**

B and C

**Overall Explanation**

The correct functions that compute a "fingerprint" over data in Snowflake are: `B. HASH_AGG(*) and C. HASH_AGG(<expr>, <expr>)`.

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_06-42-19-25998394804f30748172b9b14589e1bf.png)

Incorrect Options and Explanations:

* **A. HASH(*):** While Snowflake might support `HASH` for some specific data types, it doesn't have a general `HASH` function for computing a fingerprint over the entire table.

* **D. HASH_AGG_COMPARE(*):** There's no built-in function named `HASH_AGG_COMPARE` in Snowflake. You would likely need to compare the results of two separate `HASH_AGG` calls to determine changes.

* **E. HASH_COMPARE(*):** Similar to `HASH_AGG_COMPARE`, Snowflake doesn't have a built-in `HASH_COMPARE` function. You might need to compare hash values from `HASH_AGG` for change detection.

**Resources**

* https://docs.snowflake.com/en/sql-reference/functions/hash_agg

### Question 15

The following chart represents the performance of a virtual warehouse over time:

(Image: https://img.examtopics.com/snowpro-advanced-data-engineer/image22.png)

A Data Engineer notices that the warehouse is queueing queries. The warehouse is size X-Small, the minimum and maximum cluster counts are set to 1, the scaling policy is set to standard, and auto-suspend is set to 20 minutes. How can the performance be improved?

**Answers**

A. Change the cluster settings.

B. Increase the size of the warehouse.

C. Change the scaling policy to economy.

D. Change auto-suspend to a longer time frame

**Correct Answer**

B

**Overall Explanation**

Correct Answer:  `B. Increase the size of the warehouse` is the most effective way to improve performance.

Here's a breakdown of the reasoning and why other options are not ideal:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-07-29_04-01-26-bdc23032a0431fca700ed65e28fd4a42.png)
(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_06-43-42-fd5c015207169813d55523faa92c372b.png)

Other Options and Considerations:

* **A. Change the cluster settings:** While cluster settings can influence scaling behavior, directly increasing the warehouse size provides a more substantial boost in resources.
Dont't confuse it with warehouse settings. The settings like converting to multi-cluster are set at warehouse level not via cluster settings.

* **C. Change the scaling policy to economy:** The economy policy prioritizes cost savings over performance.
It might delay query execution and worsen queueing.

* **D. Change auto-suspend to a longer time frame:**
This might save costs during idle periods, but it won't address the current performance bottleneck.
Consider adjusting auto-suspend after increasing the warehouse size if queueing persists

**Resources**

* https://community.snowflake.com/s/article/Understanding-Queuing
* https://docs.snowflake.com/en/user-guide/performance-query-warehouse-size

### Question 16

What is a characteristic of the use of external tokenization?

**Answers**

A. Secure data sharing can be used with external tokenization.

B. External tokenization cannot be used with database replication.

C. Pre-loading of unmasked data is supported with external tokenization

D. External tokenization allows the preservation of analytical values after de-identification.

**Correct Answer**

D

**Overall Explanation**

The correct option is: `D. External tokenization allows the preservation of analytical values after de-identification.`

Explanation: 

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_13-19-19-6cebe32f1b0a3cd95f3701b4d786e7f5.png)
(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_06-46-40-c52d0326fed00c2e9e1e2f54b9661a42.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/security-column-intro

### Question 17

Which Snowflake objects does the Snowflake Kafka connector use? **(Choose three)**

**Answers**

A. Pipe

B. Serverless task

C. Internal user stage

D. Internal table stage

E. Internal named stage

F. Storage integration

**Correct Answer**

A, C and E

**Overall Explanation**

The Snowflake Kafka connector interacts with the following Snowflake objects (Choose three): `A. Internal stage, D. Internal user stage and E. Internal named stage`

The following diagram shows the ingest flow for Kafka with the Kafka connector:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_13-34-12-8d993c696e44fbbb0e3a75cfaee8b07e.png)

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-21-56-6d0356bab51db1f9a8b9ae1031af5d50.png)

One or more applications publish JSON or Avro records to a Kafka cluster.

The records are split into one or more topic partitions.

The Kafka connector buffers messages from the Kafka topics.

When a threshold (time or memory or number of messages) is reached, the connector writes the messages to a temporary file in the internal stage.

The connector triggers Snowpipe to ingest the temporary file.

Snowpipe copies a pointer to the data file into a queue.

A Snowflake-provided virtual warehouse loads data from the staged file into the target table (i.e. the table specified in the configuration file for the topic) via the pipe created for the Kafka topic partition.

(Not shown) The connector monitors Snowpipe and deletes each file in the internal stage after confirming that the file data was loaded into the table.

If a failure prevented the data from loading, the connector moves the file into the table stage and produces an error message.

The connector repeats steps 2-4.

Explanation:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-21-56-4c02002b87811bbd78390690cf987079.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/kafka-connector-overview#workflow-for-the-kafka-connector

### Question 18

A Data Engineer is evaluating the performance of a query in a development environment.

(Image: https://img.examtopics.com/snowpro-advanced-data-engineer/image15.png)

(Image: https://img.examtopics.com/snowpro-advanced-data-engineer/image16.png)

Based on the Query Profile, what are some performance tuning options the Engineer can use? **(Choose two)**

**Answers**

A. Add a LIMIT to the ORDER BY if possible

B. Use a multi-cluster virtual warehouse with the scaling policy set to standard

C. Move the query to a larger virtual warehouse

D. Create indexes to ensure sorted access to data

E. Increase the MAX_CLUSTER_COUNT

**Correct Answer**

A and C

**Overall Explanation**

Answer: `A && C`

Explanation:

* Snowflake don't support the create of index, We can cluster a table by a cluster key, but this option is not in the list of option.
 

* In addition to this in the question is write that the engineer is in DEV environment.
So we may not need to have all of the data and can use limit to decrease the data to be scanned.

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-02_14-11-09-2cedb471c4867aba5953bf47722f5640.png)

**Resources**

* https://docs.snowflake.com/en/user

### Question 19

A stream called `ORDERS_STRM` is created on top of a `ORDERS` table in a continuous pipeline running in Snowflake. After a couple of months, the `ORDERS` table is renamed `ORDERS_RAW` to comply with new naming standards. What will happen to the `ORDERS_STRM` object?

**Answers**

A. `ORDERS_STRM` will keep working as expected.

B. `ORDERS_STRM` will be stale and will need to be re-created.

C. `ORDERS_STRM` will be automatically renamed `ORDERS_RAW_STRM`.

D. Reading from the `ORDERS_STRM` stream will succeed for some time after the expected `STALE_TIME`.

**Correct Answer**

A

**Overall Explanation**

The correct answer is: `A.ORDERS_STRM will keep working as expected.`

Explanation:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-03_06-58-04-3879dc26ede336c5cd44b692d81f9dbf.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/streams-intro

### Question 20

Which output is provided by both the `SYSTEM$CLUSTERING_DEPTH` function and the `SYSTEM$CLUSTERING_INFORMATION` function?

**Answers**

A. average_depth

B. notes

C. average_overlaps

D. total_partition_count

**Correct Answer**

A

**Overall Explanation**

**Answer:** `A. average_depth`

**Explanation:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-27-38-5dba657c9f59ce66b5966f662cb04619.png)

**Resources**

* https://docs.snowflake.com/en/sql-reference/functions/system_clustering_depth
* https://docs.snowflake.com/en/sql-reference/functions/system_clustering_information

### Question 21

A database contains a table and a stored procedure defined as:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question/2024-06-03_06-00-55-78a285385513dd354640774b94df65b8.png)

The `binni_udemy_log_table` is initially empty and a Data Engineer issues the following command:

`sql
CALL insert_log(NULL::VARCHAR);

No other operations are affecting the binni_udemy_log_table. What will be the outcome of the procedure call?
Answers

A. The log_table contains zero records and the stored procedure returned 1 as a return value.

B. The log_table contains one record and the stored procedure returned 1 as a return value

C. The log_table contains one record and the stored procedure returned NULL as a return value

D. The log_table contains zero records and the stored procedure returned NULL as a return value.
`

**Correct Answer**

D

**Overall Explanation**


(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-28-39-eca7fbddb2ca451a40d42ef23b6b9219.png)

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-03_06-00-55-638b94de3f3124e909aba7b39b82f787.png)

**Correct Answer:** `D. The binni_udemy_log_table contains zero records and the stored procedure returned NULL as a return value.`

**Explanation:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-29-37-b18de72743d79d920ab873613ab6e24a.png)

**Resources**

https://docs.snowflake.com/en/sql-reference/sql/create-procedure


* https://docs.snowflake.com/en/user-guide/querying-persisted-results
Correct Answer






### Question 22

A Data Engineer has developed a dashboard that will issue the same SQL select clause to Snowflake every 15 hours. How long will Snowflake use the persisted query results from the result cache, provided that the underlying data has not changed?

**Answers**

A. 12 hours

B. 15 hours

C. 24 hours

D. 14 days

E. 31 days

**Correct Answer**

E

**Overall Explanation**

**Correct Answer:** `E. 31 days`

**Explanation:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-29-37-b18de72743d79d920ab873613ab6e24a.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/querying-persisted-results

### Question 23

The following is returned from `SYSTEM$CLUSTERING_INFORMATION()` for a table named ORDERS with a DATE column named O_ORDERDATE:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question/2024-09-29_07-38-49-dd36d747ef87142fb1103611ffa30f99.png)

What does the total_constant_partition_count value indicate about this table?

**Answers**

A. The table is clustered very well on O_ORDERDATE, as there are 493 micro-partitions that could not be significantly improved by reclustering.

B. The table is not clustered well on O_ORDERDATE, as there are 493 micro-partitions where the range of values in that column overlap with every other micro-partition in the table.

C. The data in O_ORDERDATE does not change very often, as there are 493 micro-partitions containing rows where that column has not been modified since the row was created.

D. The data in O_ORDERDATE has a very low cardinality, as there are 493 micro-partitions where there is only a single distinct value in that column for all rows in the micro-partition

**Correct Answer**

A

**Overall Explanation**

**Answer:** A

**Explanation:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-44-15-a70402fc9e099f31ca25dfc2724620c1.png)

**Explanation of Each Option**

*A. The table is clustered very well on O_ORDERDATE, as there are 493 micro-partitions that could not be significantly improved by reclustering.*

*   Correct: The `total_constant_partition_count` indicates the number of micro-partitions that are already optimally clustered and cannot be improved further by reclustering. In this case, 493 out of 536 micro-partitions are already well-clustered based on the `O_ORDERDATE` column.

*B. The table is not clustered well on O_ORDERDATE, as there are 493 micro-partitions where the range of values in that column overlap with every other micro-partition in the table.*

*   Incorrect: This option misinterprets the meaning of `total_constant_partition_count`. The value actually indicates well-clustered micro-partitions, not poorly clustered ones with overlapping ranges.

*C. The data in O_ORDERDATE does not change very often, as there are 493 micro-partitions containing rows where that column has not been modified since the row was created.*

*   Incorrect: The `total_constant_partition_count` does not provide information about how often the data changes. It only indicates how well the data is clustered.

*D. The data in O_ORDERDATE has very low cardinality, as there are 493 micro-partitions where there is only a single distinct value in that column for all rows in the micro-partition*

*   Incorrect: The `total_constant_partition_count` does not directly indicate the cardinality of the data. It shows how well the data is clustered, not the number of distinct values.

**Resources**

* https://docs.snowflake.com/en/sql-reference/functions/system_clustering_information#usage-notes

### Question 24

What is the purpose of the `BUILD_STAGE_FILE_URL` function in Snowflake?

**Answers**

A. It generates an encrypted URL for accessing a file in a stage.

B. It generates a staged URL for accessing a file in a stage.

C. It generates a permanent URL for accessing files in a stage.

D. It generates a temporary URL for accessing a file in a stage.

**Correct Answer**

C

**Overall Explanation**

**Correct Answer:**  `C. It generates a permanent URL for accessing files in a stage`.

**Explanation:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-03_05-35-54-2abbeacea40b314dd7c320c8a3b1ca96.png)

**Resources**

* https://docs.snowflake.com/en/sql-reference/functions/build_stage_file_url

### Question 25

Which methods can be used to create a DataFrame object in Snowpark? **(Choose three)**

**Answers**

A. session.jdbc_connection()

B. session.read.json()

C. session.table()

D. DataFrame.write()

E. session.builder()

F. session.sql()

**Correct Answer**

B, C and F

**Overall Explanation**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-45-57-5ac73bc07ba5d6b06b70662a48bb9455.png)

Incorrect Options:

*A. session.jdbc_connection()*

*   Explanation: This method's primary purpose is to establish a JDBC connection to an external database system. It doesn't directly create a DataFrame. While you could potentially use the connection object to execute queries on the external database and convert the results into a DataFrame, that would involve additional steps.
*   Reference: https://docs.snowflake.com/en/developer-guide/jdbc/jdbc

*D. DataFrame.write()*

*   Explanation: This method is typically used after creating a DataFrame to write its data to a specific location, such as a table or file. It's not a method for creating DataFrames directly within the `session` object.

*E. session.builder()*

*   Explanation: This method is used to configure and create a Snowpark `Session` object, which serves as the entry point for interacting with Snowflake data and functionalities. While session creation is essential for using other DataFrame creation methods, `session.builder()` itself doesn't directly generate DataFrames.
*   Reference: https://docs.snowflake.com/en/developer-guide/snowpark/python/creating-session

**Resources**

* https://docs.snowflake.com/en/developer-guide/snowpark/reference/python/1.3.0/api/snowflake.snowpark.DataFrame

### Question 26

A Data Engineer wants to create a new development database (`DEV`) as a clone of the permanent production database (`PROD`). There is a requirement to disable Fail-safe for all tables. Which command will meet these requirements?

**Answers**

A. CREATE DATABASE DEV CLONE PROD FAIL_SAFE = FALSE;

B. CREATE DATABASE DEV CLONE PROD FAIL_SAFE = FALSE;

C. CREATE TRANSIENT DATABASE DEV CLONE PROD;

D. CREATE DATABASE DEV CLONE PROD DATA_RETENTION_TIME_IN DAYS = 0;

**Correct Answer**

C

**Overall Explanation**

**Answer:** `C. CREATE TRANSIENT DATABASE DEV CLONE PROD`

**Explanation:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-03_05-25-08-2292d4b746483a930a2036afc9ac8f34.png)

Here's a breakdown of each option and why only Option C fulfills all the requirements:
(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-46-54-707b73242cb3a9159f42f016014a4577.png)

**Resources**

* https://docs.snowflake.com/en/sql-reference/sql/create-database

### Question 27

A large table with 100 columns contains three years of historical data. When queried, the table is filtered on a single day. Below is the Query Profile:

(Image: https://img.examtopics.com/snowpro-advanced-data-engineer/image3.png)

Using a size 2XL virtual warehouse, this query took over an hour to complete. What will improve the query performance the MOST?

**Answers**

A. Increase the size of the virtual warehouse.

B. Increase the number of clusters in the virtual warehouse.

C. Implement the search optimization service on the table.

D. Add a date column as a cluster key on the table

**Correct Answer**

D

**Overall Explanation**

**Answer:** `D`

**Explanation:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-48-05-b6f7f1cea7cc49f64efaa34019d993a4.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/ui-query-profile#inefficient-pruning
* https://docs.snowflake.com/en/user-guide/tables-clustering-key

### Question 28

A Data Engineer executes a complex query and wants to make use of Snowflake’s query results caching capabilities to reuse the results. Which conditions must be met? **(Choose three.)**

**Answers**

A. The results must be reused within 72 hours.

B. The query must be executed using the same virtual warehouse.

C. The USED_CACHED_RESULT parameter must be included in the query.

D. The table structure contributing to the query result cannot have changed.

E. The new query must have the same syntax as the previously executed query

F. The micro-partitions cannot have changed due to changes to other data in the table

**Correct Answer**

D, E and F

**Overall Explanation**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-49-12-81920f999d6222b1e7f2a57c467298fc.png)

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-03_04-41-26-f74d6b7a8954ff774b2efbc5525892af.png)

Incorrect Options:

*A. The results must be reused within 72 hours.*

*   Explanation: The default cache retention period in Snowflake is 24 hours. However, if the same query is re-executed within that timeframe, the clock resets, effectively extending the cache usage up to a maximum of 30 days.

*B. The query must be executed using the same virtual warehouse.*

*   Explanation: Snowflake's result cache is shared across virtual warehouses within an account. As long as the other conditions are met, any virtual warehouse can leverage the cached results.

*C. The USED_CACHED_RESULT parameter must be included in the query.*

*   Explanation: Snowflake automatically determines whether to use cached results based on the conditions mentioned above. There's no need to include a specific parameter to activate result caching.

**Resources**

* https://docs.snowflake.com/en/user-guide/querying-persisted-results

### Question 29

How can the following relational data be transformed into semi-structured data using the least amount of operational overhead?

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question/2024-06-03_04-23-32-d435797a806a3ab777b3b7232f347c6f.png)

**Answers**

A. Use the `TO_JSON` function.

B. Use the `PARSE_JSON` function to produce a `VARIANT` value.

C. Use the `OBJECT_CONSTRUCT` function to return a Snowflake object.

D. Use the `TO_VARIANT` function to convert each of the relational columns to `VARIANT`.

**Correct Answer**

C

**Overall Explanation**

**The correct answer is:** `C. Use the OBJECT_CONSTRUCT function to return a Snowflake object.`

**Explanation:**
(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-50-33-4a0553478301e18e365553d69502aa87.png)

**Example:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-03_04-23-33-20d0d4013a1f64ae7459425b80e2121f.png)

**Resources**

* https://docs.snowflake.com/en/sql-reference/functions/object_construct

### Question 30

Which is the most accurate description of the Snowflake Partner Connect?

**Answers**

A. The Snowflake Partner Connect allows Snowflake data to be exported to a business partners Snowflake account.

B. The Snowflake Partner Connect allows you to easily create trial account with selected Snowflake business partners and integrate these accounts with Snowflake.

C. The Snowflake Partner Connect allows an account to securely import data from a business partners Snowflake account.

D. The Snowflake Partner Connect exposes contact details for third-party data providers, so a user can connect with them in their own time.

**Correct Answer**

B

**Overall Explanation**

**The correct answer is:** `B. The Snowflake Partner Connect allows you to easily create trial account with selected Snowflake business partners and integrate these accounts with Snowflake.`

**Explanation:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-51-40-9c290112e612bcb5f0a5f6fb7c209105.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/ecosystem-partner-connect

### Question 31

Snowflake uses the following access control schemes: role based access control (RBAC) and _________. Choose one correct value.

**Answers**

A. Discretionary Access Control (DAC)

B. Mandatory Access Control (MAC)

C. Compulsory Access Control (CAC)

D. Imperative Access Control (IAC)

**Correct Answer**

A

**Overall Explanation**

The correct answer is: `A. Discretionary Access Control (DAC)`

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-09_10-59-27-2373bd2c43e2cfa56b26293e1900a3d9.png)

Here's why each option is correct or incorrect:
(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-52-35-ef0d5b2f6ad349063042cd97a7cd94de.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/security-access-control-overview

### Question 32

How does a standard virtual warehouse policy work in Snowflake?

**Answers**

A. It prevents or minimizes queuing by starting additional clusters instead of conserving credits.

B. It starts only if the system estimates that there is a query load that will keep the cluster busy for at least 2 minutes.

C. It starts only if the system estimates that there is a query load that will keep the cluster busy for at least 6 minutes.

D. It conserves credits by keeping running clusters fully loaded rather than starting additional clusters.

**Correct Answer**

A

**Overall Explanation**

**Correct Answer:** `A. It prevents or minimizes queuing by starting additional clusters instead of conserving credits.`

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-54-00-8354de605c124410a74a9ec8285b9d9a.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/warehouses-multicluster

### Question 33

A company that is in one region wants to share data with two different consumers who are both based in a second region

How can this be accomplished with the `MINIMUM` duplication of data?

**Answers**

A. Replicate one copy of the data to the second region, and share it with the two data consumers

B. Replicate two copies of the data to the second region, but only share one of the copies with the two data consumers

C. Replicate two copies of the data to the second region and share each one respectively with the two consumers

D. Create a direct share from the first region to the second region, and provide access to both data consumers

**Correct Answer**

A

**Overall Explanation**

**The correct answer is:** `A. Replicate one copy of the data to the second region, and share it with the two data consumers.`

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-13_04-49-36-cdfae9bd4671feecd962e4d5c97c1518.png)

**Explanation:**
(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-54-58-64da8e4bebfea0dcd935d22de6588269.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/account-replication-intro

### Question 34

What two requirements are necessary for the remote service to be called by the Snowflake external function? (Select 2)

**Answers**

A. Expose an HTTPS endpoint.

B. Store security-related external function information in secure storage.

C. Return a multiple values for each input row

D. Accept JSON inputs and return JSON outputs.

**Correct Answer**

A and D

**Overall Explanation**

**Correct Answers:**

*A. Expose an HTTPS endpoint:* The remote service must be accessible through an HTTPS endpoint for Snowflake to communicate with it securely.

*E. Accept JSON inputs and return JSON outputs:* Snowflake communicates with external functions using JSON data. The remote service needs to be able to handle JSON inputs for processing and return results in JSON format.

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-56-07-8495d49bc3666aa8f41fc02d357a24f4.png)

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-13_08-50-01-8aab2dc3841421b4948221bebecd02c2.png)

**Incorrect Answer:**

*Store security-related external function information in secure storage:* While security is crucial, this is not a specific requirement for the remote service itself. Snowflake manages security aspects like authentication and authorization for accessing the function.

*Return multiple values for each input row:* Currently, external functions must be scalar functions. A scalar external function returns a single value for each input row. So the remote service must also return exactly one row for each row received.

**Resources**

* https://docs.snowflake.com/en/sql-reference/external-functions-introduction

### Question 35

What does the `average_overlaps` in the output of `SYSTEM$CLUSTERING_INFORMATION` refer to?

**Answers**

A. The average number of micro-partitions in the table associated with cloned objects.

B. The average number of micro-partitions which contain overlapping value ranges.

C. The average number of micro-partitions stored in Time Travel.

D. The average number of partitions physically stored in the same location.

**Correct Answer**

B

**Overall Explanation**

**Correct Answer:** `B. The average number of micro-partitions which contain overlapping value ranges.`

**Explanation:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-57-12-7658a36ffeed9d336ae114654496ae44.png)

**Resources**

* https://docs.snowflake.com/en/sql-reference/functions/system_clustering_information

### Question 36

A query is taking a lot of time, and you see the following information in the query profiler:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question/2024-06-18_11-56-22-0351caa45164621c50a8fa73792474b0.png)

What might be the cause of this?

**Answers**

A. There is inefficient pruning.

B. The virtual warehouse is queuing queries.

C. A "exploding join" issue might be the problem.

D. The query is too large to fit in memory.

**Correct Answer**

C

**Overall Explanation**

**Answer:** `C. A "exploding join" issue might be the problem.`

**Explanation:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-58-35-c99437bd83a38245849ec7ff53055ea1.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/ui-query-profile#execution-time
* https://community.snowflake.com/s/article/Performance-impact-from-local-and-remote-disk-spilling

### Question 37

A Snowflake Data Engineer is writing a User-Defined Function (UDF) with some unqualified object names. How will those object names be resolved during execution?

**Answers**

A. Snowflake will resolve them according to the SEARCH_PATH parameter.

B. Snowflake will first check the current schema, and then the schema the previous query used.

C. Snowflake will first check the current schema, and then the PUBLIC schema of the current database.

D. Snowflake will only check the schema the UDF belongs to.

**Correct Answer**

D

**Overall Explanation**

**Answer:** `D. Snowflake will only check the schema the UDF belongs to.`

**Explanation:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_07-59-50-3a13237fd1a9db3692a37182a8230cc1.png)

**Resources**

* https://docs.snowflake.com/en/sql-reference/name-resolution#unqualified-objects

### Question 38

After creating a database and a schema using the following commands:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question/2024-06-18_14-12-43-8ad1b5d693f7c6266e21bb38cf2d4e54.png)

The `MIN_DATA_RETENTION_TIME_IN_DAYS` is set to 10 days at the account level. How long will we be able to access the data from the schema using the Time Travel functionality if we drop the database `BINNI_UDEMY_DB`?

**Answers**

A. 50 days.

B. 30 days.

C. 90 days.

D. The default time of the account.

**Correct Answer**

B

**Overall Explanation**

**Answer:** `B. 30 days.`

**Explanation:**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_08-00-48-1610132fce6f065614920e43c10f0e2f.png)

**Resources**

* https://docs.snowflake.com/en/user-guide/data-time-travel#specifying-the-data-retention-period-for-an-object

### Question 39

Which are the two limitations of the `insertReport` API of Snowpipe? (Select 2)

**Answers**

A. Events are retained for a maximum of 14 days.

B. Events are retained for a maximum of 24 hours.

C. The 10,000 most recent events are retained

D. Events are retained for a maximum of 10 minutes.

E. The 100,000 most recent events are retained

**Correct Answer**

C and D

**Overall Explanation**

**Correct Answers:**

* **C. The 10,000 most recent events are retained.**
* **D. Events are retained for a maximum of 10 minutes.**

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_08-05-38-83312c7cbeb4f4f997e737742c16362b.png)

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-17_07-31-54-baa63fcf194fc705faf21a80291df155.png)

**Incorrect Answers:**

* **A. Events are retained for a maximum of 14 days.** This is incorrect. The actual retention period is 10 minutes.
* **B. Events are retained for a maximum of 24 hours.** This is also incorrect. The retention period is significantly shorter, at 10 minutes.
* **E. The 100,000 most recent events are retained.** The actual limit is 10,000 events.

**Resources**

* https://docs.snowflake.com/en/user-guide/data-load-snowpipe-rest-apis#endpoint-insertreport

### Question 40

What is the meaning of “Local Disk IO” in the query profiler menu when running a query?

**Answers**

A. The time spent on data processing by the CPU.

B. The time when the processing was waiting for the network data transfer.

C. The time when the processing was blocked by local disk access.

D. The time spent setting up the query processing.

**Correct Answer**

C

**Overall Explanation**

The correct answer is: `C. The time when the processing was blocked by local disk access.`

Explanation:

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-09-29_08-07-45-f5bf10d9656cec8efc4a95b33696daef.png)

(Image: https://img-c.udemycdn.com/redactor/raw/practice_test_question_explanation/2024-06-21_07-53-28-dc6bcee0a04c0c32c0e32186c785d8d2.png)

Here's a breakdown of each option and why it's correct or incorrect:

* **A. The time spent on data processing by the CPU (Incorrect):** This is represented by the "Processing" category in the query profile.
* **B. The time when the processing was waiting for the network data transfer (Incorrect):** This is represented by the "Network Communication" category.
* **C. The time when the processing was blocked by local disk access (Correct):** This is the intended meaning of "Local Disk IO." Snowflake's virtual warehouses use local disks on the worker nodes to temporarily store data during query execution. If the amount of data being processed exceeds the available memory, Snowflake spills data to local disks, leading to "Local Disk IO" wait time.
* **D. The time spent setting up the query processing (Incorrect):** This is typically included in the overall processing time or might be a negligible factor in modern query processing engines.

**Resources**

* https://docs.snowflake.com/en/user-guide/ui-query-profile#execution-time