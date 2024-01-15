# AWS
Resume-Parser-AWS-Event-Driven-Workflow
Prerequisite For Lambda Layer Creation:

![image](https://github.com/ashishraj2112/AWS/assets/92364203/9facd012-1a8f-4856-ab8d-c9e367361c07)


Commands on Ubuntu EC2 Instance:

sudo apt-get update
sudo apt install zip
mkdir -p build/python/lib/python3.10/site-packages
pip3 install PyMuPDF regex -t build/python/lib/python3.10/site-packages
zip -r pymupdf.zip build/
sudo apt install awscli
aws s3 cp pymupdf.zip s3://<path>
Steps:
![image](https://github.com/ashishraj2112/AWS/assets/92364203/dc089733-ea41-4a99-9fb6-ebbfaca84ad6)

image

Basic Idea :

When user uploads resume pdf file to S3 bucket,it triggers lambda function which parse the resume using fitz module and extracts basic information like contact number,Email id etc and puts it in DynamoDB table.After deleting file,it deletes that record from DynamoDB Table.Also it sends mail to subscribed users using SNS service.

Response For add & delete from S3 bucket:


s3 object add response
{'Records': [{'eventVersion': '2.1', 'eventSource': 'aws:s3', 'awsRegion': 'eu-north-1', 'eventTime': '2024-01-01T07:00:56.117Z', 'eventName': 'ObjectCreated:Put', 'requestParameters': {'sourceIPAddress': '<address>'}, 'responseElements': {'x-amz-request-id': '<id>', 'x-amz-id-2': 'id'}, 's3': {'s3SchemaVersion': '1.0', 'configurationId': '<id>', 'bucket': {'name': 'ashutosh-training', 'ownerIdentity': {'principalId': 'A2WPWP9O8UZRYM'}, 'arn': 'arn:aws:s3:::ashutosh-training'}, 'object': {'key': 'resume.pdf', 'size': 37, 'eTag': '<tag>', 'sequencer': '<val>'}}}]}

s3 object delete response

{'Records': [{'eventVersion': '2.1', 'eventSource': 'aws:s3', 'awsRegion': 'eu-north-1', 'eventTime': '2024-01-01T07:53:55.042Z', 'eventName': 'ObjectRemoved:Delete', 'userIdentity': {'principalId': '<id>'}, 'requestParameters': {'sourceIPAddress': '<ip>'}, 'responseElements': {'x-amz-request-id': '<id>', 'x-amz-id-2': '<id>'}, 's3': {'s3SchemaVersion': '1.0', 'configurationId': '<id>', 'bucket': {'name': 'ashutosh-training', 'ownerIdentity': {'principalId': '<id>'}, 'arn': 'arn:aws:s3:::ashutosh-training'}, 'object': {'key': 'resume.pdf', 'sequencer': 'id'}}}]}
