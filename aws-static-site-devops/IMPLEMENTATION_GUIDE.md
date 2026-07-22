# AWS Static Website CI/CD Pipeline
## Implementation Guide

This document provides the detailed implementation steps followed to build and deploy the AWS Static Website CI/CD Pipeline.

---

# Prerequisites

### Hardware

- MacBook

### Accounts

- AWS Account
- GitHub Account

---

# Environment Setup

## Install Git (Mac)

```bash
brew install git
git --version
```

---

## Install AWS CLI (Mac)

```bash
brew install awscli
aws --version
```

---

# AWS Configuration

## Create IAM User

Create IAM user:

```
devops-user
```

Attach policy:

```
AdministratorAccess
```

---

## Create Access Key

Generate an Access Key for the IAM user.

---

## Configure AWS CLI

```bash
aws configure
```

Provide:

- AWS Access Key
- AWS Secret Access Key
- Default Region (`us-east-1`)
- Output Format (`json`)

Verify the configuration:

```bash
aws s3 ls
```

---

# GitHub Repository

## Create Repository

Create the GitHub repository.

---

## Clone Repository

```bash
git clone https://github.com/<username>/aws-static-site-devops.git
```

---

# Website Development

## Create Static Website

Navigate to the project directory.

```bash
cd aws-static-site-devops
```

Create:

- `index.html`
- `style.css`

---

# Git Operations

## Commit Source Code

```bash
git init
git add .
git commit -m "Initial Website"
git remote -v
```

---

## Generate GitHub Personal Access Token

Generate a GitHub Personal Access Token with repository access.

---

## Push Source Code

```bash
git push -u origin main
```

Authenticate using:

- GitHub Username
- Personal Access Token

---

# Amazon S3

## Create S3 Bucket

Bucket Name:

```
aws-static-site-devops
```

Configuration:

- Enable Static Website Hosting
- Configure Index Document
- Disable Block Public Access
- Attach Bucket Policy

---

## Upload Website Files

```bash
aws s3 cp index.html s3://aws-static-site-devops/

aws s3 cp style.css s3://aws-static-site-devops/

aws s3 ls s3://aws-static-site-devops/
```

---

## Verify Website URL

Navigate to:

```
S3 Bucket
→ Properties
→ Static Website Hosting
```

Copy the Website Endpoint URL.

---

# Amazon CloudFront

## Create Distribution

Create a CloudFront Distribution.

Configuration:

- Origin: Amazon S3 Bucket
- Enable HTTPS
- Default Root Object:
  ```
  index.html
  ```

Deployment takes approximately:

```
10–15 minutes
```

Verify the Distribution Domain Name in the browser.

---

# GitHub Repository Secrets

Navigate to:

```
Repository
→ Settings
→ Secrets and Variables
→ Actions
```

Create the following Repository Secrets:

- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- AWS_REGION
- S3_BUCKET
- CLOUDFRONT_DISTRIBUTION_ID

---

# GitHub Actions

## Create Workflow

Create the workflow file:

```
.github/workflows/deploy-static-site.yml
```

---

## Verify Workflow

Navigate to:

```
Repository
→ Actions
```

Monitor the workflow execution.

---

## Issue Encountered

Issue:

```
Incorrect CloudFront Distribution ID
```

Resolution:

- Updated the Distribution ID
- Re-ran the deployment workflow

---

# CI/CD Validation

Modify any content in:

```
index.html
```

Commit and push the changes.

Verify:

- GitHub Actions completes successfully
- Updated content is reflected on the CloudFront URL

---

# Cleanup

## Amazon CloudFront

- Disable the CloudFront Distribution
- Wait until the status changes to **Deployed**
- Delete the Distribution

---

## Amazon S3

- Empty the S3 Bucket
- Delete the S3 Bucket

---

## IAM

Delete the IAM User.

---

## GitHub

Delete the Repository Secrets.

---

# Project Summary

This implementation demonstrates:

- Git & GitHub
- GitHub Actions
- AWS CLI
- Amazon S3 Static Website Hosting
- Amazon CloudFront
- AWS IAM
- CI/CD Pipeline Automation
