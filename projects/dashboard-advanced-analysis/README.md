# 🧠 Project 2: Advanced Apache Log Analysis Using Splunk

This project focuses on log analysis using Splunk. I uploaded real Apache logs and created a custom dashboard with multiple visualizations using SPL (Search Processing Language).

---

## 📁 Dataset
- **File**: `apache_logs.txt`
- **Source Type**: `access_combined`
- **Index**: `apache_logs`
- **Host**: `DESKTOP-U52N20A`

---

## 📊 Dashboard Charts & SPL Queries

### 1. Bar Chart: Top IP Addresses (clientip)
```spl
index=apache_logs sourcetype=access_combined 
| top limit=10 clientip
🔹 Insight: Shows the most active IP addresses making requests to the server.

2. Bar Chart: Most Active Users
index=apache_logs sourcetype=access_combined 
| top limit=10 user
🔹 Insight: Only one record was shown, indicating user field was likely missing in the logs.

🔍 SPL Searches Screenshots
clientip search result:
user search result:

📘 Summary
A full Word document (Apache_Log_Analysis_Summary.docx) is included in this folder, detailing:
Steps followed
Dashboard creation process
Challenges encountered
Final results

📚 Skills Demonstrated
Splunk data ingestion
SPL querying
Field recognition and troubleshooting
Dashboard creation
