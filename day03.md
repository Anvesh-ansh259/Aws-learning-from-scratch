# AWS S3 (Simple Storage Service)

## Overview

Amazon S3 is a **scalable, secure, and highly available cloud storage service** provided by AWS. It allows you to store and retrieve **any amount of data from anywhere on the web**.

---

## S3 Buckets

### What are S3 Buckets?

* Containers for storing objects (files) in S3.
* Each bucket has a **globally unique name**.
* Acts like a top-level folder holding your data.

### Why Use S3 Buckets?

* Reliable and highly scalable storage solution.
* Common use cases:

  * Backup & restore
  * Data archiving
  * Website content storage
  * Big data analytics

### Key Benefits

* **Durability & availability:** High reliability for data storage.
* **Scalability:** Store/retrieve any amount of data without capacity concerns.
* **Security:** Encryption, access control, and audit logging.
* **Performance:** Optimized for high-speed data operations.
* **Cost-effective:** Pay based on usage and storage class.

---

## Creating & Configuring Buckets

### Creating an S3 Bucket

* Use AWS Console, CLI, or SDKs.
* Specify a **globally unique bucket name** and choose a **region**.

### Bucket Name Rules

* 3–63 characters
* Lowercase letters, numbers, periods, hyphens
* Must follow DNS conventions

### Bucket Properties

* **Versioning:** Keep multiple versions to prevent accidental deletion.
* **Permissions & Policies:** Control access using **IAM policies**.

---

## Uploading & Managing Objects

### Uploading Objects

* Methods: Console, CLI, SDK, HTTP upload.
* Each object has a **unique key (name)** within the bucket.

### Object Metadata & Properties

* Metadata: Content type, cache control, encryption, custom metadata.

### File Formats & Encryption

* Supports text, images, videos, etc.
* **Encryption options:** SSE-S3, SSE-KMS, SSE-C

### Lifecycle Management

* Define rules to transition or delete objects automatically.

### Multipart Uploads

* Split large files into parts for parallel upload.
* Enables **resumable uploads**.

### S3 Batch Operations

* Perform bulk operations like copying, tagging, or restoring large numbers of objects.

---

## Advanced Features

### S3 Storage Classes

* Different classes for cost/performance optimization.

### S3 Replication

* **CRR:** Disaster recovery & compliance.
* **SRR:** Resilience and low-latency access.

### S3 Event Notifications

* Trigger AWS Lambda, SQS, or SNS on object creation/deletion.

---

## Security & Compliance

### Bucket Security Considerations

* Properly configure policies, access controls, and encryption.
* Regularly audit access logs.

### Encryption

* **At rest:** SSE-S3, SSE-KMS, SSE-C
* **In transit:** SSL/TLS

### Monitoring

* Enable **access logging** and track unauthorized activity

---

## Management & Administration

* Bucket Policies: JSON rules defining access.
* IAM Roles: Fine-grained access and temporary credentials.
* APIs & SDKs: Programmatic management.
* CloudWatch: Monitor metrics and set alarms.
* Management Tools: AWS Console, CLI, SDKs, third-party tools.

---

## Troubleshooting & Error Handling

* Common Errors: Access denied, bucket not found, quota exceeded.
* Debugging: Use CloudTrail and S3 logs.
* Data Consistency & Durability: Understand replication and storage mechanisms.
* Recovering Deleted Objects: Versioning, event notifications, CRR.

---

# AWS S3 Interview Questions & Answers

1. **What is Amazon S3 and why is it used?**

   * S3 is a scalable, secure cloud storage service used to store and retrieve any amount of data from anywhere.

2. **Explain the concept of S3 buckets.**

   * Buckets are containers in S3 for storing objects. Each bucket has a unique name and acts as a top-level folder.

3. **What are the different S3 storage classes and their use cases?**

   * Standard: frequently accessed data
   * Standard-IA: infrequently accessed data
   * Glacier: archival and long-term storage

4. **How does S3 versioning work and why is it important?**

   * Versioning keeps multiple versions of an object, preventing accidental deletion or overwrites.

5. **Explain server-side encryption in S3 and its types.**

   * SSE-S3: AWS-managed keys
   * SSE-KMS: AWS KMS-managed keys
   * SSE-C: Customer-provided keys

6. **What is Cross-Region Replication (CRR) and when would you use it?**

   * CRR replicates objects automatically across regions for disaster recovery and compliance.

7. **How do you manage permissions for an S3 bucket?**

   * Using IAM roles, bucket policies, and ACLs for fine-grained access control.

8. **Explain lifecycle policies in S3.**

   * Automate moving objects to different storage classes or deleting them after a certain period.

9. **What are S3 Event Notifications and how can they be used?**

   * Notifications trigger actions like Lambda, SQS, or SNS when objects are created or deleted.

10. **Describe multipart uploads and their benefits.**

    * Allows large objects to be uploaded in parts for better performance and resumable uploads.

11. **How can you recover deleted objects in S3?**

    * Use versioning, event notifications, or CRR.

12. **What are common S3 errors and how do you troubleshoot them?**

    * Access denied: Check IAM policies
    * Bucket not found: Verify bucket name and region
    * Quota exceeded: Adjust storage limits

13. **How can you secure data in S3 at rest and in transit?**

    * At rest: SSE encryption
    * In transit: SSL/TLS encryption

14. **Explain the difference between S3 Standard, S3 IA, and S3 Glacier.**

    * Standard: frequent access
    * IA: infrequent access, lower cost
    * Glacier: archival storage, lowest cost

15. **How can S3 Batch Operations help in managing large datasets?**

    * Automates bulk tasks like copying, tagging, or deleting multiple objects efficiently.

---

# AWS S3 Scenario-Based Questions & Answers

1. **Scenario:** Store sensitive financial data with encryption at rest and in transit.

   * **Answer:** Use SSE-KMS for server-side encryption and enable SSL/TLS for data transfers.

2. **Scenario:** Frequent uploads of large video files.

   * **Answer:** Use multipart uploads and consider S3 Standard or S3 Intelligent-Tiering for cost optimization.

3. **Scenario:** Move older objects to lower-cost storage automatically.

   * **Answer:** Implement S3 lifecycle rules to transition data to S3 IA or Glacier after a defined period.

4. **Scenario:** Global access with low latency.

   * **Answer:** Use Cross-Region Replication and consider edge caching with CloudFront.

5. **Scenario:** Accidental deletion of an important object.

   * **Answer:** Recover using versioning or CRR.

6. **Scenario:** Tag 100,000 objects across multiple buckets.

   * **Answer:** Use S3 Batch Operations with a manifest file specifying the objects.

7. **Scenario:** Trigger Lambda on object upload.

   * **Answer:** Configure S3 Event Notification for the bucket to invoke the Lambda function on `s3:ObjectCreated:*` events.

8. **Scenario:** Receiving 'Access Denied' errors.

   * **Answer:** Check IAM policies, bucket policies, ACLs, and confirm correct credentials and region.
