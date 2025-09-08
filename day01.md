# 📘 Day 1 – AWS Basics (Interview-Style Explanations)

---

## 🔹 Why Public Cloud is Required
If an interviewer asks:  
👉 *“Why do we need the cloud instead of traditional infrastructure?”*  

✅ Answer:  
In traditional IT, companies had to **buy physical servers, maintain them, upgrade hardware, and manage downtime**. This required **high upfront cost** and scaling was slow.  
With the public cloud (like AWS):  
- We **rent IT infrastructure on-demand** and pay only for what we use.  
- It offers **scalability, global reach, and reduced cost**.  
- Teams can focus on building applications instead of managing hardware.  

---

## 🔹 Cloud Service Models
👉 *“Can you explain IaaS, PaaS, and SaaS with examples?”*  

✅ Answer:  
- **IaaS (Infrastructure as a Service):** AWS provides raw compute, storage, and networking. We control the OS, apps, and configs.  
  - Example: **EC2, S3, VPC**.  
- **PaaS (Platform as a Service):** AWS provides infrastructure + runtime + OS. We just deploy applications.  
  - Example: **Elastic Beanstalk, RDS**.  
- **SaaS (Software as a Service):** Fully managed applications delivered over the internet. No management by the user.  
  - Example: **Gmail, Salesforce, Zoom**.  

👉 Easy analogy:  
- IaaS = Renting a house, managing everything inside.  
- PaaS = Renting a furnished apartment.  
- SaaS = Booking a hotel room.  

---

## 🔹 AWS Global Infrastructure
If asked: *“What are Regions, AZs, and Edge Locations?”*  

✅ Answer:  

**1. Region**  
- A **fully isolated geographical area** containing multiple Availability Zones.  
- Purpose: Deploy applications close to users and meet compliance requirements.  
- Example:  
  > “AWS Mumbai (`ap-south-1`) is a region. Deploying my application here reduces latency for Indian users and ensures data residency compliance.”

**2. Availability Zone (AZ)**  
- One or more **discrete data centers** within a region with **independent power, networking, and cooling**.  
- Purpose: Provide **high availability and fault tolerance**.  
- Example:  
  > “Deploying a web server in AZ1 and a database in AZ2 ensures the application continues running even if AZ1 fails.”

**3. Edge Location**  
- **Site deployed by AWS to cache content closer to end users**, mainly used by **CloudFront CDN**.  
- Purpose: Reduce latency for global users by delivering content quickly.  
- Example:  
  > “A user in Delhi accessing an image hosted in Mumbai will get it from the nearest Edge Location in Delhi, improving speed.”

💡 Quick tip:  
- **Regions = geographic distribution**  
- **AZs = fault-tolerant data centers**  
- **Edge = low-latency content delivery**  

---

## 🔹 Amazon EC2 (Elastic Compute Cloud)
If asked: *“What is EC2?”*  

✅ Answer:  
- EC2 provides **virtual servers in the AWS cloud**.  
- We can launch instances with different CPU, RAM, and storage sizes within minutes.  
- **Instance families:**  
  - General Purpose → Balanced (web apps).  
  - Compute Optimized → CPU heavy (gaming, encoding).  
  - Memory Optimized → RAM heavy (databases).  
  - Storage Optimized → High throughput (big data).  
  - Accelerated Computing → GPUs (ML/AI).  

---

## 🔹 EC2 Purchase Options
If asked: *“What are EC2 purchase models?”*  

✅ Answer:  
- **On-Demand** – Pay per second/hour, no commitment. Best for unpredictable workloads.  
- **Reserved Instances** – 1 or 3 years commitment, cheaper. Best for steady workloads.  
- **Spot Instances** – Up to 90% cheaper, but can be interrupted. Best for non-critical batch jobs.  
- **Dedicated Hosts** – Physical server for compliance/licensing.  
- **Savings Plans** – Commit to spend ($/hour), flexible across instance types.  

---

# 🎯 Interview Questions with Answers  

### ✅ For Freshers
**Q1. Why do we need the cloud instead of on-premise infrastructure?**  
👉 In on-prem, we spend huge upfront costs, scaling is slow, and managing hardware is complex. Cloud removes all that by offering on-demand, pay-as-you-go, and scalable infrastructure.  

**Q2. Explain IaaS, PaaS, SaaS with examples.**  
👉 IaaS gives infra like EC2. PaaS provides platform services like Elastic Beanstalk. SaaS provides complete apps like Gmail.  

**Q3. What are AWS Regions, AZs, and Edge Locations?**  
👉 Regions = fully isolated geographic areas. AZs = independent data centers in regions for high availability. Edge Locations = caching points to deliver content faster to users globally.  

**Q4. What is EC2?**  
👉 EC2 = virtual server in the cloud, scalable, supports multiple instance families.  

**Q5. Difference between On-Demand and Reserved Instances?**  
👉 On-Demand = pay as you go, no commitment. Reserved = cheaper, long-term commitment.  

---

### ✅ For Experienced
**Q1. How would you design for high availability?**  
👉 Deploy across multiple AZs within a region. For global HA, deploy across multiple regions with Route 53 failover.  

**Q2. Compare Savings Plans vs Reserved Instances.**  
👉 RIs are tied to instance type/region. Savings Plans are more flexible and apply across instance families/services.  

**Q3. When to use Spot Instances?**  
👉 For workloads that are fault-tolerant, like batch jobs, data analysis, ML training.  

**Q4. Which EC2 instance family fits different workloads?**  
- ML/AI → Accelerated (P3, G4).  
- Database → Memory Optimized (R5).  
- Video Encoding → Compute Optimized (C5).  
- Web Server → General Purpose (T3).  

**Q5. How does CloudFront help performance?**  
👉 By caching content at Edge Locations close to users, reducing latency and improving speed globally.  

---

# 🛠 Scenario-Based Questions with Answers  

**Scenario 1:** Your company has unpredictable traffic for a website. Which EC2 purchase option will you choose?  
👉 **On-Demand Instances**, because they’re flexible and scale with traffic.  

**Scenario 2:** You need to train ML models requiring GPUs. Which instance type will you select?  
👉 **Accelerated Computing (P3/G4)**.  

**Scenario 3:** A client wants global users to access images/videos faster. What service would you suggest?  
👉 **CloudFront with Edge Locations**.  

**Scenario 4:** You have a 24/7 workload running for 3 years. Which pricing model is cost-effective?  
👉 **Reserved Instances or Savings Plans**.  
