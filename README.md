# Cloudtrail Logs -> S3 -> Lambda -> AWS Elasticsearch Service

Automagically put your cloudtrail logs into Amazon Elasticsearch Service! and get a nice Kibana interface for it ;)

Cloudtrail, we all need it, and hey, its fairly easy to check stuff on the console.
Now, if you have multiple AWS accounts, it starts to get hairy, nobody wants to keep jumping over account consoles for that right?

Enter automation to save your skin!

## Requirements

- basic knowledge of all the aws services involved (s3, lambda, elasticsearch, cloudtrail)
- cloudtrail already set to store logs in an s3 bucket
- elasticsearch cluster ready

## Steps

Assuming some basic knowledge of the services involved.

- clone this repo
- on your terminal, install the requests module on the same folder with ```pip install requests -t .```
- edit s3_lambda_es.py changing the following variables
  - host = the full hostname for your AWS ES endpoint
  - region = region were your ES cluster is located
  - access_key and secret_key = a key pair to sign your requests to ES
- put the elastic_search_cloudtrail_template.json file contents on your ES cluster
- create a new lambda function
  - for uploading the code zip this entire folder and upload away (can keep readme, elastic_search_cloudtrail_template.json and .gitignore out). Very important! The files must be on the root of the zip, not inside a folder.
  - handler for the function is s3_lambda_es.lambda_handler
  - lambda role must allow access to the cloudtrail s3 bucket, and to create logs on cloudwatch
- on s3 create an event for ObjectCreated (All) pointing to the lambda function
- done! go check your kibana now and see the data flowing in ;)

## Notes

I have a more detailed post on [my blog](https://www.fernandobattistella.com.br/log_processing/2016/03/13/Cloudtrail-S3-Lambda-Elasticsearch.html).

## Issues

On lambda web console, in the monitoring tab, theres a link for its logs on cloudwatch, if anything blows, its gonna show there.
