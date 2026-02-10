# Baltimore Community Resource Finder

A serverless web application built on **AWS Free Tier** to help Baltimore residents find **food pantries**, **homeless shelters**, and **free medical clinics**.

## Overview

Provides a centralized resource directory for essential community services in Baltimore.

- Mobile-friendly static website
- Powered entirely by AWS managed services
- Designed to stay within the AWS Free Tier limits

## Architecture

- **Amazon S3** – Static site hosting  
- **Amazon CloudFront** – Global content delivery & caching  
- **Amazon DynamoDB** – NoSQL database for storing resources + metadata  
- **AWS Lambda** – Serverless backend logic for search and filtering  
- **Amazon API Gateway** – RESTful API endpoint  
- **AWS IAM** – Fine-grained security and permissions  
- **VPC + Internet Gateway** – Basic networking setup (usually default VPC)

## How It Works

1. User visits the website (hosted on S3 + CloudFront)  
2. Browser sends search/filter request to API Gateway  
3. API Gateway triggers the Lambda function  
4. Lambda queries DynamoDB for matching resources  
5. JSON results are returned and rendered dynamically in the browser

## Features

- Category-based and keyword search  
- Fully responsive web UI (works great on phones & desktops)  
- Public JSON API endpoint for flexibility / future integrations

## Setup Instructions

1. **S3**  
   - Create a bucket  
   - Enable **Static website hosting**  
   - Upload your `index.html` (and any CSS/JS/assets)  
   - Set public access / bucket policy as needed

2. **DynamoDB**  
   - Create a table named `CommunityResources`  
   - Define keys (example: partition key = `category`, sort key = `name`)  
   - Add sample resource items (food pantries, shelters, clinics, etc.)

3. **Lambda**  
   - Create a Python function  
   - Upload/deploy your backend code  
   - Set environment variable: `TABLE_NAME = CommunityResources`  
   - Give it a reasonable timeout (e.g. 30 seconds)

4. **API Gateway**  
   - Create a new **REST API**  
   - Add a resource `/search` with **GET** method  
   - Integrate it with your Lambda function  
   - Deploy the API and **enable CORS** (important for browser access)

5. **IAM**  
   - Attach policies to Lambda execution role:  
     - `AmazonDynamoDBReadOnlyAccess` (or custom least-privilege policy)  
     - `AWSLambdaBasicExecutionRole` (for CloudWatch Logs)

6. **Networking (VPC/IGW)**  
   - Usually not needed — use the default VPC  
   - If you added VPC config, confirm Internet Gateway and route tables allow outbound access

## Benefits

- **Scalable** — handles growth automatically  
- **Cost-effective** — stays free/low-cost with AWS Free Tier  
- **Reliable & serverless** — no servers to manage  
- **Secure** — controlled via IAM  
- **Accessible** — mobile-first design for community use

## Future Plans

- Add geo-location / map-based search  
- Enable user-submitted resource additions (with moderation)  
- Improve UI with better filtering & visuals  
- Set up CI/CD (e.g. GitHub Actions → AWS deployment)

Made with ❤️ for the Baltimore community.
