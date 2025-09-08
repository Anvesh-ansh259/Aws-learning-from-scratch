# AWS IAM (Identity and Access Management)

## Overview

AWS IAM is a web service that helps securely control access to AWS resources. It allows you to manage users, groups, roles, and permissions in AWS.

---

## Key Concepts

### 1. IAM Users

* Represents individual people or applications.
* Each user has credentials to access AWS resources.

### 2. IAM Groups

* A collection of IAM users.
* Groups help assign the same permissions to multiple users easily.

### 3. IAM Roles

* Roles are similar to users but are intended to be **assumed by trusted entities** (e.g., AWS services, users from another account, or applications).
* Roles do not have long-term credentials; temporary credentials are provided when assumed.

### 4. IAM Policies

* JSON documents that define **permissions** (allow or deny) to AWS resources.
* Can be attached to users, groups, or roles.

### 5. Difference Between IAM, IAM Policy, Group, and Roles

| Concept    | Description                                  | Example                                      |
| ---------- | -------------------------------------------- | -------------------------------------------- |
| IAM User   | Individual identity with credentials         | An employee `John` with AWS console login    |
| IAM Group  | Collection of users sharing same permissions | `Developers` group with S3 read/write access |
| IAM Role   | Temporary credentials for trusted entities   | Lambda function assuming a role to access S3 |
| IAM Policy | JSON permission document                     | Allow EC2 start/stop or S3 read/write        |

---

## Interview Questions & Answers

1. **What is IAM?**

   * IAM is a service to manage access to AWS resources securely.

2. **What is an IAM policy?**

   * A JSON document that defines permissions to allow or deny actions on AWS resources.

3. **Difference between IAM user and IAM role?**

   * User: Permanent identity with long-term credentials.
   * Role: Temporary identity assumed by trusted entities.

4. **What is an IAM group?**

   * A collection of users with common permissions.

5. **Can you attach a policy to a group?**

   * Yes, attaching a policy to a group automatically applies it to all users in the group.

6. **Difference between managed and inline policy?**

   * Managed: Standalone policy that can be reused.
   * Inline: Embedded directly to a single user, group, or role.

7. **What is the difference between identity-based and resource-based policies?**

   * Identity-based: Attached to user, group, or role.
   * Resource-based: Attached to the resource itself (like S3 bucket policy).

---

## Scenario-Based Questions & Answers

1. **Scenario:** Grant an EC2 instance permissions to read from S3.

   * **Answer:** Create an IAM role with S3 read permissions and assign it to the EC2 instance.

2. **Scenario:** New developer joins the team and needs access to DynamoDB.

   * **Answer:** Add the user to a `Developers` group with a policy granting DynamoDB access.

3. **Scenario:** Lambda function needs to write logs to CloudWatch.

   * **Answer:** Create a role with CloudWatch write permissions and assign it to the Lambda function.

4. **Scenario:** You want to ensure a user cannot delete objects from an S3 bucket.

   * **Answer:** Attach a policy to the user or group denying `s3:DeleteObject` on the bucket.

5. **Scenario:** Allow a cross-account user to access your S3 bucket.

   * **Answer:** Create a role with trust policy for the external account and attach S3 access policy.

---

This markdown file summarizes IAM concepts, differences, interview questions, and scenario-based examples.
