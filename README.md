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
