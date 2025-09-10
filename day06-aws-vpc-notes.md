# AWS VPC (Virtual Private Cloud) Notes

## 1. What is VPC?
- **VPC (Virtual Private Cloud)** is a logically isolated section of the AWS cloud where you can launch AWS resources.  
- Provides full control over networking, including IP addresses, subnets, routing, and security.  
- **Why required?**
  - To isolate resources for better security.  
  - To design custom network architectures.  
  - To control inbound and outbound traffic.  
  - To connect AWS resources with on-premises networks securely.  

---

## 2. Subnets
- **Definition:** Subnets are subdivisions of a VPC’s IP address range (CIDR block).  
- **Why required?**
  - To organize resources into logical groups.  
  - To separate public-facing and private resources.  

### Types of Subnets:
- **Public Subnet**  
  - Has a route to an **Internet Gateway (IGW)**.  
  - Used for resources that need internet access (e.g., web servers).  

- **Private Subnet**  
  - No direct route to the internet.  
  - Can use a **NAT Gateway** to access internet outbound only.  
  - Used for internal resources (e.g., databases).  

---

## 3. Internet Gateway (IGW)
- **Definition:** A horizontally scaled, redundant, and highly available gateway that connects a VPC to the internet.  
- **Why required?**
  - Enables instances in a public subnet to communicate with the internet.  
  - Required for both inbound and outbound internet traffic.  

---

## 4. NAT Gateway
- **Definition:** A managed AWS service that allows instances in private subnets to connect to the internet or other AWS services, but prevents the internet from initiating a connection with those instances.  
- **Why required?**
  - For private subnet instances to download patches/updates from the internet without being exposed.  
  - More secure than making instances public.  

---

## 5. Security Group (SG)
- **Definition:** A virtual firewall that controls **inbound and outbound traffic at the instance level**.  
- **Why required?**
  - Protects EC2 instances by allowing only defined traffic.  
  - Stateful: if inbound traffic is allowed, outbound is automatically allowed.  

---

## 6. Network ACL (NACL)
- **Definition:** A virtual firewall that controls traffic **at the subnet level**.  
- **Why required?**
  - Provides an additional layer of security.  
  - Stateless: return traffic must be explicitly allowed.  
  - Useful for blocking specific IPs or ranges at the subnet level.  

---

## 7. VPC Peering
- **Definition:** A networking connection between two VPCs that enables routing traffic privately between them using internal IP addresses.  
- **Why required?**
  - To share resources across VPCs.  
  - For cross-team or cross-application communication.  
  - Low latency and cost-effective compared to using internet.  

---

## 8. VPC Transit Gateway
- **Definition:** A service that enables connecting multiple VPCs and on-premises networks through a central hub.  
- **Why required?**
  - Simplifies complex network topologies (hub-and-spoke model).  
  - Scales better than many-to-many VPC peering.  

---

## 9. VPC Endpoints
- **Definition:** Private connections between VPCs and AWS services without using the internet.  
- **Types:**
  - **Interface Endpoint:** Uses ENI (Elastic Network Interface).  
  - **Gateway Endpoint:** Supports services like S3 and DynamoDB.  
- **Why required?**
  - Increases security by avoiding internet traffic.  
  - Reduces data transfer costs.  

---

## 10. Additional Components
- **Elastic IP:** Static, public IPv4 address for EC2 or NAT.  
- **Route Tables:** Define how traffic is directed within VPC and outside.  
- **DHCP Options Set:** Configure domain name servers and domain names.  
- **VPN & Direct Connect:** Connect on-premises networks to AWS securely.  

---

## 11. Interview Tips / Common Questions
1. Difference between Security Group and NACL?  
   - SG: Instance level, Stateful.  
   - NACL: Subnet level, Stateless.  

2. How to make a subnet public?  
   - Attach a route to Internet Gateway in subnet’s route table.  

3. Why prefer NAT Gateway over NAT Instance?  
   - Fully managed, scalable, highly available, better performance.  

4. Why use VPC Endpoints?  
   - To access AWS services securely without using internet.  

---

✅ This covers **VPC, Subnets, Internet Gateway, NAT Gateway, Security Groups, NACLs, VPC Peering, Transit Gateway, and Endpoints** with reasons why they are required.
