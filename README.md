# DataGate

A serverless data pipeline built on AWS that automatically ingests CSV files uploaded to S3 and loads them into DynamoDB.

## Why this project

Built as a hands-on learning project after completing AWS Educate's Cloud 101 and AWS Management Console courses. The goal is to practice core data engineering concepts — ingestion, processing, and storage — using a small, real AWS pipeline rather than just reading about it.

## Architecture

```
Upload CSV --> S3 Bucket --> Lambda Trigger --> Process Rows --> DynamoDB Table
```

1. A CSV file is uploaded to an S3 bucket.
2. The upload event triggers a Lambda function.
3. Lambda reads the CSV, parses each row, and writes it to DynamoDB.
4. Data can then be queried directly from the DynamoDB console.

## AWS Services Used

- **S3** — raw file storage / ingestion point
- **Lambda** — serverless compute to process files (Python)
- **DynamoDB** — NoSQL database for processed records
- **IAM** — least-privilege permissions connecting the services
- **CloudWatch** — logs for debugging Lambda runs

## Project Structure

```
datagate/
├── README.md
├── lambda_function.py    # Lambda code: reads CSV from S3, writes to DynamoDB
├── iam_policy.json       # Least-privilege IAM policy for the Lambda role
└── sample_data.csv       # Small sample file for testing the pipeline
```

## Setup Steps

1. Create an S3 bucket (e.g. `datagate-uploads`).
2. Create a DynamoDB table (e.g. `DataGateRecords`) with partition key `id`.
3. Create a Lambda function, paste in `lambda_function.py`, and set the `TABLE_NAME` environment variable.
4. Attach the IAM policy in `iam_policy.json` to the Lambda's execution role.
5. Add an S3 trigger on the Lambda for `PUT` events on the bucket.
6. Upload `sample_data.csv` to the bucket and confirm records appear in DynamoDB.
7. Check CloudWatch Logs if anything doesn't work as expected.

## Status

- [ ] S3 bucket created
- [ ] DynamoDB table created
- [ ] Lambda function deployed
- [ ] S3 trigger connected
- [ ] IAM permissions set
- [ ] End-to-end test passed

## Notes / Learnings

_(Add reflections here as you go — what broke, what you'd do differently, what you learned.)_
