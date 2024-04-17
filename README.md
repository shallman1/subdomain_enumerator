# Subdomain Enumeration API

## Overview
This Flask application manages the enumeration of subdomains using the Subfinder tool. It provides functionality to filter active subdomains and identify inactive or wildcard subdomains. The application offers an API endpoint for submitting domain names and receiving detailed subdomain data, categorized into active and inactive/wildcard lists.

## Functionality
- **Subdomain Enumeration:** Enumerates subdomains from a list of domains using the Subfinder tool.
- **Active Subdomains Filtering:** Filters and categorizes subdomains based on their status as active, inactive, or wildcard entries.
- **API Endpoint:** Delivers results through an API endpoint where users can submit domain names and receive structured subdomain data.

## Installation and Setup
1. Clone the repository and navigate to the project directory.
2. Install required Python packages: 'pip install flask'
3. Run the application: 'python app.py'

## API Usage
- **Endpoint:** `/subdomains`
- **Method:** `GET`
- **Parameters:** `domains` (comma-separated list of domains)
- **Returns:** JSON object containing subdomain data categorized by active and inactive/wildcard counts and lists.

## Wildcard Qualification Logic
The application uses the `-active` flag in the Subfinder command to qualify subdomains as active or wildcard/inactive. This process includes:
- **Initialize Wildcard IPs:** The `enumerate_subdomains` function appends a `-nW` flag to the Subfinder command to exclude wildcards when the `active_only` parameter is true.
- **DNS Lookup and Filtering:** Subfinder resolves DNS for each subdomain and filters out entries matching any known wildcard IP addresses.
- **Results Categorization:** Subdomains are categorized based on their activity status and whether they match wildcard IPs. Active subdomains are sent to an "active subdomains" results channel, while those that match wildcard criteria are sent to an "inactive_or_wildcards" results channel.

## Prerequisites
### Installing Subfinder
Subfinder must be installed for this application to function. It can be installed using several methods:

#### Binary Installation
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest

### API setup
- **To use DNSDB and other sources requiring API keys, configure the ~/.config/subfinder/provider-config.yaml file. Add your API keys as follows:
  
 "- dnsdb:
   - your-dnsdb-api-key"
