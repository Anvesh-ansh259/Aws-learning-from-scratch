1\) **Explain how you would design a highly available EC2 architecture across multiple AZs for a web application.**



Use multiple AZs with an Application Load Balancer in front of Auto Scaling Groups that span those AZs. Put app servers in private subnets, keep static assets in S3/CloudFront, use RDS with Multi-AZ (and read replicas for scale), add ElastiCache for caching, and use Route 53 health checks and failover. Add IAM, security groups, CloudWatch monitoring, backups and automated deployments (rolling or blue/green) to make it resilient and maintainable.



=================================================================================================================================================================================



**2) How would you migrate a running EC2 instance to another region with minimal downtime?**



To migrate an EC2 instance to another region with minimal downtime, I’d create an AMI of the running instance and copy it to the target region. From that AMI, I’d launch a new instance in the destination VPC. To minimize downtime, I’d sync any application or database data ahead of time, then do a final delta sync at cutover. Finally, I’d update DNS in Route 53 with a low TTL so traffic shifts quickly to the new region. This approach ensures minimal service interruption while providing a tested rollback path.



=================================================================================================================================================================================



**3) If your EC2 instance is not reachable via SSH, what troubleshooting steps would you perform?**



If I cannot reach an EC2 instance via SSH, I would first check the security group to ensure port 22 is allowed from my IP. Next, I’d verify the subnet’s Network ACLs, confirm the instance has a public IP if in a public subnet, and check the route table points to the Internet Gateway. I’d also ensure I’m using the correct key pair with proper permissions. On the OS, I’d check that the firewall isn’t blocking SSH, and I’d review instance status checks and console output. If needed, I could use AWS Session Manager to connect without SSH.



=================================================================================================================================================================================



**4) Your web application experiences unpredictable traffic spikes. How would you configure auto scaling policies to handle this while optimizing costs?**



To handle unpredictable traffic spikes while optimizing costs, I would configure an Auto Scaling Group across multiple AZs and use a target-tracking policy based on metrics like average CPU utilization or requests per instance. For sudden bursts, I’d add a step-scaling policy to scale quickly when thresholds are crossed. Scheduled scaling could also be used for predictable traffic patterns. I’d set appropriate cooldown periods to prevent thrashing and optimize costs by right-sizing instances and using spot instances for non-critical workloads. This approach ensures responsiveness to spikes without unnecessary over-provisioning.



=================================================================================================================================================================================

**5) Explain a scenario where scheduled scaling is more appropriate than dynamic scaling.**



Scheduled scaling is ideal when traffic patterns are predictable. For example, an e-commerce site might experience daily traffic spikes in the morning and evening. Instead of waiting for CPU utilization to rise and trigger dynamic scaling, I’d schedule the Auto Scaling Group to increase instance count just before the spike and scale down afterward. This ensures the application handles peak load efficiently and optimizes costs by not over-provisioning outside peak periods.



=================================================================================================================================================================================

6\) **Your organization needs to grant cross-account access to a partner. How would you implement it?**



To grant cross-account access to a partner, I would create an IAM role in our account with a policy granting only the permissions needed. I would define a trust policy allowing the partner’s AWS account to assume the role. Optionally, I’d use an External ID for security. The partner can then assume the role via STS, getting temporary credentials to access only the allowed resources. All activity would be logged with CloudTrail for auditing.



==============================================================================================================================================================================

**7) You want to audit all IAM users and roles for compliance. How would you do this?**



To audit all IAM users and roles for compliance, I would start by generating an IAM credential report to get a snapshot of all users, their access keys, last usage, and MFA status. I’d also review IAM Access Advisor to identify unused permissions. CloudTrail would provide a history of API activity for auditing, and AWS Config rules can continuously check IAM compliance. Additionally, tools like Security Hub and IAM Access Analyzer help detect misconfigurations or risky permissions.



==============================================================================================================================================================

**8) How would you deploy Lambda functions across multiple environments securely?**



To deploy Lambda functions securely across multiple environments, I would separate environments using different AWS accounts or VPCs. I’d use CI/CD pipelines to promote functions from dev to test to production. Sensitive data would be stored in Secrets Manager or encrypted environment variables. I’d enable Lambda versioning and use aliases per environment for safe promotion and rollback. Functions would run with least-privilege IAM roles, in private subnets if they need VPC access, with monitoring via CloudWatch and CloudTrail to maintain security and compliance.



===================================================================================================================================================================

**9) How can Instance 2, with a static IP, communicate with Instance 1, which is in a private subnet and mapped to a multi-AZ load balancer?**



To enable Instance 2 with a static IP to communicate with Instance 1 in a private subnet behind a multi-AZ load balancer, I would have Instance 2 send traffic to the load balancer’s DNS name. The load balancer handles routing to Instance 1 across multiple AZs. I would configure the security groups so the LB allows traffic from Instance 2 and Instance 1 only accepts traffic from the load balancer’s SG. If Instance 2 is in a different VPC or on-prem, I’d set up VPC Peering, VPN, or Direct Connect to enable network reachability.



===================================================================================================================================================================



**10) For an EC2 instance in a private subnet, how can it verify and download required packages from the internet without using a NAT gateway or bastion host? Are there any other AWS services that can facilitate this?**



You can use VPC Endpoints (PrivateLink) — specifically, S3 Gateway Endpoint for package repositories and SSM VPC Endpoints to manage and install updates privately, without needing a NAT Gateway or bastion host.



==================================================================================================================================================================



11\) **can u increase the root volume without shutting down the instances ?**



Yes, we can increase the root volume of an EC2 instance without shutting it down, because Amazon EBS supports online resizing. First, we go to the EC2 console and modify the volume to the desired size. Then, inside the running instance, we expand the partition and filesystem using tools like growpart and resize2fs on Linux, or Disk Management on Windows. This entire process happens while the instance is still running, so there’s no downtime. The only limitation is that we can increase the size, but shrinking would require downtime.



==================================================================================================

12\) **Types of elb**





| Feature                        | CLB         | ALB                      | NLB                     | GLB                |

| ------------------------------ | ----------- | ------------------------ | ----------------------- | ------------------ |

| OSI Layer                      | 4 \& 7       | 7                        | 4                       | 3                  |

| HTTP/HTTPS Support             | Yes         | Yes                      | Limited (TLS)           | No                 |

| Path/Host-based Routing        | No          | Yes                      | No                      | No                 |

| High Performance / Low Latency | Medium      | Medium                   | High                    | Medium             |

| Use Case                       | Legacy apps | Web apps / Microservices | TCP/UDP high throughput | Network appliances |





============================================================================================================================================================================================



13\) What is ENI?

**An ENI, or Elastic Network Interface, is a virtual network card that can be attached to an EC2 instance. It provides primary and secondary private IPs, can have its own security groups, and can be attached/detached independently. We use ENIs for high availability and failover, multiple IP assignments, traffic isolation, and managing both public and private network access. For example, in a critical application, we can detach an ENI with a fixed IP from a failed instance and attach it to a new instance to maintain continuity.**



============================================================================================================================================================================================



**14) what is WAF?

“**AWS WAF is a web application firewall that protects applications from common web attacks like SQL injection, cross-site scripting, and DDoS attacks. It works by evaluating HTTP/S requests against customizable rules or managed rule groups and either allows, blocks, or counts them. It can be integrated with CloudFront, ALB, or API Gateway. WAF also provides rate limiting, IP restrictions, and logging, making applications more secure and resilient without affecting performance.



============================================================================================================================================================================================



| **Service**                      | **Default Retention**                              | **Max Retention / Notes**                         | **Explanation**                                                                                                                                                                                                                               |

| ---------------------------- | ---------------------------------------------- | --------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| \*\*CloudTrail Event History\*\* | 90 days                                        | For longer retention, store in S3             | AWS keeps the last \*\*90 days of management events\*\* in the CloudTrail console. For compliance or long-term auditing, you need to \*\*configure CloudTrail to deliver logs to an S3 bucket\*\*, which can store data indefinitely.             |

| \*\*CloudTrail S3 Logs\*\*       | Depends on S3 lifecycle                        | Indefinite (you define)                       | When you configure CloudTrail to \*\*write events to S3\*\*, the retention depends on your \*\*S3 lifecycle policies\*\*. You can keep logs indefinitely, archive to Glacier, or delete automatically.                                            |

| \*\*CloudWatch Metrics\*\*       | 1-min metrics: 15 days, 1-hr metrics: 455 days | Fixed                                         | CloudWatch metrics are stored at different granularities: \\n- \*\*1-minute metrics\*\* are available for \*\*15 days\*\*\\n- \*\*1-hour aggregated metrics\*\* are kept for \*\*455 days\*\*\\nThese retention periods are \*\*fixed and cannot be changed\*\*. |

| \*\*CloudWatch Logs\*\*          | Never by default                               | Configurable per log group (1 day → 10 years) | CloudWatch Logs \*\*does not delete logs automatically\*\* by default. You must set a \*\*retention policy per log group\*\* to automatically delete old logs. Options range from \*\*1 day up to 10 years\*\*.                                       |
























































