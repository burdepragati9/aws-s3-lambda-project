# 🚀 AWS S3 + Lambda + SNS Project

## 📌 Project Overview
This project demonstrates an **event-driven architecture** using AWS services.  
It automatically processes files uploaded to Amazon S3 using AWS Lambda and sends notifications via Amazon SNS.

---

## 🧠 Architecture Flow

1. User uploads a file to **Source S3 Bucket**
2. **AWS Lambda** is triggered automatically
3. Lambda:
   - Copies file to **Destination S3 Bucket**
   - Checks file size
4. If file size < 1MB:
   - Sends email notification using **Amazon SNS**

---

## 🛠️ Technologies Used

- AWS S3 (Storage)
- AWS Lambda (Serverless Compute)
- Amazon SNS (Notification Service)
- Python (Lambda Function)
- Git & GitHub (Version Control)

---

## 📂 Project Structure

aws-s3-lambda-project/
│
├── lambda_function.py # Main Lambda logic
├── README.md # Project documentation


---

## ⚙️ Setup Instructions

### 1️⃣ Create S3 Buckets
- Create two buckets:
  - Source Bucket
  - Destination Bucket

---

### 2️⃣ Create SNS Topic
- Create a topic
- Add email subscriptions
- Confirm emails

---

### 3️⃣ Create Lambda Function
- Runtime: Python 3.x
- Add S3 trigger (source bucket)

---

### 4️⃣ Attach Permissions
Attach these policies to Lambda role:
- AmazonS3FullAccess
- AmazonSNSFullAccess

---

### 5️⃣ Add Lambda Code

```python
import boto3

s3 = boto3.client('s3')
sns = boto3.client('sns')

DEST_BUCKET = 'your-destination-bucket'
TOPIC_ARN = 'your-sns-topic-arn'

def lambda_handler(event, context):

    bucket = event['Records'][0]['s3']['bucket']['name']
    key = event['Records'][0]['s3']['object']['key']

    response = s3.head_object(Bucket=bucket, Key=key)
    size = response['ContentLength']

    s3.copy_object(
        Bucket=DEST_BUCKET,
        CopySource={'Bucket': bucket, 'Key': key},
        Key=key
    )

    if size < 1048576:
        sns.publish(
            TopicArn=TOPIC_ARN,
            Message=f"{key} is less than 1MB",
            Subject="File Alert"
        )

    return "Success"
