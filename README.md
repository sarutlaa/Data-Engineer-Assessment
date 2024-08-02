# Data-Engineer-Assessment
Community Choice Credit Union Assessment

This document outlines the steps required to set up and configure the necessary services and integrations for the Data Engineer Assessment at Community Choice Credit Union.

## Prerequisites
Oracle Cloud Account: Set up a free Oracle Cloud account to access Oracle Cloud Infrastructure (OCI) services.

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

### Integration Setup
* Start Integration Development:
* In OIC, select App Driven option under the integration type.
* Configure the integration to read data from the CSV file stored in Object Storage as a Trigger.
* Map the readCSV file with its proper format.




REST IS PENDING, FACED AN ISSUE WITH MAPPING, NEED MORE CLARITY WITH RESPECT TO ORACLE CLOUD. 


