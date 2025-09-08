# AWS CLI (Command Line Interface)

## Overview

AWS CLI is a unified tool to manage AWS services from the command line. It allows you to **control multiple AWS services and automate tasks** using scripts.

---

## Key Features

* Execute AWS service commands directly from the terminal.
* Automate repetitive tasks with scripts.
* Supports all AWS services.
* Configure profiles for multiple accounts.
* Access AWS using access keys, IAM roles, or temporary credentials.

---

## Basic CLI Commands

| Service    | Command Example                  | Description             |
| ---------- | -------------------------------- | ----------------------- |
| S3         | `aws s3 ls`                      | List buckets or objects |
| EC2        | `aws ec2 describe-instances`     | Describe EC2 instances  |
| IAM        | `aws iam list-users`             | List all IAM users      |
| Lambda     | `aws lambda list-functions`      | List Lambda functions   |
| CloudWatch | `aws cloudwatch describe-alarms` | List CloudWatch alarms  |

### Configuring CLI

```
aws configure
```

* Prompts for Access Key ID, Secret Access Key, Region, Output format

### Using Profiles

```
aws s3 ls --profile dev
```

* Allows switching between multiple accounts/profiles.

### Command Options

* `--region` to specify region
* `--output` to specify output format (json, text, table)
* `--query` to filter results

---

## Interview Questions & Answers

1. **What is AWS CLI?**

   * A command-line tool to manage AWS services and automate tasks.

2. **How do you configure AWS CLI?**

   * Using `aws configure` and entering access key, secret key, region, and output format.

3. **Difference between AWS CLI and AWS SDK?**

   * CLI: Command-line interface.
   * SDK: Programmatic access through code in languages like Python, Java, etc.

4. **What are AWS CLI profiles?**

   * Profiles allow you to configure multiple accounts and switch between them using `--profile`.

5. **How can you list all S3 buckets using AWS CLI?**

   * `aws s3 ls`

6. **How to describe all EC2 instances?**

   * `aws ec2 describe-instances`

7. **How can you filter CLI output?**

   * Using `--query` option, e.g., `aws ec2 describe-instances --query 'Reservations[*].Instances[*].InstanceId'`

8. **How can you change the output format of AWS CLI?**

   * Using `--output json|text|table`

---

## Scenario-Based Questions & Answers

1. **Scenario:** You want to automate creating S3 buckets for a new project.

   * **Answer:** Use a shell script with `aws s3 mb s3://bucket-name` command.

2. **Scenario:** Need to list all EC2 instance IDs in a specific region.

   * **Answer:** `aws ec2 describe-instances --region us-east-1 --query 'Reservations[*].Instances[*].InstanceId' --output text`

3. **Scenario:** Switch between production and development AWS accounts.

   * **Answer:** Configure separate profiles with `aws configure --profile prod` and `aws configure --profile dev`, then use `--profile` flag.

4. **Scenario:** Delete all objects in a bucket using CLI.

   * **Answer:** `aws s3 rm s3://bucket-name --recursive`

5. **Scenario:** Download files from S3 bucket to local system.

   * **Answer:** `aws s3 cp s3://bucket-name/ ./local-dir --recursive`

6. **Scenario:** Check which IAM users exist in the account.

   * **Answer:** `aws iam list-users`

7. **Scenario:** Monitor CloudWatch alarms for specific metrics.

   * **Answer:** `aws cloudwatch describe-alarms --query 'MetricAlarms[*].AlarmName'`

---

This markdown summarizes AWS CLI, common commands, interview questions, and scenario-based examples.
