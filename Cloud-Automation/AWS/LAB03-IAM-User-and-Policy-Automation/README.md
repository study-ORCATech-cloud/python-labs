# AWS LAB03 - Automate IAM User and Policy Creation with Python (boto3)

In this lab, you'll learn how to automate the creation of IAM users and attach policies using Python and the `boto3` library. IAM automation is critical for managing access to AWS in a secure and scalable way.

---

## 🎯 Objectives

By the end of this lab, you will:
- Create an IAM user programmatically using `boto3`
- Attach an existing policy (e.g., `AmazonS3ReadOnlyAccess`)
- Optionally create and attach a custom inline policy
- List users to verify creation

---

## 🧰 Prerequisites

- AWS account with IAM permissions
- AWS credentials configured locally (`aws configure`)
- Python 3.8+ and `boto3` installed

---

## 📁 Lab Files

```
Cloud-Automation/AWS/LAB03-IAM-User-and-Policy-Automation/
├── create_iam_user.py
├── requirements.txt
└── README.md
```

---

## 🚀 Getting Started

1. Navigate to the lab folder:
```bash
cd Cloud-Automation/AWS/LAB03-IAM-User-and-Policy-Automation/
```

2. Create and activate a virtual environment:
```bash
python -m venv .venv
source .venv/bin/activate
```

3. Install dependencies:
```bash
pip install boto3
pip freeze > requirements.txt
```

---

## ✍️ Your Task

### 1. Create an IAM user:
```python
import boto3

username = 'devops-lab-user'
iam = boto3.client('iam', region_name='eu-west-1')

response = iam.create_user(UserName=username)
print(f"Created user: {response['User']['UserName']}")
```

### 2. Attach a managed policy:
```python
policy_arn = 'arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess'
iam.attach_user_policy(UserName=username, PolicyArn=policy_arn)
print("Attached AmazonS3ReadOnlyAccess policy")
```

### 3. List IAM users:
```python
users = iam.list_users()
for user in users['Users']:
    print(user['UserName'])
```

---

## 🧪 Validation Checklist

✅ IAM user created via Python  
✅ Policy attached successfully  
✅ User appears in `list_users()` result  
✅ Script runs without error:
```bash
python create_iam_user.py
```

---

## 🧹 Cleanup
You can delete the user with:
```python
iam.delete_user(UserName=username)
```

Note: Detach policies before deleting a user if required.

---

## 💬 What's Next?
Try [AWS LAB04 - CloudWatch Metrics and Alerts](../LAB04-CloudWatch-Metrics-and-Alerts/) to collect metrics and send alerts using Python.

---

## 🙏 Acknowledgments
Security automation is essential in DevOps. Mastering IAM management with Python opens doors to building secure cloud platforms.

Happy securing! 🛡🐍