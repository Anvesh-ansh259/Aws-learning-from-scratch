# AWS Storage Services: EBS vs EFS vs S3

This document provides a comparison between **Amazon EBS (Elastic Block Store)**, **Amazon EFS (Elastic File System)**, and **Amazon S3 (Simple Storage Service)**.

---

## 1. Amazon EBS (Elastic Block Store)
- **Type**: Block storage
- **Use Case**: Persistent block-level storage for EC2 instances (like a virtual hard disk)
- **Max Volume Size**: Up to **16 TiB**
- **Max File Size**: Limited by the file system you format on EBS (e.g., ext4, XFS)
- **Performance**: High performance, low latency (good for databases, OS, applications)
- **Availability**: Tied to a single Availability Zone (AZ)
- **Durability**: Replicated within an AZ
- **Pricing**: Pay for provisioned storage

---

## 2. Amazon EFS (Elastic File System)
- **Type**: Managed NFS file system
- **Use Case**: Shared file storage for multiple EC2 instances, containers, and on-premises servers
- **Max Volume Size**: Virtually unlimited (scales automatically)
- **Max File Size**: Up to **47.9 TiB per file**
- **Performance**: Scales automatically with workload, supports thousands of concurrent connections
- **Availability**: Regional (spans multiple AZs)
- **Durability**: Data replicated across multiple AZs
- **Pricing**: Pay for storage used (elastic scaling)

---

## 3. Amazon S3 (Simple Storage Service)
- **Type**: Object storage
- **Use Case**: Store any type of object data (images, videos, backups, logs, static websites)
- **Max Volume Size**: Virtually unlimited (bucket can hold unlimited objects)
- **Max File Size**: Up to **5 TB per object**
- **Performance**: High durability, scalable throughput, eventual consistency (strong consistency for some operations)
- **Availability**: Regional (data replicated across multiple AZs by default)
- **Durability**: 99.999999999% (11 9’s)
- **Pricing**: Pay for storage, requests, and data transfer

---

## 📊 Quick Comparison Table

| Feature            | EBS                           | EFS                           | S3                          |
|--------------------|-------------------------------|-------------------------------|-----------------------------|
| **Type**           | Block Storage                 | File Storage (NFS)            | Object Storage              |
| **Max Volume Size**| 16 TiB                        | Virtually unlimited           | Virtually unlimited         |
| **Max File Size**  | Depends on FS (e.g., ext4/XFS)| 47.9 TiB per file             | 5 TB per object             |
| **Performance**    | Low latency, high IOPS        | Scales with workload          | High throughput, eventual consistency |
| **Availability**   | Single AZ                     | Multi-AZ (regional)           | Multi-AZ (regional)         |
| **Durability**     | Replicated within an AZ       | Replicated across AZs         | 11 9’s durability           |
| **Best For**       | Databases, OS, apps           | Shared file storage           | Backups, media, static sites|

---

## ✅ Summary
- Use **EBS** when you need block storage for **a single EC2 instance** (databases, applications).  
- Use **EFS** when you need **shared storage** accessible by multiple EC2 instances across AZs.  
- Use **S3** when you need **object storage** for large-scale, durable, and cost-effective storage (images, videos, backups, static hosting).  
