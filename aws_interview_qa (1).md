# AWS Interview Questions and Answers

## 1. Explain EBS? What type of performance do you expect? How do you back it up? How do you improve its performance?

### Explanation:
**Amazon Elastic Block Store (EBS):**
- EBS provides block-level storage volumes for EC2 instances.
- It behaves like a virtual hard drive that you can attach to instances.
- Volumes are highly available, durable, and can be used for databases, file systems, or applications.

**Types of EBS Volumes and Performance Expectations:**
- **gp3 (General Purpose SSD):** Balanced price and performance, up to 16,000 IOPS.
- **io2/io2 Block Express (Provisioned IOPS SSD):** High-performance, designed for critical applications, up to 256,000 IOPS.
- **st1 (Throughput Optimized HDD):** For big data and sequential workloads.
- **sc1 (Cold HDD):** Lowest cost, for infrequent access.

**Backup of EBS:**
- Use **EBS Snapshots** stored in S3.
- Snapshots are incremental (only changed data is saved).
- You can automate backups using AWS Backup.

**Improving Performance:**
- Choose the right EBS type based on workload (e.g., io2 for databases).
- Enable **EBS-optimized instances** for dedicated bandwidth.
- Use **RAID 0** for striping across multiple volumes.
- Use **Provisioned IOPS** (io2) for consistent high performance.

---

## 2. CloudTrail and CloudWatch Retention

| Service                  | Default Retention              | Max Retention / Notes                         |
| ------------------------ | ------------------------------ | --------------------------------------------- |
| CloudTrail Event History | 90 days                        | For longer retention, store in S3             |
| CloudTrail S3 Logs       | Depends on S3 lifecycle        | Indefinite (you define lifecycle policies)    |
| CloudWatch Metrics       | 1 min: 15 days, 1 hr: 455 days | Fixed retention by AWS                        |
| CloudWatch Logs          | Never by default               | Configurable per log group (1 day → 10 years) |

### Explanation:
- **CloudTrail Event History** only keeps events for 90 days. For long-term auditing, you must send them to S3.
- **CloudTrail S3 Logs** stored in S3 can last forever, unless you set lifecycle rules to delete/transition them.
- **CloudWatch Metrics:**
  - 1-minute granularity data is stored for 15 days.
  - 5-minute granularity data is stored for 63 days.
  - 1-hour granularity data is stored for 455 days.
- **CloudWatch Logs:** By default, they are kept forever until you configure a retention period.

---

## 3. CloudWatch Metrics Retention (Detailed)

When you push metrics to **CloudWatch**, AWS automatically stores them with different resolutions:
- **1-minute resolution data points** → kept for 15 days.
- **5-minute resolution data points** → kept for 63 days.
- **1-hour resolution data points** → kept for 455 days.

This means AWS gradually aggregates old data into coarser granularity to save storage space.

---

## 4. How would you secure S3 data in transit and at rest for compliance?

### At Rest:
- Use **Server-Side Encryption (SSE):**
  - SSE-S3: Keys managed by AWS.
  - SSE-KMS: Keys managed with AWS KMS (recommended for compliance).
  - SSE-C: Customer-managed keys.
- Enable **Bucket encryption policy** to enforce encryption.

### In Transit:
- Enforce HTTPS (TLS) connections only.
- Example Bucket Policy to enforce TLS:
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Deny",
            "Principal": "*",
            "Action": "s3:*",
            "Resource": ["arn:aws:s3:::your-bucket/*"],
            "Condition": {"Bool": {"aws:SecureTransport": "false"}}
        }
    ]
}
```
- This denies all requests that are not using HTTPS.

### Easy Explanation:
- **TLS** = modern encryption protocol that secures communication between client and server.
- Without TLS → data could be intercepted.
- With TLS enforced via policy → bucket only accepts encrypted requests.

---

## 5. What is TLS?

**TLS (Transport Layer Security):**
- Cryptographic protocol that ensures **data confidentiality, integrity, and authenticity**.
- Secures communication between client and server.
- Successor of SSL.
- Example: When accessing `https://` websites, TLS encrypts the data in transit.

---

## 6. Explain CRR in S3 (Cross-Region Replication)

### Explanation:
- **CRR (Cross-Region Replication)** automatically replicates objects from one S3 bucket to another bucket in a **different AWS region**.
- Ensures high availability, disaster recovery, and compliance.
- Works asynchronously.
- Requires:
  - Versioning enabled on both source and destination.
  - Proper IAM permissions.

### Use Cases:
- Disaster recovery across regions.
- Latency reduction by keeping data closer to users.
- Compliance with regulatory requirements.

---

## 7. Interview Questions on Secure S3 and CRR

### Secure S3:
1. How do you secure S3 buckets at rest?
   - By enabling SSE (SSE-S3, SSE-KMS) and enforcing encryption policies.
2. How do you secure data in transit for S3?
   - Enforce TLS by bucket policy, allow only HTTPS requests.
3. How do you restrict public access to S3?
   - Use **Block Public Access** settings and IAM bucket policies.
4. How do you audit S3 access?
   - Enable **CloudTrail** and S3 access logs.

### CRR:
1. What is CRR in S3?
   - Cross-Region Replication replicates objects between S3 buckets in different regions.
2. What are the requirements for CRR?
   - Versioning enabled on source and destination.
3. Can you replicate existing objects with CRR?
   - No, CRR only replicates new objects after replication is enabled (existing ones need batch replication).
4. Can you apply CRR to a subset of objects?
   - Yes, using **prefixes** or **tags**.
5. What is the difference between SRR and CRR?
   - **SRR (Same-Region Replication):** Replicates within same region for compliance/logging.
   - **CRR:** Replicates across regions for DR, latency, compliance.

---

