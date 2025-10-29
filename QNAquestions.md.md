# DevOps Interview Q&A

*(Categorized --- AWS / Linux / Git / Jenkins / Others)*

✅ Total Questions: **79**

## AWS

### 1) What is VPC Peering?

VPC Peering connects two VPCs privately using AWS backbone network so
that resources communicate using private IPs.\
No transitive communication (A↔B, B↔C ≠ A↔C).

### 2) What is Transit Gateway (TGW)?

A Transit Gateway acts like a **central hub** to connect multiple VPCs,
VPNs, and on-prem networks.\
✅ Supports transitive routing.

### 3) Can we attach EBS volume to multiple instances?

No, except **EBS Multi-Attach (io1/io2)** volumes to multiple instances
in the same AZ.

### 4) What is CloudFormation?

An AWS IaC tool to provision AWS resources using YAML/JSON templates.

### 5) Public Key vs Private Key?

  Key           Purpose
  ------------- ----------------------------------------
  Public Key    Shared, used to encrypt
  Private Key   Secret, used to decrypt & authenticate

### 6) Difference: S3 vs Glacier

  Feature          S3                Glacier
  ---------------- ----------------- ----------------
  Use case         Frequent access   Archival
  Retrieval time   ms                Minutes--hours
  Cost             Higher            Very low

### 7) Can you increase root volume without shutting down instance?

✅ Yes --- using EBS Modify Volume.

### 8) How to make application highly available?

-   Multi-AZ
-   Load Balancer
-   Auto Scaling
-   Health checks

### 9) Explain Primary & Secondary IP

Primary = main IP\
Secondary = additional IP

### 10) How to attach a secondary IP?

EC2 → Networking → Assign IPv4

### 11) Can ENI attach to another VPC?

❌ No.

### 12) What is ENI?

Elastic Network Interface.

### 13) What is WAF?

Web Application Firewall for L7 protection.

### 14) Scheduled scaling example

Predictable usage like office timing.

### 15) Cross-account access

IAM Role + External ID.

### 16) Audit IAM users & roles

-   IAM Access Analyzer
-   Credential Report
-   CloudTrail

### 17) Private EC2 downloading without NAT?

Use VPC endpoints.

### 18) Explain EBS

Performance: IOPS\
Backup: Snapshot

### 19) Secure S3 data

-   TLS in-transit
-   SSE at-rest

### 20) CRR

Cross Region Replication.

### 21) Shrink EBS?

❌ No.

### 22) Custom vs Inline policy

Inline → single entity\
Custom → reusable

### 23) Check port 80

    sudo lsof -i:80

### 24) SNS vs SQS

SNS push\
SQS pull

### 25) Change Private IP of EC2 while running?

Primary ❌\
Secondary ✅

### 26) Internet needed for VPC peering?

❌ No.

### 27) Modify VPC route table?

✅ Yes.

### 28) AMI & Instance relation

AMI = template\
Instance = compute

### 29) EC2 Security Best Practices

Encrypt, Roles, SG, Patch.

### 30) EC2 connection issues

SG/NACL/Key mismatch.

### 31) AWS Storage Types

EBS, EFS, S3, FSx.

### 32) Purchasing Options

On‑Demand, Spot, RI.

### 33) CloudTrail vs SNS

Trail = logs\
SNS = notifications

### 34) Log retention

CloudTrail = 90 days\
CloudWatch = configurable

### 35) Move S3 cross‑account

Use replication or sync.

## Linux

### 36) Check system health

top, sar, systemctl

### 37) Inode

Metadata index.

### 38) Foreground vs Background

FG blocks terminal\
BG uses &

### 39) Environment Variable

Key‑value pair.

### 40) Zombie vs Orphan

Zombie = not reaped\
Orphan = parent died

### 41) Ping/traceroute troubleshoot

Check DNS/route.

### 42) Boot failure

Check grub, kernel, fstab.

### 43) Mount/unmount

mount / umount

### 44) Memory leaks

top, ps, logs.

### 45) Highest memory process

    ps aux --sort=-%mem

### 46) Check port

ss -ltnp

### 47) Linux file management

Everything is file; inode index.

## Git

### 48) Recover deleted branch

    git reflog

### 49) Detached head

HEAD → commit.

### 50) TXT record

DNS metadata.

### 51) Conflicts

Fix → add → commit.

### 52) Snapshot vs Backup

Snapshot = block level\
Backup = full copy

### 53) Fork vs Clone

Fork = server copy\
Clone = local copy

### 54) Fast‑forward merge

Pointer move only.

### 55) Best practices

Small commits.

### 56) Alias

    git config --global alias.co checkout

### 57) How many HEADs?

1 active.

### 58) Lock branch

Branch protection.

## Jenkins

### 59) CI/CD

SCM → Build → Deploy

### 60) Stages

Build/Test/Deploy

### 61) Parallel

parallel {}

### 62) Shared library

Reusable pipeline funcs.

### 63) Security

RBAC, credentials.

### 64) Credentials

Store secrets.

### 65) Build types

Freestyle, Pipeline.

### 66) Pass parameters

parameters {}

### 67) Configure Jenkins

Manage Jenkins → System.

### 68) JFrog

Artifact store.

### 69) Gearman plugin

Distribute builds.

### 70) Rollback

Redeploy previous.

## Others

### 71) \$0, $$, $?
$0 script  
$$ pid

\$? status

### 72) set -x, set -n

-x debug\
-n syntax only

### 73) Stash vs Squash

Stash temp\
Squash combine

### 74) Git architecture

Working → Index → Repo

### 75) EC2 migrate region

AMI copy → launch.

### 76) Lambda env vars

Key‑value settings.

✅ Total = 79 questions
