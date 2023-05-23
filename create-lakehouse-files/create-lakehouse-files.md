# Load mysql\_customer\_orders Data into HeatWave Cluster

## Introduction

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

### Objectives

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

### Prerequisites

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

## Task 1: Download and unzip  Sample files

1. If not already connected with SSH, on Command Line, connect to the Compute instance using SSH ... be sure replace the  "private key file"  and the "new compute instance ip"

     ```bash
    <copy>ssh -i private_key_file opc@new_compute_instance_ip</copy>
     ```

2. Setup folder to house imported sample data

    a. Create folder

    ```bash
    <copy>mkdir lakehouse</copy>
     ```

    b. Go into folder

    ```bash
    <copy>cd lakehouse</copy>
     ```

3. Download sample files

    ```bash
    <copy>wget https://objectstorage.us-ashburn-1.oraclecloud.com/p/TGmbWNTNxauEBSZKxOaKPggbJRz2k_3i6XiDp5Kq5LRJ3c47Z-U8bb_iuSweoi9X/n/mysqlpm/b/plf_mysql_customer_orders/o/lakehouse/lakehouse-order.zip</copy>
     ```

4. Unzip sample files

    ```bash
    <copy>unzip lakehouse-order.zip</copy>
     ```

## Task 2: Create your own data Oject Storage Bucket

## Task 3: Load Sample data into your Bucket

You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Solution Engineering
- **Contributors** - Abhinav Agarwal, Principal Senior Principal Product Manager, Nick Mader, MySQL Global Channel Enablement & Strategy Manager
- **Last Updated By/Date** - Perside Foster, MySQL Principal Solution Engineering, April 2023
