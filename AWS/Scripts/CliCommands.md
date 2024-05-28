#### [Back](./README.md)

# CLI Commands

### How to Install. ###
```bash
    npm i
```

### Download Dynamodb Data. ###
```bash
    bash DDB/download.sh sandbox timezone_list
```

### Download Swagger Documentation JSON ###
```bash
    bash Swagger/documentation.sh DEV 5juhqihl5c adminservice
```

### Download All Rest API. ###
```bash
    bash Swagger/downloadRestAPIList.sh sandbox
```

### Download All Gateway Keys. ###
```bash
    bash Swagger/downloadApiKeysList.sh sandbox
```

### Download All Gateway Keys. ###
```bash
    bash IOTCore/JobExecutionList.sh sandbox 1639672481646 PNRA0PIF01333K8PE3
```

### Create IOT JOB CLI. ###
```bash
    bash IOTCore/CreateJob.sh sandbox PNR01IF31017111984 IOTCore/jobDocument.json
```

### Sync S3 Bucket Content. ###
```bash
    bash S3/syncbucket.sh sandbox pentair-sandbox
```

### Update User Attributes. ###
```bash
    bash Cognito/updateattribute.sh sandbox dealerPool \
      Salesforce_https://test.salesforce.com/id/00D6C0000000yzhUAA/0056C000002mZAwQAM \
      custom:externalProviderData asdf
```

### Make AWS API Call ###
```bash
    node Http/post.js requests/ScheduledOta/List/all.json admin2/admin2-service/schedulerJobConfig/list
```

### Create Scheduled OTA ###
```bash
    node Http/ota.js PNRD1IC21017111984 2
```

### Delete User from Cognito from Email Id. ###
```bash
    bash Cognito/deleteUserByEmail.sh sandbox dealerPool vishal.gupta@pentair.com
```

### Create Things. ###
```bash
    bash IOTCore/CreateThings.sh
```

### Download List of Things. ###
```bash
    profile=sandbox node IOTCore/export.js
```

### Start EC2 Server. ###
```bash
    aws ec2 start-instances \
        --instance-ids i-XXXXXXXXXXXX
```

### Start EC2 Server. ###
```bash
    aws ec2 stop-instances \
        --instance-ids i-XXXXXXXXXXXX
```
