# AWS CLI Notes with Interview Q&A

## What is AWS CLI?
- **AWS CLI (Command Line Interface)** is a unified tool to manage AWS services from the terminal or command prompt.
- It allows developers, system administrators, and DevOps engineers to **automate AWS tasks** using simple commands instead of navigating through the AWS Management Console.

---

## Why AWS CLI is Required?
1. **Automation** – Automate repetitive tasks using shell scripts.
2. **Faster execution** – Perform bulk operations faster than using the console.
3. **Integration** – Works well with CI/CD pipelines and automation tools.
4. **Flexibility** – Manage multiple AWS accounts and regions easily.
5. **Scripting Support** – Run commands in Bash, PowerShell, or Python scripts.
6. **Consistency** – Same commands work across environments, ensuring repeatability.

---

## AWS CLI Examples

### 1. Configure AWS CLI
```bash
aws configure
# Provide Access Key, Secret Key, Region, Output format
```

### 2. List all S3 Buckets
```bash
aws s3 ls
```

### 3. Upload a File to S3
```bash
aws s3 cp localfile.txt s3://my-bucket-name/
```

### 4. Download from S3
```bash
aws s3 cp s3://my-bucket-name/remote.txt local.txt
```

### 5. Launch an EC2 Instance
```bash
aws ec2 run-instances   --image-id ami-12345678   --count 1   --instance-type t2.micro   --key-name MyKeyPair   --security-groups MySecurityGroup
```

### 6. Describe Running Instances
```bash
aws ec2 describe-instances
```

### 7. Stop an Instance
```bash
aws ec2 stop-instances --instance-ids i-0123456789abcdef0
```

---

## AWS CLI Interview Questions with Answers

### Q1. What is AWS CLI and why is it used?
**Answer:** AWS CLI is a command-line tool to interact with AWS services. It is used for automation, faster execution of tasks, scripting, and integrating AWS with CI/CD pipelines.

---

### Q2. How do you configure AWS CLI?
**Answer:**
```bash
aws configure
```
You provide **Access Key, Secret Key, Default Region, and Output Format**.  
Credentials are stored in `~/.aws/credentials`.

---

### Q3. What’s the difference between AWS CLI and AWS SDK?
**Answer:**
- **AWS CLI**: Command-line tool for executing AWS commands.
- **AWS SDK**: Programming libraries for languages like Python (boto3), Java, Node.js, etc., to integrate AWS into applications.

---

### Q4. Can we use AWS CLI without IAM credentials?
**Answer:** No, AWS CLI requires IAM credentials (Access Key and Secret Key). However, you can also use temporary credentials from AWS STS or IAM roles when running CLI from EC2.

---

### Q5. How do you switch between multiple AWS profiles in AWS CLI?
**Answer:**
- Define profiles in `~/.aws/credentials` file.
- Use `--profile` option:
```bash
aws s3 ls --profile dev
aws s3 ls --profile prod
```

---

### Q6. What output formats are available in AWS CLI?
**Answer:**  
- **json** (default)  
- **text**  
- **table**  

Example:
```bash
aws ec2 describe-instances --output table
```

---

### Q7. How can you change the region while running an AWS CLI command?
**Answer:**  
Use `--region` flag in the command:
```bash
aws ec2 describe-instances --region us-west-2
```

---

### Q8. How is AWS CLI useful in CI/CD pipelines?
**Answer:**  
- Automates deployments, infrastructure provisioning, and resource management.  
- Integrates easily with tools like Jenkins, GitHub Actions, and GitLab CI.  
- Helps in scripting build, test, and deploy processes.

---

## Scenario-Based Interview Questions with Answers

### Q1. S3 Upload Scenario
**Question:** You need to upload 1,000 log files daily to an S3 bucket. How would you automate this using AWS CLI?  
**Answer:** Use the `aws s3 sync` command inside a cron job or script:
```bash
aws s3 sync /var/logs/ s3://my-log-bucket/ --delete
```

---

### Q2. IAM User Access
**Question:** You want to give a new developer CLI access but restrict them to only S3 operations. How will you configure this?  
**Answer:**  
- Create an IAM user and attach **AmazonS3FullAccess** or a custom S3-only policy.  
- Share the Access Key and Secret Key with the developer for AWS CLI configuration.  

---

### Q3. Multi-Region Deployment
**Question:** You have EC2 instances running in multiple regions. How would you use AWS CLI to list all instances across regions?  
**Answer:** Loop through all regions:
```bash
for region in $(aws ec2 describe-regions --query "Regions[*].RegionName" --output text); do
  echo "Listing instances in region: $region"
  aws ec2 describe-instances --region $region
done
```

---

### Q4. Cost Saving
**Question:** You want to stop all EC2 instances in non-production accounts every night. How would you achieve this with AWS CLI?  
**Answer:** Use a scheduled script (cron job) with:
```bash
aws ec2 stop-instances --instance-ids $(aws ec2 describe-instances   --filters "Name=tag:Environment,Values=Non-Prod"   --query "Reservations[*].Instances[*].InstanceId" --output text)
```

---

### Q5. Disaster Recovery
**Question:** Your application backup is stored in S3 in `us-east-1`. How would you use AWS CLI to copy the data to another region for DR purposes?  
**Answer:**
```bash
aws s3 sync s3://mybucket-us-east-1 s3://mybucket-us-west-2 --source-region us-east-1 --region us-west-2
```

---

### Q6. Profile Switching
**Question:** You have two AWS accounts (Dev and Prod). How do you use AWS CLI to run commands on both without re-configuring each time?  
**Answer:** Configure profiles in credentials file:
```bash
aws configure --profile dev
aws configure --profile prod
```
Run commands with:
```bash
aws s3 ls --profile dev
aws s3 ls --profile prod
```

---

### Q7. EC2 Health Check
**Question:** If an instance goes down, how would you quickly check its state using AWS CLI?  
**Answer:**
```bash
aws ec2 describe-instance-status --instance-id i-0123456789abcdef0
```
This shows running status, system checks, and health checks.

---

## Key Takeaways
- AWS CLI is a powerful tool for **automation and scripting**.  
- It supports **multi-account, multi-region** setups.  
- Frequently asked in **DevOps and Cloud Engineer interviews**.  
- Real-world scenarios often test your ability to write AWS CLI **scripts** for automation.
