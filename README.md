  Baltimore-Community-Resource-Finder
A serverless web application built on AWS Free Tier to help Baltimore residents find food pantries, homeless shelters, and free medical clinics.

Overview
Provides a centralized resource directory
Mobile-friendly static website
Powered by AWS managed services

Architecture
Amazon S3 – Static site hosting
Amazon CloudFront – Content delivery
DynamoDB – Resource storage (services + metadata)
Lambda – Backend logic for search/filter
API Gateway – REST API entry point
IAM – Security and permissions
VPC + IGW – Baseline networking context

How It Works
User opens website hosted on S3/CloudFront
Website calls API Gateway with search request
API Gateway invokes Lambda
Lambda queries DynamoDB for resources
JSON results returned and displayed in browser

Features
Category & keyword search
Responsive web UI
JSON API for flexibility

Setup
S3 → Host index.html
DynamoDB → Create CommunityResources table with sample items
Lambda → Deploy Python code; set TABLE_NAME=CommunityResources
API Gateway → Add GET /search route; enable CORS
IAM → Attach DynamoDB + CloudWatch policy to Lambda role
VPC/IGW → Confirm default VPC available

Benefits
Scalable, cost-effective, reliable, secure, and accessible

Future Plans
Geo-location search
User submissions
Enhanced UI
CI/CD pipeline
