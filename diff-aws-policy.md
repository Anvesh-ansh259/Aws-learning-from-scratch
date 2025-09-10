
# IAM Policies in AWS: Inline, Custom, and AWS Managed

In AWS IAM, policies define **permissions** for users, groups, and roles.  
There are 3 main types: **Inline Policy**, **Customer Managed Policy**, and **AWS Managed Policy**.

---

## 1. Inline Policy
- **Definition**: Policy embedded *directly* into a single IAM user, group, or role.  
- **Scope**: Attached to **only one principal**.  
- **Use case**: When you want a permission that should **exist only with a specific identity**.  

### Example
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

---

## 2. Customer Managed Policy
- **Definition**: A standalone policy that **you create and manage** in your AWS account.  
- **Scope**: Can be attached to **multiple users, groups, or roles**.  
- **Use case**: When you want **reusable and customizable policies** across your organization.  

### Example
Custom policy named `S3ReadOnlyAccess`:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::my-bucket",
        "arn:aws:s3:::my-bucket/*"
      ]
    }
  ]
}
```

---

## 3. AWS Managed Policy
- **Definition**: Predefined policies created and maintained by AWS.  
- **Scope**: Read-only (you can attach but not edit).  
- **Use case**: For **common use cases** without having to write JSON policies manually.  

### Example
AWS provides a policy named `AmazonS3ReadOnlyAccess`:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:Get*",
        "s3:List*"
      ],
      "Resource": "*"
    }
  ]
}
```

---

## 🔑 Key Differences

| Feature              | Inline Policy                          | Customer Managed Policy                   | AWS Managed Policy               |
|----------------------|----------------------------------------|-------------------------------------------|----------------------------------|
| **Created by**       | You (inside a role/user/group)         | You                                       | AWS                              |
| **Reusability**      | ❌ Only for one identity                | ✅ Reusable across multiple identities     | ✅ Reusable across multiple identities |
| **Management**       | Tied to a single entity                | Centralized and manageable                | Managed/updated by AWS           |
| **Best for**         | Strict, one-off permissions            | Organization-specific reusable policies   | Common AWS use cases             |

---

✅ **Best Practice**:  
- Use **AWS Managed Policies** for standard permissions.  
- Use **Customer Managed Policies** for custom requirements.  
- Avoid Inline Policies unless you need a **tight one-to-one relationship**.
