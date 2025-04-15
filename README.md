**EC2 Auto-Restart Lambda with Boto3**


A simple AWS automation project using Python and Boto3 to monitor EC2 instance states and automatically start any stopped instances on a scheduled basis.



**Overview**


This project uses an AWS Lambda function triggered by a CloudWatch Events rule to:
-Check the status of specified EC2 instances
-Automatically start any instances that are stopped


It’s designed as a lightweight automation to ensure important instances stay available without manual intervention.



**Technologies Used:**
-AWS Lambda
-Amazon EC2
-CloudWatch Events (EventBridge)
-IAM Roles and Policies
-Python 3.x
-Boto3 (AWS SDK for Python)



**Architecture**

-Lambda Function: Contains Python logic using Boto3 to query EC2 states and start any stopped instances.
-CloudWatch Event Rule: Triggers the Lambda function on an hourly schedule.
-IAM Role: Provides the Lambda function permission to describe and start EC2 instances.



**Setup Instructions**

1. Clone the Repository (you can view the full lambda function and setup instructions below in this README. if you'd still like to clone the repo for reference):

```
git clone https://github.com//ec2-auto-restart-lambda.git
cd ec2-auto-restart-lambda
```



2. Deploy Lambda Function

You can deploy this function manually via the AWS Console or using the AWS CLI.

```python
import boto3

def lambda_handler(event, context):
    ec2 = boto3.resource('ec2')
    for instance in ec2.instances.all():
        state = instance.state['Name']
        if state == 'stopped':
             try:
                 instance.start()
             except:
                 print('something went wrong') 
```



3. Create CloudWatch Trigger

-Go to Amazon CloudWatch > Rules
-Create a new rule with a fixed rate of 1 hour
-Set the Lambda function as the target


4. IAM Permissions

Make sure the Lambda execution role has at least the following permissions:

```json
{
"Effect": "Allow",
"Action": [
"ec2:DescribeInstances",
"ec2:StartInstances"
],
"Resource": "*"
} 
```

**Future Improvements**
-Add notifications (e.g., via SNS) for action logs
-Add unit tests and logging


Author:
Jesse Ogbe
LinkedIn.com/in/JesseOgbe
[X: @h_u_n_cho]




