# AWS LAB01 - Automate EC2 Instance Launch with Python (boto3)

In this lab, you'll learn how to launch an Amazon EC2 instance using Python and the `boto3` SDK. This is your first step into cloud automation using Python!

---

## 🎯 Objectives

By the end of this lab, you will:
- Understand how to configure AWS credentials for `boto3`
- Use Python to interact with EC2 APIs
- Launch a t2.micro EC2 instance in your default VPC
- Print out the instance ID and public DNS

---

## 🧰 Prerequisites

- AWS account and IAM user with EC2 permissions
- `aws configure` run at least once (to store credentials)
- Python 3.8+ and `boto3` installed

---

## 📁 Lab Files

```
Cloud-Automation/AWS/LAB01-EC2-Automation/
├── launch_ec2.py
├── requirements.txt
└── README.md
```

---

## 🚀 Getting Started

1. Navigate to the lab folder:
```bash
cd Cloud-Automation/AWS/LAB01-EC2-Automation/
```

2. Create and activate a virtual environment:
```bash
python -m venv .venv
source .venv/bin/activate
```

3. Install `boto3`:
```bash
pip install boto3
pip freeze > requirements.txt
```

---

## ✍️ Your Task

### 1. Write a script to launch EC2:
```python
import boto3

# Create EC2 resource
ec2 = boto3.resource('ec2', region_name='eu-west-1')

# Launch a t2.micro instance
instance = ec2.create_instances(
    ImageId='ami-0fe0b2cf0e1f25c8a',  # Amazon Linux 2023 AMI in eu-west-1
    MinCount=1,
    MaxCount=1,
    InstanceType='t2.micro',
    KeyName='your-key-name',  # Replace with your key pair
    TagSpecifications=[{
        'ResourceType': 'instance',
        'Tags': [{'Key': 'Name', 'Value': 'PythonLabEC2'}]
    }]
)[0]

print("Launching instance...")
instance.wait_until_running()
instance.reload()
print("Instance launched with ID:", instance.id)
print("Public DNS:", instance.public_dns_name)
```

### 2. Replace placeholders:
- Replace `your-key-name` with your actual EC2 key pair name.

---

## 🧪 Validation Checklist

✅ AWS credentials configured  
✅ Instance launched successfully (t2.micro)  
✅ Printed instance ID and public DNS  
✅ Script runs without error:
```bash
python launch_ec2.py
```

---

## 🧹 Cleanup
Terminate the instance manually in AWS Console or run:
```python
instance.terminate()
```

---

## 💬 What's Next?
Try [AWS LAB02 - S3 File Upload](../LAB02-S3-File-Upload/) to automate object storage tasks using Python.

---

## 🙏 Acknowledgments
Launching infrastructure with code is the essence of DevOps. Mastering `boto3` enables powerful automations across AWS.

Happy automating! ☁️🐍