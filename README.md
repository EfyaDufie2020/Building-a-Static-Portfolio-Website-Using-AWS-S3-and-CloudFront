# Building-a-Static-Portfolio-Website-Using-AWS-S3-and-CloudFront
# 🌐 Building a Static Portfolio Website Using AWS S3 and CloudFront

This project showcases a **static personal website** hosted on **Amazon S3**, secured using IAM, and globally accelerated with **CloudFront**.  

It includes an architecture diagram and a clean structure for learning or showcasing a portfolio.

---

## 🚀 Project Overview

This website displays your personal profile, skills, and projects using static HTML & CSS files.  

---

## 🎯 Objectives

- Build a static portfolio site using HTML and CSS
- Host it using S3 static website hosting (Free Tier)
- Secure AWS environment using IAM and MFA
- Use CloudFront for global performance and HTTPS

---

## 🏗️ Architecture Diagram

![Architecture](docs/architecture-diagram-static-website-on-s3.png)

---

### 🔑 Key Components

| Component          | Description                                                   |
|--------------------|---------------------------------------------------------------|
| **S3 Bucket**      | Stores static website files (HTML, images, CSS)              |
| **Bucket Policy**  | Public read-only access to website content                   |
| **IAM Setup**      | Least privilege IAM user and MFA on root account             |
| **CloudFront**     | Global CDN for fast delivery and HTTPS                       |
| **HTML Files**     | `index.html`, `error.html`, images                           |

---

## 🛠️ Prerequisites

- AWS account with [MFA enabled](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html)
- Basic HTML knowledge & AWS Console access
- Git (optional, for version control)

---

## 🪜 Steps to Deploy

### 1️⃣ Enable MFA on AWS Root

- Go to IAM → Enable MFA on root account for added security.

---

### 2️⃣ Create an IAM User

- Create a new IAM user (e.g., `s3-website-admin`).
- Select **Programmatic access**.
- Attach **custom policy** (example policy below) or use:
  - `AmazonS3FullAccess`
  - `CloudFrontFullAccess`
- Enable MFA on the user for extra security.

---

### 💡IAM Policy for Limited S3 + CloudFront

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets",
                "s3:GetBucketLocation",
                "s3:ListBucket",
                "s3:GetObject",
                "s3:PutObject",
                "s3:DeleteObject",
                "s3:PutBucketPolicy",
                "s3:GetBucketPolicy"
            ],
            "Resource": [
                "arn:aws:s3:::your-bucket-name",
                "arn:aws:s3:::your-bucket-name/*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "cloudfront:CreateInvalidation",
                "cloudfront:GetDistribution",
                "cloudfront:UpdateDistribution"
            ],
            "Resource": "*"
        }
    ]
}
