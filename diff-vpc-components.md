# AWS Networking Components - Key Differences

## 1. Public Subnet vs Private Subnet
| Feature              | Public Subnet                                                                 | Private Subnet                                                                 |
|----------------------|---------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| Internet Access      | Has a route to **Internet Gateway (IGW)**                                       | No direct route to Internet Gateway                                             |
| Use Case             | Hosting resources that must be accessible from the internet (e.g., web servers)| Hosting internal resources (e.g., databases, application servers)               |
| Security             | Higher exposure, needs tighter security group rules                            | More secure, as they are isolated from direct internet exposure                 |
| NAT Usage            | Not required (direct internet access available via IGW)                        | Requires **NAT Gateway/Instance** in a public subnet for outbound internet access |

---

## 2. NACL (Network ACL) vs Security Group
| Feature              | NACL                                                        | Security Group                                              |
|----------------------|-------------------------------------------------------------|-------------------------------------------------------------|
| Type                 | **Stateless** – Return traffic must be explicitly allowed   | **Stateful** – Return traffic automatically allowed         |
| Level of Control     | Works at the **subnet level**                               | Works at the **instance (ENI) level**                       |
| Rules                | Supports both **allow** and **deny** rules                  | Only **allow** rules (no deny)                              |
| Default Behavior     | By default, allows all inbound/outbound traffic             | By default, denies all inbound, allows all outbound          |
| Rule Evaluation      | Rules evaluated in order, lowest number first               | All rules are evaluated before deciding                      |
| Best Use             | Adding an extra layer of subnet-level security              | Controlling instance-level access                            |

---

## 3. Internet Gateway (IGW) vs NAT Gateway
| Feature              | Internet Gateway (IGW)                                    | NAT Gateway                                                 |
|----------------------|-----------------------------------------------------------|-------------------------------------------------------------|
| Purpose              | Allows **public subnets** to connect directly to the internet | Allows **private subnets** to access internet **outbound only** |
| Direction            | Inbound & Outbound internet traffic                        | Outbound internet traffic only (no inbound connections)      |
| Placement            | Attached to the **VPC**                                   | Deployed in a **public subnet**                             |
| IP Type              | Uses **public IP/Elastic IP**                             | Uses **Elastic IP**                                         |
| Example              | Web server in a public subnet uses IGW                    | Database in private subnet downloads updates via NAT        |

---

## 4. NAT Gateway vs Security Group
| Feature              | NAT Gateway                                               | Security Group                                              |
|----------------------|-----------------------------------------------------------|-------------------------------------------------------------|
| Purpose              | Enables outbound internet access for private subnets       | Controls inbound & outbound traffic to resources            |
| Type                 | Managed AWS service (network translation)                 | Virtual firewall (rules)                                    |
| Works At             | Subnet level (private subnet → internet)                  | Instance level (EC2/ENI)                                    |
| Direction            | Only outbound (no inbound)                                | Both inbound and outbound rules                             |
| Relation             | NAT provides connectivity, Security Group provides filtering | Work together: NAT allows internet connection, SG controls what traffic is allowed |

---

## 5. Additional Key Comparisons

### Route Table vs NACL
| Feature              | Route Table                                               | NACL                                                        |
|----------------------|-----------------------------------------------------------|-------------------------------------------------------------|
| Purpose              | Defines where traffic is routed (subnet-level)            | Defines what traffic is allowed/denied (subnet-level firewall) |
| Type                 | Routing mechanism                                         | Security mechanism                                          |

### Stateful vs Stateless
- **Security Group (Stateful)**: Automatically allows return traffic.  
- **NACL (Stateless)**: Return traffic must be explicitly defined.  

---

# 📌 Summary
- **Public Subnet** → Direct internet access via IGW.  
- **Private Subnet** → Uses NAT for outbound internet only.  
- **Security Groups** → Instance-level, stateful, only allow rules.  
- **NACLs** → Subnet-level, stateless, allow + deny rules.  
- **IGW** → Enables public internet access.  
- **NAT Gateway** → Enables private outbound internet access.  
