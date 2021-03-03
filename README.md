# AWS-Image-Scanner
# Used Amazon Web Services to create a python code that has the ability to describe the top 5 traits of a given image up to a 70% confidence level.

import json
import boto3

def lambda_handler(event, context):
    rekognition = boto3.client("rekognition")
    s3 = boto3.client("s3")
    fileObj = s3.get_object(Bucket= "name_of_bucket", Key="image_file_name")
    file_content = fileObj["Body"].read()
    response = rekognition.detect_labels(Image= {"S3Object" : {"Bucket" : "name_of_bucket", "Name": "image_file_name"}}, MaxLaels=5, MinConfidence=70)
    print(response)
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }
