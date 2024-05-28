#### [Back](./README.md)

# AWS IOT Create OTA With RollOut and Abort Configuration.

### What is OTA?

Over-the-air (OTA) Updated allows you to deploy update firmware updates on one or more devices in your fleet.
Below is the bash command to create OTA.
```angular2html
    aws iot create-job \
        --job-id "example-cli-job" \
        --document file://IOTCore/jobDocument.json \
        --description "Job test for dynamic group" \
        --target-selection SNAPSHOT \
        --job-executions-retry-config file://IOTCore/config/retries.json \
        --job-executions-rollout-config file://IOTCore/config/rollout.json \
        --abort-config file://IOTCore/config/abort.json \
        --targets "arn:aws:iot:us-east-1:test_account_id:thinggroup/testdevices"
```
You need a latest AWS Cli version for creating OTA with above given command (mine is 2.5.8).

**targets:-** Targets can be single Device, group of Devices Or Groups like Static and Dynamic Group.

**retry-config:-**  Retry config is a config on how failed devices should behave. Like below JSON i have used to retry 2 times on Failed OTA Update. It is an array of config so we can pass more than option.    

```json
{
  "criteriaList": [
    {
      "failureType": "FAILED",
      "numberOfRetries": 2
    }
  ]
}
```

**rollout-config:-**  Roll Out config is a config on how the OTA update should roll out on devices. Below is the config for start ota update on 10 devices per minute. if the rate increase creteria met the OTA will increase rate on OTA Update with given incrementFactor.
```json
{
    "maximumPerMinute": 10,
    "exponentialRate": {
        "baseRatePerMinute": 10,
        "incrementFactor": 1.5,
        "rateIncreaseCriteria": {
            "numberOfSucceededThings": 1
        }
    }
}
```

**abort-config:-** Abort Config is a config on how the OTA Job update should abort. Like in below if the thresholdPercentage met of OTA Type Failed the OTA Job will be abort.
```json
{
    "criteriaList": [ 
        { 
           "action": "CANCEL",
           "failureType": "FAILED",
           "minNumberOfExecutedThings": 5,
           "thresholdPercentage": 10
        }
     ]
}
```