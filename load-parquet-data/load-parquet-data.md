# Load Parquet data from OCI Object Store

## Introduction

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

### Objectives

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

### Prerequisites

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

## Task 1: Load data by specifying a PAR URL for all objects with a prefix

1. From your OCI console, navigate to your bucket in OCI.
2. Select the first file —> delivery-orders-1.csv and click the three vertical dots.
3. Click on ‘Create Pre-Authenticated Request’
4. Click to select the ‘Objects with prefix’ option under ‘Pre0Authentcated Request Target’.
5. Leave the ‘Access Type’ option as-is: ‘Permit object reads on those with the specified prefix’.
6. Click to select the ‘Enable Object Listing’ checkbox.
7. Click the ‘Create Pre-Authenticated Request’ button.
8. Click the ‘Copy’ icon to copy the PAR URL.
9. Save the generated PAR URL; you will need it later.
10. You can test the URL out by pasting it in your browser. It should return output like this:
11. Since we have already created the table, we will not run Autopilot again. Instead we will simply go ahead and change the table definition to point it to this new PAR URL as the table source.
12. Run this command to add this PAR URL as a source for the DELIVERY table:

    ```bash
    <copy>ALTER TABLE `livelabs`.`DELIVERY` ENGINE_ATTRIBUTE='{"file": [{"par": "https://objectstorage.us-ashburn-1.oraclecloud.com/p/oJ4umFlMGGM6OqxlgBwxLw5PfNFzOVleaa_qVDDvtCDNtrkgQ8u4Nwx9PgY5_KuE/n/mysqlpm/b/lakehouse-livelabs/o/"}], "dialect": {"format": "csv", "field_delimiter": "\\t", "record_delimiter": "\\n"}}'; </copy>
    ```

13. Now load data into the DELIVERY table:

    ```bash
    <copy>alter table DELIVERY secondary_load;</copy>
    ```

14. View the number of rows in the DELIVERY table:

    ```bash
    <copy>select count(*) from DELIVERY;</copy>
    ```

- The DELIVERY table now has 34 million rows.

## Task 2: Load Parquet format data directly from Object Store

1. Create PAR URL for Parquet file
2. Create DELIVERY_VENDOR table
3. On your SQL prompt, run the following command:

    ```bash
    <copy>CREATE TABLE DELIVERY_VENDOR(
    id INTEGER,
    vendor_name VARCHAR(200)
    ) 
    ENGINE=lakehouse SECONDARY_ENGINE=RAPID 
    ENGINE_ATTRIBUTE='{"file": [{"par": "https://objectstorage.us-ashburn-1.oraclecloud.com/p/FEE4UaxvnmCHkVCbDFcqe38AJIjaxJAiJSheDBt4LgB-ZvZFrfxCeWhHgB1O3eqE/n/mysqlpm/b/lakehouse-livelabs/o/delivery-vendor.pq"}], "dialect": {"format":"parquet"}}';</copy>
    ```

4. Run this command to see the table structure created.

    ```bash
    <copy>desc DELIVERY_VENDOR;</copy>
    ```

5. Now load the data from the Object Store into the ORDERS table.

    ```bash
    <copy>ALTER TABLE DELIVERY_VENDOR SECONDARY_LOAD;</copy>
    ```

6. Once Autoload completes, check the number of rows loaded into the table.

    ```bash
    <copy>select count(*) from DELIVERY_VENDOR;</copy>

7. View a sample of the data in the table.

    ```bash
    <copy>select * from DELIVERY_VENDOR limit 5;</copy>
    

You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Solution Engineering
- **Contributors** - Abhinav Agarwal, Principal Senior Principal Product Manager, Nick Mader, MySQL Global Channel Enablement & Strategy Manager
- **Last Updated By/Date** - Perside Foster, MySQL Principal Solution Engineering, April 2023
