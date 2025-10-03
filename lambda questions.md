# AWS Lambda FAQs - Interview Ready

## Q&A Format

### Q1: What is AWS Lambda, and how does it work?

**A:** AWS Lambda is a serverless compute service that lets you run code without managing servers. You upload your code, and Lambda executes it in response to events. AWS handles scaling, fault tolerance, and availability. You only pay for compute time used.

---

### Q2: What are the key features and benefits of AWS Lambda?

**A:**

* **Serverless architecture:** No server management required.
* **Automatic scaling:** Lambda scales based on incoming requests.
* **Event-driven:** Triggered by various AWS services or HTTP requests.
* **Cost-efficient:** Pay only for execution time and requests.
* **High availability:** Runs across multiple Availability Zones.
* **Simplified deployment:** Deploy small pieces of code independently.

---

### Q3: What is a cold start in Lambda, and how can it be reduced?

**A:** A cold start happens when a new Lambda container is initialized to handle a request, introducing latency. It can be reduced by:

* Using **Provisioned Concurrency**.
* Keeping functions small and lightweight.
* Minimizing dependencies.
* Keeping functions warm using scheduled triggers.

---

### Q4: What is a warm start?

**A:** A warm start occurs when Lambda reuses an existing container that has already executed a previous request. This avoids initialization delay and executes faster.

---

### Q5: What programming languages are supported by Lambda?

**A:** Node.js, Python, Java, Go, Ruby, .NET Core (C#), and custom runtimes via the Lambda Runtime API.

---

### Q6: How does AWS Lambda pricing work?

**A:** Pricing is based on:

* **Requests:** Charged per million requests.
* **Compute time:** Charged per 1ms based on memory allocated.
* **Free tier:** 1M free requests + 400,000 GB-seconds per month.

---

### Q7: What are Lambda layers, and why are they used?

**A:** Lambda Layers are packages containing libraries, dependencies, or runtimes shared across multiple functions. They reduce deployment size and promote code reuse.

---

### Q8: How do you trigger a Lambda function?

**A:** Lambda can be triggered by events from:

* Amazon S3 (object created/deleted)
* DynamoDB Streams
* Kinesis Streams
* SNS
* SQS
* API Gateway
* CloudWatch Events / EventBridge
* CodeCommit / CodePipeline
* Step Functions

---

### Q9: What are environment variables in Lambda, and how are they used?

**A:** Environment variables are key-value pairs available at runtime. They store configuration, secrets (encrypted with KMS), API endpoints, or environment-specific data.

---

### Q10: What is the difference between synchronous and asynchronous invocation?

**A:**

* **Synchronous:** Caller waits for the function to complete (e.g., API Gateway). Errors are returned directly.
* **Asynchronous:** Caller does not wait. Lambda retries failed invocations automatically and can send failed events to a DLQ (e.g., S3 or SNS triggers).

---

### Q11: How do you handle errors and retries in Lambda?

**A:**

* **Synchronous errors:** Returned to caller.
* **Asynchronous errors:** Auto-retries twice.
* **Dead Letter Queue (DLQ):** Send failed events to SQS or SNS.
* **Lambda Destinations:** Route success/failure to other services.
* **Structured logging and try/catch** for debugging.

---

### Q12: How can Lambda access resources inside a VPC?

**A:**

* Attach Lambda to private subnets.
* Assign security groups that allow access to VPC resources (RDS, EC2, etc.).
* Configure NAT Gateway if internet access is needed.

---

### Q13: What is the maximum memory and temporary storage for Lambda?

**A:**

* **Memory:** 128 MB – 10,240 MB
* **/tmp storage:** 512 MB default, up to 10 GB

---

### Q14: How do you monitor and debug Lambda functions?

**A:**

* CloudWatch Logs and Metrics
* AWS X-Ray for distributed tracing
* Structured logging and custom metrics

---

### Q15: What are concurrency, reserved concurrency, and provisioned concurrency?

**A:**

* **Concurrency:** Number of simultaneous executions.
* **Reserved concurrency:** Guarantees a set number of concurrent executions.
* **Provisioned concurrency:** Pre-initialized containers to reduce cold start latency.

---

### Q16: What are Lambda execution roles, and why are they important?

**A:** IAM roles define permissions for Lambda to access AWS resources securely. Follow the principle of least privilege.

---

### Q17: How do you package and deploy a Lambda function with external dependencies?

**A:**

* Create a ZIP package with code + dependencies.
* Python: `pip install -t ./package`
* Node.js: include `node_modules`
* Use Lambda Layers for shared dependencies
* Optionally use container images via ECR.

---

### Q18: What is the difference between Lambda and EC2?

**A:**

| Feature           | Lambda                    | EC2               |
| ----------------- | ------------------------- | ----------------- |
| Server management | Fully managed             | Full control      |
| Scaling           | Automatic                 | Manual / ASG      |
| Pricing           | Pay per invocation        | Pay for uptime    |
| Runtime           | Limited/custom runtimes   | Any OS/language   |
| Use case          | Event-driven, short tasks | Long-running apps |

---

### Q19: Can Lambda run Docker containers? How?

**A:** Yes, Lambda supports container images up to 10 GB. Steps:

1. Build Docker image with code + dependencies.
2. Push to Amazon ECR.
3. Deploy Lambda from container image.
   Supports same triggers and scaling as normal Lambda functions.

---

### Q20: How can you integrate Lambda with other AWS services?

**A:**

* **S3:** Trigger on object creation/deletion.
* **API Gateway:** Serverless APIs.
* **DynamoDB Streams:** Trigger on table updates.
* **SNS:** Trigger on message publish.
* **SQS:** Poll messages asynchronously.
* **CloudWatch / EventBridge:** Scheduled or event-based triggers.

---

### Q21: How would you deploy Lambda functions across multiple environments securely?

**A:**

* Isolate environments using accounts or VPCs
* CI/CD pipelines for promotion (dev → test → prod)
* Store secrets in Secrets Manager / encrypted env variables
* Use Lambda versioning + aliases for safe deployment and rollback
* Least-privilege IAM roles per environment
* VPC placement for sensitive resources
* Monitoring via CloudWatch, X-Ray, CloudTrail
