````markdown
# Frothly AWS Incident Investigation

## Project Overview
This project analyzes Frothly's AWS environment logs using Splunk to answer key security and operational questions. It demonstrates the use of Splunk searches and log analysis techniques to investigate IAM user activity, S3 bucket access, system processor details, and endpoint characteristics.

---

## Questions & Answers

1. **List out the IAM users that accessed an AWS service (successfully or unsuccessfully) in Frothly's AWS environment?**

   - IAM Users:
     - bstoll

2. **What is the processor number used on the web servers?**

   - Processor Number: `E5-2676 v3`

3. **Bud accidentally makes an S3 bucket publicly accessible. What is the event ID of the API call that enabled public access?**

   - Event ID: `5a44f1e1-3801-4e7a-9a88-4f3e121f2f1d`

4. **What is the name of the S3 bucket that was made publicly accessible?**

   - Bucket Name: `frothlywebcode`

5. **What is the name of the text file that was successfully uploaded into the S3 bucket while it was publicly accessible?**

   - File Name: `OPEN_BUCKET_PLEASE_FIX.txt`

6. **What is the size (in mb) of the .tar.gz file that was successfully uploaded into the S3 bucket while it was publicly accessible?**

   - Size: `2.93 MB`

7. **What is the short hostname of the only Frothly endpoint to actually mine Monero cryptocurrency?**

   - Short Hostname: `BTUN-L`

8. **What is the FQDN of the endpoint that is running a different Windows operating system edition than the others?**

   - FQDN: `SEPM.froth.ly`

---

## Splunk Search Queries Used

### 1. IAM Users Accessing AWS Services

```splunk
index=aws_cloudtrail userIdentity.type=IAMUser | stats count by userIdentity.userName
````

### 2. Processor Number on Web Servers

```splunk
index=linux_metrics sourcetype=top | stats values(cpu_model) as ProcessorNumber
```

### 3. Public Access Event ID for S3 Bucket

```splunk
index=aws_cloudtrail eventName=PutBucketAcl | table eventID, userIdentity.userName, requestParameters.bucketName
```

### 4. Publicly Accessible S3 Bucket Name

```splunk
index=aws_s3_accesslogs status=200 | stats values(bucket) as BucketName
```

### 5. Text File Uploaded During Public Access

```splunk
index=aws_s3_accesslogs action=REST.GET.OBJECT | search filename="OPEN_BUCKET_PLEASE_FIX.txt" | table filename
```

### 6. Size of Uploaded .tar.gz File

```splunk
index=aws_s3_accesslogs action=REST.PUT.OBJECT | search filename="frothly_html_memcached.tar.gz" | stats max(size) as FileSizeBytes | eval FileSizeMB = round(FileSizeBytes/1024/1024, 2)
```

### 7. Short Hostname Mining Monero Cryptocurrency

```splunk
index=endpoint_logs process_name=miner_monero | table hostname
```

### 8. FQDN of Endpoint with Different Windows OS Edition

```splunk
index=windows_logs os_edition!= "Windows 10 Pro" | table fqdn
```

---

## Summary

This investigation leveraged Splunk's powerful search capabilities on Frothly's datasets to extract valuable security insights. The analysis identified specific IAM users accessing AWS resources, revealed accidental public S3 bucket exposure along with details of files uploaded, and detected endpoint behaviors including mining activities and OS version discrepancies.

This project serves as an example of how log analysis and SIEM tools like Splunk can be used in practical security operations center (SOC) investigations.

---

## Author

Francis Olorunfemi Jacob
Email: [femijay123@gmail.com](mailto:femijay123@gmail.com)
GitHub: [https://github.com/Femijay-code](https://github.com/Femijay-code)

```
```
