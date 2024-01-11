# Report Creation using surveys using Serverless Application on AWS Cloud 
> Creating a report in .docx format having analysis based on chosen answers in a survey. A webpage is shown with a questionaire and a report gets generated after submission.

## Table of Contents

*[Problem Statement](#problem-statement)
*[AWS Solution Architecture](#aws-solution-architecture)
*[AWS Services Used](#aws-services-used)
*[Solution Steps](#solution-steps)
*[Contact](#contact)


## Problem Statement
Many times different teams like solution architects, data architects,TAMs etc takes surveys using multiple choice questions to get more insights in some related work of clients. Based on the answers provided by clients, a detailed report is created using this solution provided here which will help solution architects or managers proceed further with the client's use cases. The architecture is based on serverless application using AWS services.

## AWS Solution Architecture
![aws-solution-architecture]()

## AWS Services Used

1. Amazon Code Commit repository: It stores the code of the website and integrates with AWS Amplify.
2. AWS Amplify: AWS Amplify hosts the website for accessing over internet.
3. Amazon API gateway: Acts as API endpoint to communicate with backend infrastructure.
4. AWS Lambda handlers: AWS Lambda is used to fetch required information from Amazon DynamoDB, create a report in .docx format and save the file in Amazon S3 bucket.
5. Amazon DynamoDB: A NoSQL database used to store the recommendations and other metadata corresponding to a specific option for a survey question. 
6. Amazon S3: Amazon S3 bucket stores the detailed report and a presigned URL is created for downloading the document report file.

## Solution steps

1. Clients interact with the survey website via internet hosted on AWS Amplify.
2. Amazon code commit repository stores the website code and all changes made in the repository automatically builds the AWS amplify app. index.html file contains the application code.
3. The answers provided by clients are passed from AWS amplify via POST request to an API endpoint hosted on Amazon API gateway.
4. The POST request with answers payload is passed to AWS Lambda handlers for further processing.
5. AWS Lambda handler calls Amazon DynamoDB table to get the recommendations corresponding to chosen answer of a question and stores it in a variable. lambda-handler.py file contains the lambda code and Items folder contains the sample items of dymanoDB in JSON format. 
6. After processing, AWS Lambda creates a document report (.docx format) and saves it in S3 bucket.
7. AWS Lambda also creates a S3 presigned URL of S3 object for downloading the file.
8. AWS lambda handler passes the S3 presigned URL to API gateway.
9. API gateway in turn passes the S3 presigned URL to AWS Amplify and the link is displayed on website. When client clicks on Download link, the document gets downloaded to Local device storage.

Note: Please make sure that the lambda function has required permissions to access DynamoDB, S3 and API gateway. Also, S3 bucket policy should allow read and write operations from lambda.

## Contact
Created by [@A-yush] - feel free to contact me!
