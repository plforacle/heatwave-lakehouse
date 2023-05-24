# Load CSV data from OCI Object Store

## Introduction

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

### Objectives

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

### Prerequisites

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

## Task 1: Run Autoload to infer the schema and estimate capacity required for the DELIVERY table in the Object Store

1. Login to the OCI Console.
2. Click the Cloud Shell icon in the Console
3. Connect to MySQL using the MySQL Shell client tool with the following command:

    ```bash
    <copy>mysqlsh -uadmin -p -h 10.0.1... --sql </copy>
    ```

    ![Connect](./images/mysql-shell-login.png " mysql shell login")

4. Enter the following commands one by one and hit Enter.

    a.

    ```bash
    <copy>SET @db_list = '["mysql_customer_orders"]';</copy>
    ```

    b.

    ```bash
    <copy>SET @dl_tables = '[{
    "db_name": "mysql_customer_orders",
    "tables": [{
        "table_name": "delivery_orders",
        "dialect": 
           {
           "format": "csv",
           "field_delimiter": "\\t",
           "record_delimiter": "\\n"
           },
        "file": [{"par": "https://objectstorage.us-ashburn-1.oraclecloud.com/p/MAGNmpjq3Ej4wX6LN6KaE3R9AM2_h_fQDhfM5C9SbKXO_Zbe4MdrTvypV5XsyHkS/n/mysqlpm/b/lakehousefiles/o/delivery-orders-1.csv"}]
    }] }]';</copy>
    ```

    a.

    ```bash
    <copy>SET @db_list = '["SET @options = JSON_OBJECT('mode', 'dryrun', 
    'policy', 'disable_unsupported_columns',
    'external_tables', CAST(@dl_tables AS JSON));"]';</copy>
    ```

    a.

    ```bash
    <copy>CALL sys.heatwave_load(@db_list, @options);</copy>
    ```

    a.

    ```bash
    <copy>SELECT log->>"$.sql" AS "Load Script" FROM sys.heatwave_autopilot_report WHERE type = "sql" ORDER BY id;</copy>
    ```

    a.

    ```bash
    <copy>CREATE TABLE `mysql_customer_orders`.`delivery_orders`( `col_1` int unsigned NOT NULL, `col_2` bigint unsigned NOT NULL, `col_3` tinyint unsigned NOT NULL, `col_4` varchar(9) NOT NULL COMMENT 'RAPID_COLUMN=ENCODING=VARLEN', `col_5` tinyint unsigned NOT NULL, `col_6` tinyint unsigned NOT NULL, `col_7` tinyint unsigned NOT NULL) ENGINE=lakehouse SECONDARY_ENGINE=RAPID ENGINE_ATTRIBUTE='{"file": [{"par": "https://objectstorage.us-ashburn-1.oraclecloud.com/p/MAGNmpjq3Ej4wX6LN6KaE3R9AM2_h_fQDhfM5C9SbKXO_Zbe4MdrTvypV5XsyHkS/n/mysqlpm/b/lakehousefiles/o/delivery-orders-1.csv"}], "dialect": {"format": "csv", "field_delimiter": "\\t", "record_delimiter": "\\n"}}'; ALTER TABLE `mysql_customer_orders`.`delivery_orders` SECONDARY_LOAD;</copy>
    ```

## Task 2: Load complete DELIVERY table from Object Store into MySQL HeatWave

    a.

    ```bash
    <copy>desc delivery_orders;</copy>
    ```

    a.

    ```bash
    <copy> ALTER TABLE `mysql_customer_orders`.`delivery_orders` SECONDARY_LOAD; </copy>
    ```

    a.

    ```bash
    <copy>use mysql_customer_orders</copy>
    ```

    a.

    ```bash
    <copy>select count(*) from delivery_orders;</copy>
    ```

    a.

    ```bash
    <copy>select * from delivery_orders limit 5;</copy>
    ```

    a.

    ```bash
    <copy> select o.* ,d.*
        from  orders o
        join delivery_orders d on o.ORDER_ID = d.col_2
        where o.order_id = 93751524; </copy>
    ```

    a. Get Second Link

    ```bash
    <copy>use mysql_customer_orders;</copy>
    ```

    a.

    ```bash
    <copy>ALTER TABLE delivery_orders SECONDARY_UNLOAD;</copy>
    ```

    a.

    ```bash
    <copy>ALTER TABLE `mysql_customer_orders`.`delivery_orders` ENGINE_ATTRIBUTE='{"file": [{"par": "https://objectstorage.us-ashburn-1.oraclecloud.com/p/4EayDq3tv-D08oTTPja-2XEYZSQ0v5cG87CFNc31wT724QB5R21C1UXbK0_snbZA/n/mysqlpm/b/lakehousefiles/o/"}], "dialect": {"format": "csv", "field_delimiter": "\\t", "record_delimiter": "\\n"}}';
    </copy>
    ```

    a.

    ```bash
    <copy>alter table delivery_orders secondary_load;</copy>
    ```

    a.

    ```bash
    <copy>select count(*) from delivery_orders;</copy>
    ```

You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Solution Engineering

- **Contributors** - Abhinav Agarwal, Senior Principal Product Manager, Nick Mader, MySQL Global Channel Enablement & Strategy Manager
- **Last Updated By/Date** - Perside Foster, MySQL Solution Engineering, May 2023
