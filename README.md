# Cloud-Nonce-Discovery-System

Finn Hobson - fh16413

## Deployment Instructions

If I had more time I would have liked to use AWS CloudFormation to automatically perform these deployment steps. 

1. Make sure that Boto 3 and AWS CLI are installed on your local machine.

2. On the IAM management console, create a new user. Tick the "Programmatic access" checkbox and attach the "AmazonEC2FullAccess" permissions policy. Access credentials should be generated for this user. Enter these credentials on the command line using the command "aws configure". If a user with these attributes already exists on your AWS account then this step can be skipped.

3. On the S3 management console, create a new S3 Bucket. Enter the name of this bucket on line 12 of the cnd_setup.py script.

4. On the IAM management console, create a new role and give it the "AmazonS3FullAccess" permissions policy. Enter the name of this role on line 13 of the cnd_setup.py script. This will allow the created EC2 instances to access the new S3 bucket.

5. On the Lambda management console, create a new Lambda Function. Select the language Python 3.7 and copy the code from the terminate_instances_lambda.py file into the Lambda code environment. Press the "Add Trigger" button and select "S3" from the dropdown menu. Select your new bucket from the "Bucket" dropdown menu and select "PUT" from the "Event type" dropdown menu. Make sure the "Enable trigger" checkbox is ticked and click "Add". Enter the name of this Lambda function on line 14 of the cnd_setup.py file.

6. Creating this Lambda function should automatically create a new IAM role. On the IAM management console, find this new role on the "Roles" page, click the "Attach policies" button and add the "AmazonEC2FullAccess" permissions policy. This will allow the Lambda function to terminate EC2 instances. 

7. My custom AMI has been made publicly accessible for ease of deployment. This AMI should already have Python 3 and the cnd_worker.py script downloaded on it.

8. The CND system can be run by executing the cnd_setup.py script on your local machine.
