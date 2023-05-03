## **Digital Sales I-Analyze**

Digital Sales I-Analyze is a comprehensive project designed to fetch and analyze data from multiple sources in order to provide valuable insights and analytics for digital sales activities. The project integrates with various data sources including e-dialog, Google Analytics, Search Ad 360, Supermetrics (CM360, DV360, Meta, Google Ads), and utilizes GCP Airflow for data loading and transfer.

## **Data Sources**

The project fetches data from the following sources:

**E-dialog**: Provides access to Google Analytics data, including website traffic, user behavior, and conversions.

**Google Analytics (GA4)**: Fetches data related to website traffic, user interactions, and conversion events.

**Search Ad 360 (SA360)**: Retrieves data from the search management platform, including campaign performance metrics, ad impressions, clicks, and conversions.

## **Supermetrics**:

**CM360 (Campaign Manager 360)**: Fetches data on campaign performance, ad impressions, clicks, and conversions.
**DV360 (Display and Video 360)**: Retrieves data related to display and video ad performance, impressions, clicks, and conversions.<br>
**Meta (Facebook)**: Fetches data from Facebook, including ad campaign metrics and performance.<br>
**Google Ads**: Retrieves data related to Google Ads campaigns, ad performance, clicks, and conversions.

## **Data Loading and Scripts**

The project utilizes the following scripts to load and transfer data:

**daily_load_to_bq.py**: This script is used for the daily load to the target tables in BigQuery. It fetches data from the source BigQuery tables, which are loaded via connections, and creates a CSV file of all the data. The CSV file is then stored in a GCS (Google Cloud Storage) bucket associated with the target tables.

**bq_transfer_from_prod_to_test.py**: This script transfers all the data from the production BigQuery environment to the test BigQuery environment. It creates a CSV file of the data and stores it in a GCS bucket.

**bq_transfer_from_prod_to_dev.py**: This script is run incrementally after the daily load to the production environment. It transfers the daily changes to the development environment and creates CSV files for the transferred data.

**retention_multiple_partition.py**: This script runs monthly to delete partitions older than 2 years from BigQuery. Before deletion, the script stores the deleted partitions in an archive bucket in GCS.

## **Workflow Steps**

**Data Extraction**: The project initiates data extraction from each data source using appropriate APIs and connectors. The data is fetched based on the defined queries and filters to retrieve the desired information.

**GCP Airflow Integration**: The project utilizes GCP Airflow, a workflow management system, to orchestrate the data loading and transfer processes. Airflow provides the ability to schedule, monitor, and execute tasks in a reliable and scalable manner.

**Daily Load to BigQuery**: The daily_load_to_bq.py script is executed on a daily basis. It retrieves data from the source BigQuery tables (which are loaded via connections) and loads it into staging/target tables in BigQuery. Additionally, the script generates a CSV file containing all the data and stores it in a GCS bucket associated with the target tables.

**Transfer to Test Environment**: The bq_transfer_from_prod_to_test.py script is run on a monthly basis. It transfers all the data from the production BigQuery environment to the test BigQuery environment. The script creates a CSV file of the transferred data and stores it in a GCS bucket for further analysis and testing.

**Incremental Transfer to Development**: After the daily load to the production environment, the bq_transfer_from_prod_to_dev.py script is executed on an incremental basis. It transfers only the daily changes to the development environment and generates corresponding CSV files for further analysis and development purposes.

**Retention and Archiving**: The retention_multiple_partition.py script runs monthly to delete partitions older than 2 years from BigQuery. Before deletion, it securely archives the partitions by storing them in an archive bucket in GCS. This ensures efficient data management and compliance with data retention policies.

**EDWH Data Transfer**: The project facilitates the transfer of data from both the production and development environments to the Enterprise Data Warehouse (EDWH) on a regular basis. This is accomplished using a "$universe" script running on the application server. The script retrieves the CSV files from the GCS bucket and loads them into the EDWH using TPT (Teradata Parallel Transport)

## **Conclusion**

Digital Sales I-Analyze is a robust project that enables the seamless extraction, analysis, and transfer of data from multiple sources to gain valuable insights and analytics for digital sales activities. By integrating with e-dialog, Google Analytics, Search Ad 360, and Supermetrics (CM360, DV360, Meta, Google Ads), the project covers a wide range of data sources to provide comprehensive and accurate information.

The project utilizes GCP Airflow for efficient workflow management, ensuring reliable and scheduled execution of tasks. The daily load to BigQuery script (daily_load_to_bq.py) facilitates the daily transfer of data to staging/target tables, creating CSV files for further analysis and storage in a designated GCS bucket.

To support testing and analysis, the bq_transfer_from_prod_to_test.py script transfers data from the production BigQuery environment to the test environment, allowing for thorough examination of the data's accuracy and reliability. The incremental transfer to the development environment script (bq_transfer_from_prod_to_dev.py) ensures that only the daily changes are loaded, improving efficiency and reducing redundancy.

Data retention and archiving are addressed by the retention_multiple_partition.py script, which removes older partitions from BigQuery while securely storing them in an archive bucket in GCS. This helps maintain data integrity while complying with retention policies.

Finally, the project facilitates the regular transfer of data to the Enterprise Data Warehouse (EDWH) through the "$universe" script running on the application server. This ensures that data from both the production and development environments is efficiently loaded into the EDWH for further analysis and reporting.

Digital Sales I-Analyze provides a comprehensive solution for digital sales data management, enabling organizations to derive valuable insights and make informed decisions to optimize their digital sales strategies.