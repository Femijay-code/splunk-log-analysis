# Splunk Apache Log Analysis

## Overview
This project focuses on analyzing Apache server logs using Splunk.

## Tools Used
- **Splunk Enterprise**
- **apache_logs.txt** (sample data)

## Key Objectives
- Upload and index raw Apache logs into Splunk.
- Run specific search queries to extract valuable insights.
- Understand log behavior for security event detection.

## Searches Performed
1. **All Logs:**  
   `index=apache_logs`  
   Shows all logs in the Apache index.

2. **All Requested URLs:**  
   `index=apache_logs | table _time, uri_path`  
   Lists all accessed URLs.

3. **IP Addresses That Accessed the Server:**  
   `index=apache_logs | stats count by clientip`  
   Groups access by IP address.

4. **404 Error Logs:**  
   `index=apache_logs status=404`  
   Filters logs with HTTP 404 status (Not Found).

## Screenshots Included
- General log overview
- Requested URLs
- IP access stats
- 404 error logs

## Documentation
See the attached Word document for a detailed breakdown of the searches, screenshots, and insights derived from the analysis.
