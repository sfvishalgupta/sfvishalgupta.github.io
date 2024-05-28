#### [Back](./README.md)

# Amazon App Flow

Amazon AppFlow is a fully managed integration service that enables you to securely transfer 
data between Software-as-a-Service (SaaS) applications like Salesforce, SAP, Zendesk, Slack, 
and ServiceNow, and AWS services like Amazon S3 and Amazon Redshift, in just a few clicks. 
With AppFlow, you can run data flows at enterprise scale at the frequency you choose — on a schedule, 
in response to a business event, or on demand. You can configure data transformation capabilities like 
filtering and validation to generate rich, ready-to-use data as part of the flow itself, 
without additional steps. AppFlow automatically encrypts data in motion, 
and allows users to restrict data from flowing over the public Internet for SaaS applications that are 
integrated with AWS PrivateLink, reducing exposure to security threats.

**Integration of Salesforce with App Flow:-**

1. First we need to setup App Flow for which first we need to create a connector between Salesforce and AWS account. (For Connector we need a special user who has access to create a connection between salesforce and AWS).
2. App Flow will send data to our EventBridge Event via EventBridge Bus.
3. AWS Cloudwatch Event will call the lambda function.
