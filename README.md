# Bulk creation of Services in PagerDuty via .CSV file.

## Prerequisites 
This script requires 
* Python 3 installed
* A correctly formatted .CSV file in order to Bulk create Services within PagerDuty via API.
* A PagerDuty User/Account with Admin permissions
* A Valid RestAPI Token to PagerDuty - PagerDuty > Integrations > Access Keys
* TLS 1.2 is enabled with the appropriate Digicert root certificates installed  - https://developer.pagerduty.com/docs/authentication  

1: Set Up API Credentials:
  * Replace <Your API Key> with a valid PagerDuty API Key within the API_KEY field of the script.
  * Confirm the API key has the necessary permissions to create services, and is not Read-only

![Rest API Screen](https://github.com/NPBBPN/PagerDuty-Test/blob/main/images/RestAPI%20Token%20Creation.PNG "REST API Creation Page in PagerDuty")

2: Prepare the CSV File:
* Format your CSV file (services.csv) with the following headers:

      type,name,description,auto_resolve_timeout

Example data:

    type,name,description,auto_resolve_timeout
    service,My Web App,My cool web application,14400
    service,Another Web App,Another application,10800

* Ensure the CSV file is stored in the expected path, as defined in the script to be the same directory as the script itself.

3: Run the Script - See below:

## Windows
* Open Command Prompt (CMD) or PowerShell

  * Press Win + R, type cmd or powershell, and hit Enter.
* Navigate to the Script/CSV Directory

* If your script is in C:\Python Testing, run `cd C:\Python Testing`

* Execute the script `C:\Python Testing\CSVImportPagerduty.py`


## Linux
* Open Terminal

* Navigate to the Script Directory

If the script and csv are in ~/Documents/, run:

    cd ~/Documents/

* From the working directory, execute the script from the terminal:

       python3 CSVImportPagerduty.py
    
## Output
The script will read each row from the CSV and create a corresponding service in PagerDuty.

      c:\Python Testing>"CSVImportPagerduty.py"
      Successfully created service: My Web App
      Successfully created service: Another Web App
      Successfully created service: My Best Web App


## Troubleshooting
* "File  (services.csv) not found" - Check that the CSV file path is correct and the file exists.
  * If the script is in `C:\Python Testing`, confirm `services.csv` is also there.
    
* API authentication errors
  *  Ensure the API key is correct and has the right permissions:
    
    `Generate a new API key in PagerDuty > Integrations > API Access Keys.`
  
    `Replace <Your API Key> in the script with the new key.`
  

* Verify your API key is correct and has write permissions.

* "Failed to create service" - Check the specific error message for details. Common issues include duplicate service names or invalid escalation policy ID.
    * `Failed to create service Services: {"error":{"message":"Invalid Input Provided","code":2001,"errors":["Name has already been taken"]}}`
        * This is where a Service with a matching Name already exists - compare the .csv to existing services in the Service Directory under the Services tab.

  
