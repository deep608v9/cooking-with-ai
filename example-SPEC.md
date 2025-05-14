# Cloudflare IP List Monitor

This Azure Function runs on a schedule and downloads the current Cloudflare Source IP List (https://www.cloudflare.com/ips-v4), stores the list in an Azure Storage Account, and sends a webhook alert if a new IP has been added.

Written in Python, using the requests library. Deployed with Terraform to Azure; a managed service identity is used for the Azure Function to Authenticate to the Azure Storage Account.

## Infrastructure as Code
Written in Terraform
Deploys Azure Function with MSI and Azure Storage Account
Any Resource Groups or other required resources are also deployed
The Azure Function is scheduled to run hourly
There should be an input parameter for a Webhook URL that the Azure Function will use (provided to the function as an Environment Variable)
The Azure Storage Account should have versioning enabled and be set for open public access

## Azure Function Details
Download latest IP list from Cloudflare
Check the Azure Storage Account to see if there is an existing IP list; if there is, download that as well
Compare the lists, call the webhook for each new entry
Replace the list in the Azure Storage Account with the new one if there are changes
Provide detailed debug output
![Uploading image.png…]()
