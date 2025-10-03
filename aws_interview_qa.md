### AWS Interview Questions and Answers

---

#### 1. Can we attach an EBS volume to multiple instances?
**Answer:**
- Standard EBS volumes can only be attached to **one EC2 instance at a time**.
- **EBS Multi-Attach** is available for **provisioned io1/io2 volumes**, allowing the volume to be attached to **multiple instances in the same Availability Zone**.
- Applications must be designed to **handle concurrent writes** to prevent data corruption.

---

#### 2. How can we access an S3 bucket privately without exposing it to the Internet?
**Answer:**
- Use a **VPC Gateway Endpoint for S3** to provide private connectivity from your VPC.
- Update the **bucket policy** to allow access **only from your VPC endpoint ID**.
- This ensures that traffic **does not traverse the public internet**.

---

#### 3. How many VPCs can we create in a single AWS region?
**Answer:**
- By default, AWS allows **5 VPCs per region**.
- This quota can be increased by submitting a **service quota request**.

---

#### 4. What are the types of Auto Scaling in AWS?
**Answer:**
- **Dynamic Scaling:** Adjusts EC2 capacity automatically based on **real-time metrics** like CPU utilization or network traffic.
- **Scheduled Scaling:** Adjusts capacity based on a **predefined schedule**, useful for predictable traffic patterns.
- **Predictive Scaling:** Uses **machine learning** to forecast traffic trends and scales EC2 capacity in advance.

---

#### 5. What is CloudFormation in AWS?
**Answer:**
- AWS **CloudFormation** is an **Infrastructure as Code (IaC)** service.
- It allows you to **provision and manage AWS resources** using JSON or YAML templates.
- Ensures **repeatable deployments** and version control of infrastructure.

---

#### 6. What is the difference between a public key and a private key?
**Answer:**
- **Public Key:** Shared openly and used to **encrypt data**.
- **Private Key:** Kept secret and used to **decrypt data**.
- Together they enable **secure asymmetric encryption** for communication and authentication.

---

#### 7. What is the difference between S3 and Glacier?
**Answer:**
| Feature | S3 | Glacier |
|---------|----|---------|
| Use Case | Frequently accessed data | Long-term archival storage |
| Cost | Higher | Lower |
| Retrieval Time | Milliseconds | Minutes to hours |
| Durability | 11 nines (99.999999999%) | 11 nines (99.999999999%) |
| Storage Classes | Standard, Standard-IA, Intelligent-Tiering, etc. | Glacier Flexible Retrieval, Deep Archive |

---

#### 8. What does regulatory compliance (7–10 years data storage) mean?
**Answer:**
- Certain industries require **long-term storage of data or logs** for auditing purposes.
- AWS services like **S3 Glacier or Deep Archive** allow organizations to implement **retention policies** to meet compliance requirements for 7–10 years.

---

#### 9. What are the different S3 storage classes and their differences?
| Storage Class | Use Case | Retrieval Time | Cost |
|---------------|---------|----------------|------|
| S3 Standard | Frequently accessed data | Milliseconds | High |
| S3 Standard-IA | Infrequently accessed data | Milliseconds | Lower |
| S3 One Zone-IA | Infrequent access, single AZ | Milliseconds | Lower |
| S3 Intelligent-Tiering | Variable access patterns | Milliseconds | Auto-optimizes cost |
| S3 Glacier Instant Retrieval | Archive, instant retrieval | Milliseconds | Low |
| S3 Glacier Flexible Retrieval | Archive, flexible retrieval | Minutes to hours | Very Low |
| S3 Glacier Deep Archive | Long-term archival | Up to 12 hours | Lowest |

---

#### 10. How do you make an application highly available?
**Answer:**
- Deploy instances across **multiple Availability Zones (multi-AZ)**.
- Use a **load balancer** (ALB/NLB) to distribute traffic evenly.
- Implement **Auto Scaling** to adjust capacity automatically.
- Use **multi-region replication** for critical applications to handle region-wide failures.

---

#### 11. Explain primary and secondary IP addresses.
**Answer:**
- **Primary IP:** The main IP of an ENI (Elastic Network Interface), automatically assigned, used for default communication.
- **Secondary IP:** Additional IPs assigned to the same ENI for hosting multiple applications, SSL certificates, or failover purposes. They can be added or removed as needed.

---

#### 12. How do you attach a secondary IP to an EC2 instance?
**Answer:**
- **AWS Console:** ENI → Manage IP addresses → Add secondary IP.
- **CLI:** `aws ec2 assign-private-ip-addresses --network-interface-id eni-xxxx --private-ip-addresses 10.0.0.25`
- **Linux:** `sudo ip addr add 10.0.0.25/24 dev eth0`

---

#### 13. How can you modify the primary IP of an EC2 instance?
**Answer:**
- **Direct modification of the primary IP is not allowed.**
- Options:
  1. Detach the ENI, assign a new primary IP, and reattach it.
  2. Create a new ENI with the desired primary IP and attach it.
  3. For public IP changes, use an **Elastic IP**.

---

#### 14. What is an ENI (Elastic Network Interface) and why do we use it?
**Answer:**
- A **virtual network card** that can be attached to an EC2 instance.
- Features include: primary and secondary IPs, security groups, MAC address.
- Use Cases:
  - High availability and failover
  - Multiple IPs for applications
  - Traffic and security isolation
  - Managing public and private IP access

---

#### 15. What is AWS WAF and why is it used?
**Answer:**
- AWS **Web Application Firewall (WAF)** protects web applications from **common web attacks** like SQL injection, XSS, and HTTP floods.
- Integrates with **CloudFront, ALB, API Gateway**.
- Provides customizable rules, managed rule groups, rate limiting, and logging for security.

---

#### 16. Explain scheduled scaling vs dynamic scaling with an example.
**Answer:**
- **Scheduled Scaling:** Scales EC2 based on a **predefined schedule**, suitable for predictable traffic peaks.
- **Dynamic Scaling:** Reacts to **real-time metrics** for unpredictable traffic.
- **Example:** Tirupati Darshan booking system releases slots every month on 23rd or 24th from 10 AM to 12 PM. Scheduled scaling can increase instances in advance to handle predictable traffic.
- Combination: Scheduled scaling handles known peaks; dynamic scaling handles unexpected spikes.

---

#### 17. How do you grant cross-account access to a partner?
**Answer:**
- **Use an IAM role** in your account, specifying the partner’s AWS account as a trusted entity.
- Attach a **permissions policy** limiting access to required resources.
- Partner assumes the role using `sts:AssumeRole`, obtaining temporary credentials.
- **Alternative:** Use **resource-based policies** for services like S3.
- Best Practices: least privilege, use external ID, monitor via CloudTrail.

---

#### 18. How do you audit all IAM users and roles for compliance?
**Answer:**
- Generate **IAM Credential Report** to review users’ login activity, MFA, and access keys.
- Use **Access Advisor** to check if permissions are over-provisioned.
- Review **roles and policies** for least privilege.
- Use **AWS Config** and **CloudTrail** for continuous monitoring.
- Optional: AWS Security Hub or Trusted Advisor for compliance checks.

---

#### 19. How do you deploy Lambda functions across multiple environments securely?
**Answer:**
- **Isolation:** Separate accounts or aliases per environment.
- **Environment Variables:** Store configs, encrypt sensitive data with KMS.
- **IAM Roles:** Least privilege per environment.
- **Versioning & Aliases:** Map Lambda versions to Dev/QA/Prod.
- **CI/CD Pipelines:** Automate deployment.
- **Secrets Management:** Use AWS Secrets Manager or SSM Parameter Store.
- **Monitoring:** CloudWatch and X-Ray per environment.

---

#### 20. How can Instance 2 communicate with Instance 1 in a private subnet behind a multi-AZ Load Balancer?
**Answer:**
- Instance 2 can communicate via the **internal load balancer DNS name**.
- Security Groups: LB allows inbound from Instance 2, LB forwards to Instance 1.
- If both instances are in the same VPC, direct access to private IP is possible.
- For different VPCs, use **VPC Peering or Transit Gateway** for private connectivity.

---

#### 21. How can an EC2 instance in a private subnet download packages without a NAT gateway or bastion host?
**Answer:**
- Use **VPC Endpoints / PrivateLink** for AWS services.
- Examples:
  - **S3 Gateway Endpoint** to fetch OS packages mirrored in S3.
  - **SSM Endpoint** to run scripts or install packages via Systems Manager.
  - **CodeArtifact** for private package repositories.
- Traffic remains within the AWS network, eliminating the need for internet or NAT.