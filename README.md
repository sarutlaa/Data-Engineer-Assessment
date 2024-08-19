# Data-Engineer-Assessment
Community Choice Credit Union Assessment

This document outlines the steps required to set up and configure the necessary services and integrations for the Data Engineer Assessment at Community Choice Credit Union.

## Prerequisites
Oracle Cloud Account: Set up a free Oracle Cloud account to access Oracle Cloud Infrastructure (OCI) services.

![image](https://github.com/user-attachments/assets/240c1bfe-b733-4b9f-8221-a511e87b12be)



## Steps to Implement
### Step 1: Upload the CSV File to Object Storage
* Create a Bucket: Log in to your Oracle Cloud account and navigate to the Object Storage service. Create a new bucket to store your CSV file.
* Upload File: Upload the desired CSV file into the newly created bucket.

### Step 2: Add API Keys
* Navigate to Identity and Security: Access the Identity and Security settings in your Oracle Cloud dashboard.
* Manage API Keys:
* Go to Identity > Users.
* Select your user profile and add an API Key.
* Download the public and private keys for API access. Ensure you copy any displayed text or keys shown on the screen for later use.

### Step 3: Create an Oracle Integration Cloud (OIC) Instance
* Provision OIC Instance: From the main dashboard, go to Services and select Oracle Integration Cloud. Follow the prompts to create a new instance.

### Step 4: Assigning Roles and Users to OIC
* Assign Roles:
    - Navigate to Identity and Security > Identity > Domains > Users.
    - Assign the appropriate roles to your user to ensure access to the necessary services within OIC.

### Step 5: Configure REST Connection in OIC
* Open OIC Design Area:
* Navigate to OIC > Design > Integrations.
* Click on Add Connection.
* Choose REST and provide a name for the connection.
* Set Connection Type and URL:
* For the connection type, select REST API Base URL.
* Set the Connection URL to https://objectstorage.us-chicago-1.oraclecloud.com.

### Step 6: Create an Oracle ATP Instance and Configure Connection
* Create ATP Instance:
* Navigate to Oracle ATP services and create a new Autonomous Transaction Processing (ATP) instance.
* Download the wallet file which contains credentials for connecting to the database.
* Add ATP Connection to Integration:
* Return to the OIC integration area.
* Add a new database connection using the Oracle ATP type.
* Upload the wallet file and configure the database connection parameters.

### Step 7: Integration Build Setup
* Start Integration Development:
#### Trigger - GetObjectStorage
1. Purpose:
The Trigger was supposed to initiate the integration flow by connecting to OCI Object Storage to fetch the CSV file.
2 Configuration:
The REST connection was configured with the necessary authentication credentials and pointed to the correct URI where the CSV file was stored.
3 Challenges:
Despite the correct configuration, there were issues with correctly accessing or interpreting the file content, which impacted subsequent steps in the flow.

#### Stage File - readCSV
1. Purpose:
The Stage File action was intended to read the entire content of the CSV file fetched from Object Storage.

2. Configuration:
The operation was set to "Read Entire File," but there were challenges related to specifying the correct File Reference from the Trigger.

3. Challenges:
The Stage File action did not successfully read the file content. Possible issues included incorrect file reference mapping or issues with the file format/encoding that were improperly handled.

#### Logger - Logger1
1. Purpose:
The Logger action was configured to log the content of the CSV or messages related to the data processing.
2. Challenges:
Due to the issues in the previous step (Stage File), the logger might not have captured the expected data, making it difficult to verify what was processed.


#### Map - InsertCSVData
1. Purpose:
The Map action was supposed to map the CSV data fields to the corresponding columns in the ATP database table.
2. Challenges:
Since the data was not correctly read, the mapping step likely failed or did not map the expected data to the ATP table structure.

#### Invoke - InsertCSVData
1. Purpose:
The Invoke action was intended to insert the mapped data into the Oracle ATP database.
2. Challenges:
Without correctly mapped data, the insertion step would not have succeeded. The data may not have reached this point in the integration due to earlier failures.

![image](https://github.com/user-attachments/assets/17611faf-7b49-4dba-a5bd-e47c7d07c0d4)


## Data Analysis After Successful Integration Flow Execution
If the integration flow had been executed successfully, the next logical step would be to proceed with data analysis on the data that has been successfully loaded into the Oracle Autonomous Transaction Processing (ATP) database.

Write an SQL query to calculate complaint totals by product.

```SQL

SELECT 
    PRODUCT, 
    COUNT(*) AS TOTAL_COMPLAINTS
FROM 
    CONSUMER_COMPLAINTS
GROUP BY 
    PRODUCT
ORDER BY 
    TOTAL_COMPLAINTS DESC;

```




