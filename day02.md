# 📘 Day 2 – EC2 Backup, EBS, and EFS (Complete Notes)

---

## Why Backup is Needed
Backups protect **data loss due to accidental deletion, OS crash, or application failure**. Snapshots and AMIs ensure **recoverability and easy duplication** of EC2 instances or EBS volumes.

---

## Amazon Machine Image (AMI)
**Definition:** AMI is a **pre-configured template** containing **OS, applications, and configuration settings**. It allows you to **launch identical EC2 instances quickly** without manual setup.  

**How to create an AMI:**  
1. EC2 Dashboard → Instances → Select Instance → Actions → Image and templates → Create Image  
2. Enter **Name/Description**, select **No Reboot** if required  
3. Click **Create Image**  
4. Check **AMIs** section to see the new image

---

## EBS Snapshot
**Definition:** A **snapshot** is a point-in-time backup of an **EBS volume**, stored in S3. It protects data, allows volume restoration, and can be used to create new volumes.  

**How to create a snapshot:**  
1. EC2 → Elastic Block Store → Volumes → Select Volume → Actions → Create Snapshot  
2. Enter **Name/Description**, click **Create Snapshot**  
3. Monitor progress in **Snapshots** section

---

## Difference between AMI and Snapshot
| Feature         | AMI                                  | Snapshot                       |
|-----------------|-------------------------------------|--------------------------------|
| Definition      | Template for EC2 (OS + apps)        | Backup of an EBS volume        |
| Purpose         | Launch multiple identical instances | Backup or restore data         |
| Contains        | OS, software, configuration          | Data only                      |
| Usage           | Quick deployment of EC2 instances   | Recovery, clone volumes        |
| Example         | AMI of a configured web server      | Snapshot of database volume    |

---

## Attaching an EBS Volume
**Definition:** Adding extra storage to an EC2 instance.  

**Steps:**  
1. EC2 → Volumes → Select Volume → Actions → Attach Volume  
2. Choose **Instance**, specify **Device Name**, click **Attach**  
3. On the EC2 instance:  
```bash
lsblk                       # Check volume detected
sudo mkfs -t ext4 /dev/xvdf # Format if new
sudo mkdir /mnt/newvolume
sudo mount /dev/xvdf /mnt/newvolume

# 📘 Day 2 – EBS, EFS, and Storage Concepts

---

## EBS (Elastic Block Store) Types
| Volume Type                   | Use Case                                      |
|-------------------------------|-----------------------------------------------|
| General Purpose SSD (gp2/gp3) | Balanced workloads (web apps, small DB)      |
| Provisioned IOPS SSD (io1/io2)| High-performance DB, low latency             |
| Throughput Optimized HDD (st1)| Big data, streaming, sequential workloads    |
| Cold HDD (sc1)                | Infrequent access, archival                   |

**Extra Points:**  
- EBS volumes support **encryption via AWS KMS**, ensuring **data security and compliance**.

---

## Amazon EFS (Elastic File System)
**Definition:** Managed **NFS-based file system**, mountable on multiple EC2 instances simultaneously. Scales automatically with storage usage.  

**Performance Modes:**  
- **General Purpose:** Default, low latency  
- **Max I/O:** High throughput, more connections, slightly higher latency  

**How to attach EFS to EC2:**  
1. Create EFS in VPC  
2. Configure Security Group to allow **NFS port 2049**  
3. On EC2:
```bash
sudo yum install -y nfs-utils
sudo mkdir /mnt/efs
sudo mount -t nfs4 <EFS-DNS>:/ /mnt/efs


# 📘 Day 2 – EBS, EFS, and Storage Concepts

---

## EBS (Elastic Block Store) Types
| Volume Type                   | Use Case                                      |
|-------------------------------|-----------------------------------------------|
| General Purpose SSD (gp2/gp3) | Balanced workloads (web apps, small DB)      |
| Provisioned IOPS SSD (io1/io2)| High-performance DB, low latency             |
| Throughput Optimized HDD (st1)| Big data, streaming, sequential workloads    |
| Cold HDD (sc1)                | Infrequent access, archival                   |

**Extra Points:**  
- EBS volumes support **encryption via AWS KMS**, ensuring **data security and compliance**.

---

## Amazon EFS (Elastic File System)
**Definition:** Managed **NFS-based file system**, mountable on multiple EC2 instances simultaneously. Scales automatically with storage usage.  

**Performance Modes:**  
- **General Purpose:** Default, low latency  
- **Max I/O:** High throughput, more connections, slightly higher latency  

**How to attach EFS to EC2:**  
1. Create EFS in VPC  
2. Configure Security Group to allow **NFS port 2049**  
3. On EC2:
```bash
sudo yum install -y nfs-utils
sudo mkdir /mnt/efs
sudo mount -t nfs4 <EFS-DNS>:/ /mnt/efs


Interview Questions & Answers
For Freshers

Q1. Why do we need snapshots or AMIs?

Backup data, enable recovery, deploy identical EC2 instances

Q2. How to create an AMI?

EC2 → Select Instance → Actions → Create Image → Name → Create

Q3. How to create a snapshot?

Volumes → Select → Actions → Create Snapshot → Name → Create

Q4. Difference between AMI and snapshot?

AMI → Template (OS + apps), Snapshot → Backup of EBS volume

Q5. What is EFS and why use it?

Managed, scalable NFS file system for multiple EC2 instances

Q6. Difference between EBS and EFS?

EBS → single-instance block storage, EFS → multi-instance file storage

For Experienced

Q1. When to use AMI vs Snapshot?

AMI → Launch multiple identical EC2 instances

Snapshot → Backup EBS volume for recovery or cloning

Q2. How to mount EFS?

Create EFS → Allow NFS traffic → Mount via EC2

Q3. When to choose EFS over EBS?

Shared storage across multiple EC2 instances

Q4. Precautions before upgrading live EC2?

Take EBS snapshot or create AMI for rollback

Q5. Difference in encryption?

Both EBS and EFS support AWS KMS encryption

Scenario-Based Questions

Scenario 1: Launch 10 identical web servers quickly

Create AMI of configured server → Launch remaining servers

Scenario 2: Backup database before upgrade

Take EBS snapshot

Scenario 3: Multiple EC2 instances need same files

Use EFS mounted on all instances

Scenario 4: Add extra storage to EC2

Attach EBS volume, format, mount

Scenario 5 (Assignment):

Create EFS, attach to EC2, mount at /mnt/efs

Compare EBS vs EFS performance, scaling, and use case