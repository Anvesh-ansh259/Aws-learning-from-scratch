**# AWS Lambda - FAQ and Key Concepts**



**This README provides detailed answers to common AWS Lambda interview and practical questions.**



**---**



**## 1. What is AWS Lambda, and how does it work?**

**AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers. You simply upload your code to Lambda, and it automatically handles the execution in response to events, scales the infrastructure as needed, and manages fault tolerance. You only pay for the compute time used.**



**---**



**## 2. What are the key features and benefits of AWS Lambda?**

**- \*\*Serverless architecture\*\*: No need to manage servers or infrastructure.**

**- \*\*Automatic scaling\*\*: Lambda automatically scales your application based on the number of incoming requests.**

**- \*\*Event-driven\*\*: Can be triggered by various AWS services or HTTP requests.**

**- \*\*Cost-efficient\*\*: Pay only for actual compute time.**

**- \*\*High availability and fault tolerance\*\*: AWS manages availability across multiple AZs.**

**- \*\*Simplified deployment\*\*: Easy to deploy small pieces of code independently.**



**---**



**## 3. What is the maximum execution timeout for a Lambda function?**

**The maximum execution timeout for a Lambda function is \*\*15 minutes (900 seconds)\*\* per invocation.**



**---**



**## 4. What programming languages are supported by AWS Lambda?**

**AWS Lambda supports the following languages:**

**- Node.js**

**- Python**

**- Java**

**- Go**

**- Ruby**

**- .NET Core (C#)**

**- Custom runtimes via the AWS Lambda Runtime API**



**---**



**## 5. What is a cold start in Lambda, and how can it be reduced?**

**A \*\*cold start\*\* occurs when a new Lambda container is initialized to handle a request, which may introduce latency. It can be reduced by:**

**- Using \*\*Provisioned Concurrency\*\* to keep pre-initialized containers ready.**

**- Keeping functions small and lightweight.**

**- Minimizing dependencies.**

**- Keeping functions warm using scheduled triggers.**



**---**



**## 6. How does AWS Lambda pricing work?**

**Lambda pricing is based on:**

**- \*\*Number of requests\*\*: Charged per million requests.**

**- \*\*Compute time\*\*: Charged per 1ms of execution, based on memory allocated.**

**- \*\*Free tier\*\*: 1 million free requests and 400,000 GB-seconds of compute per month.**



**---**



**## 7. What are Lambda layers, and why are they used?**

**\*\*Lambda layers\*\* are packages that contain libraries, dependencies, or custom runtimes which can be shared across multiple functions. They help reduce deployment package size, simplify dependency management, and promote code reuse.**



**---**



**## 8. How do you trigger a Lambda function? Name different event sources.**

**Lambda can be triggered by events from various AWS services, including:**

**- Amazon S3 (object created/deleted)**

**- Amazon DynamoDB Streams**

**- Amazon Kinesis Streams**

**- Amazon SNS**

**- Amazon SQS**

**- Amazon API Gateway**

**- AWS CloudWatch Events / EventBridge**

**- AWS CodeCommit / CodePipeline**

**- Step Functions**



**---**



**## 9. What are environment variables in Lambda, and how are they used?**

**Environment variables are key-value pairs that Lambda functions can access at runtime. They are used to store configuration information, secrets (encrypted with AWS KMS), API endpoints, or other data that may differ between environments (development, test, production).**



**---**



**## 10. What is the difference between synchronous and asynchronous Lambda invocation?**

**- \*\*Synchronous invocation\*\*: The caller waits for the function to process and return a response (e.g., API Gateway). Errors are returned directly to the caller.**

**- \*\*Asynchronous invocation\*\*: The caller does not wait for the function to complete. Lambda retries failed invocations automatically and can send failed events to a Dead Letter Queue (DLQ). Example: S3 or SNS triggers.**



**---**



**## 11. How do you handle errors and retries in AWS Lambda?**

**- \*\*Synchronous errors\*\*: Return error to the caller for handling.**

**- \*\*Asynchronous errors\*\*: Lambda retries failed executions twice automatically.**

**- \*\*Dead Letter Queue (DLQ)\*\*: Failed events can be sent to SQS or SNS.**

**- \*\*Lambda Destinations\*\*: Route success or failure events to other AWS services.**

**- \*\*Try/Catch\*\* and structured logging for better monitoring and debugging.**



**---**



**## 12. How can Lambda access resources inside a VPC?**

**- Attach Lambda function to \*\*private subnets\*\* within a VPC.**

**- Assign \*\*security groups\*\* that allow access to VPC resources (RDS, EC2, ElastiCache).**

**- Configure \*\*NAT Gateway\*\* if the function needs internet access.**



**---**



**## 13. What is the maximum memory and temporary storage you can configure for a Lambda function?**

**- \*\*Memory allocation\*\*: 128 MB to 10,240 MB.**

**- \*\*Temporary storage (/tmp)\*\*: 512 MB by default, can be increased up to 10 GB.**



**---**



**## 14. How do you monitor and debug Lambda functions?**

**- \*\*CloudWatch Logs\*\*: Store logs generated by Lambda.**

**- \*\*CloudWatch Metrics\*\*: Track invocations, errors, duration, and throttles.**

**- \*\*AWS X-Ray\*\*: Distributed tracing for debugging and performance analysis.**

**- Structured logging, environment variables, and custom metrics for deeper insights.**



**---**



**## 15. What are concurrency and reserved concurrency in Lambda?**

**- \*\*Concurrency\*\*: The number of simultaneous executions of a Lambda function.**

**- \*\*Reserved concurrency\*\*: Guarantees a specific number of concurrent executions and limits others to prevent resource exhaustion.**

**- \*\*Provisioned concurrency\*\*: Pre-initializes containers to reduce cold start latency.**



**---**



**## 16. What are Lambda execution roles, and why are they important?**

**- Lambda uses an \*\*IAM execution role\*\* to access AWS resources.**

**- Provides least-privilege access to resources such as S3, DynamoDB, or SNS.**

**- Ensures that Lambda functions can operate securely without embedding credentials.**



**---**



**## 17. How do you package and deploy a Lambda function with external dependencies?**

**- Create a \*\*deployment package (ZIP)\*\* containing your function code and dependencies.**

**- For Python: use `pip install -t ./package` and include all libraries.**

**- For Node.js: include `node\_modules`.**

**- Optionally use \*\*Lambda layers\*\* to manage shared dependencies across multiple functions.**



**---**



**## 18. What is the difference between Lambda and EC2?**

**| Feature | AWS Lambda | EC2 |**

**|---------|------------|-----|**

**| Server management | None, fully managed | Full control over OS and software |**

**| Scaling | Automatic | Manual or Auto Scaling Groups |**

**| Pricing | Pay per invocation and duration | Pay for uptime and instance type |**

**| Runtime flexibility | Limited to supported languages or custom runtimes | Any OS/language possible |**

**| Use case | Event-driven, short-lived tasks | Long-running applications, custom servers |**



**---**



**## 19. Can Lambda run Docker containers? How?**

**Yes, Lambda supports container images up to 10 GB. You can:**

**- Build a Docker image with your application code and dependencies.**

**- Push it to \*\*Amazon ECR\*\*.**

**- Deploy Lambda function using the container image.**

**- Supports the same triggers and scaling as regular Lambda functions.**



**---**



**## 20. How can you integrate Lambda with other AWS services like S3, API Gateway, DynamoDB, and SNS?**

**- \*\*S3\*\*: Trigger Lambda on object creation, deletion, or modification.**

**- \*\*API Gateway\*\*: Connect HTTP endpoints to Lambda for serverless APIs.**

**- \*\*DynamoDB Streams\*\*: Trigger Lambda on table data changes.**

**- \*\*SNS\*\*: Trigger Lambda when messages are published to a topic.**

**- \*\*SQS\*\*: Poll messages and process asynchronously.**

**- \*\*CloudWatch Events / EventBridge\*\*: Schedule Lambda functions or react to events from other AWS services.**



**---**



**\*\*End of AWS Lambda FAQ\*\***







**This README provides detailed answers to common AWS Lambda interview and practical questions.**



**---**



**## 1. What is AWS Lambda, and how does it work?**



**AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers. You simply upload your code to Lambda, and it automatically handles the execution in response to events, scales the infrastructure as needed, and manages fault tolerance. You only pay for the compute time used.**



**---**



**## 2. What are the key features and benefits of AWS Lambda?**



**\* \*\*Serverless architecture\*\*: No need to manage servers or infrastructure.**

**\* \*\*Automatic scaling\*\*: Lambda automatically scales your application based on the number of incoming requests.**

**\* \*\*Event-driven\*\*: Can be triggered by various AWS services or HTTP requests.**

**\* \*\*Cost-efficient\*\*: Pay only for actual compute time.**

**\* \*\*High availability and fault tolerance\*\*: AWS manages availability across multiple AZs.**

**\* \*\*Simplified deployment\*\*: Easy to deploy small pieces of code independently.**



**---**



**## 3. What is the maximum execution timeout for a Lambda function?**



**The maximum execution timeout for a Lambda function is \*\*15 minutes (900 seconds)\*\* per invocation.**



**---**



**## 4. What programming languages are supported by AWS Lambda?**



**AWS Lambda supports the following languages:**



**\* Node.js**

**\* Python**

**\* Java**

**\* Go**

**\* Ruby**

**\* .NET Core (C#)**

**\* Custom runtimes via the AWS Lambda Runtime API**



**---**



**## 5. What is a cold start in Lambda, and how can it be reduced?**



**A \*\*cold start\*\* occurs when a new Lambda container is initialized to handle a request, which may introduce latency. It can be reduced by:**



**\* Using \*\*Provisioned Concurrency\*\* to keep pre-initialized containers ready.**

**\* Keeping functions small and lightweight.**

**\* Minimizing dependencies.**

**\* Keeping functions warm using scheduled triggers.**



**---**



**## 6. How does AWS Lambda pricing work?**



**Lambda pricing is based on:**



**\* \*\*Number of requests\*\*: Charged per million requests.**

**\* \*\*Compute time\*\*: Charged per 1ms of execution, based on memory allocated.**

**\* \*\*Free tier\*\*: 1 million free requests and 400,000 GB-seconds of compute per month.**



**---**



**## 7. What are Lambda layers, and why are they used?**



**\*\*Lambda layers\*\* are packages that contain libraries, dependencies, or custom runtimes which can be shared across multiple functions. They help reduce deployment package size, simplify dependency management, and promote code reuse.**



**---**



**## 8. How do you trigger a Lambda function? Name different event sources.**



**Lambda can be triggered by events from various AWS services, including:**



**\* Amazon S3 (object created/deleted)**

**\* Amazon DynamoDB Streams**

**\* Amazon Kinesis Streams**

**\* Amazon SNS**

**\* Amazon SQS**

**\* Amazon API Gateway**

**\* AWS CloudWatch Events / EventBridge**

**\* AWS CodeCommit / CodePipeline**

**\* Step Functions**



**---**



**## 9. What are environment variables in Lambda, and how are they used?**



**Environment variables are key-value pairs that Lambda functions can access at runtime. They are used to store configuration information, secrets (encrypted with AWS KMS), API endpoints, or other data that may differ between environments (development, test, production).**



**---**



**## 10. What is the difference between synchronous and asynchronous Lambda invocation?**



**\* \*\*Synchronous invocation\*\*: The caller waits for the function to process and return a response (e.g., API Gateway). Errors are returned directly to the caller.**

**\* \*\*Asynchronous invocation\*\*: The caller does not wait for the function to complete. Lambda retries failed invocations automatically and can send failed events to a Dead Letter Queue (DLQ). Example: S3 or SNS triggers.**



**---**



**## 11. How do you handle errors and retries in AWS Lambda?**



**\* \*\*Synchronous errors\*\*: Return error to the caller for handling.**

**\* \*\*Asynchronous errors\*\*: Lambda retries failed executions twice automatically.**

**\* \*\*Dead Letter Queue (DLQ)\*\*: Failed events can be sent to SQS or SNS.**

**\* \*\*Lambda Destinations\*\*: Route success or failure events to other AWS services.**

**\* \*\*Try/Catch\*\* and structured logging for better monitoring and debugging.**



**---**



**## 12. How can Lambda access resources inside a VPC?**



**\* Attach Lambda function to \*\*private subnets\*\* within a VPC.**

**\* Assign \*\*security groups\*\* that allow access to VPC resources (RDS, EC2, ElastiCache).**

**\* Configure \*\*NAT Gateway\*\* if the function needs internet access.**



**---**



**## 13. What is the maximum memory and temporary storage you can configure for a Lambda function?**



**\* \*\*Memory allocation\*\*: 128 MB to 10,240 MB.**

**\* \*\*Temporary storage (/tmp)\*\*: 512 MB by default, can be increased up to 10 GB.**



**---**



**## 14. How do you monitor and debug Lambda functions?**



**\* \*\*CloudWatch Logs\*\*: Store logs generated by Lambda.**

**\* \*\*CloudWatch Metrics\*\*: Track invocations, errors, duration, and throttles.**

**\* \*\*AWS X-Ray\*\*: Distributed tracing for debugging and performance analysis.**

**\* Structured logging, environment variables, and custom metrics for deeper insights.**



**---**



**## 15. What are concurrency and reserved concurrency in Lambda?**



**\* \*\*Concurrency\*\*: The number of simultaneous executions of a Lambda function.**

**\* \*\*Reserved concurrency\*\*: Guarantees a specific number of concurrent executions and limits others to prevent resource exhaustion.**

**\* \*\*Provisioned concurrency\*\*: Pre-initializes containers to reduce cold start latency.**



**---**



**## 16. What are Lambda execution roles, and why are they important?**



**\* Lambda uses an \*\*IAM execution role\*\* to access AWS resources.**

**\* Provides least-privilege access to resources such as S3, DynamoDB, or SNS.**

**\* Ensures that Lambda functions can operate securely without embedding credentials.**



**---**



**## 17. How do you package and deploy a Lambda function with external dependencies?**



**\* Create a \*\*deployment package (ZIP)\*\* containing your function code and dependencies.**

**\* For Python: use `pip install -t ./package` and include all libraries.**

**\* For Node.js: include `node\_modules`.**

**\* Optionally use \*\*Lambda layers\*\* to manage shared dependencies across multiple functions.**



**---**



**## 18. What is the difference between Lambda and EC2?**



**| Feature             | AWS Lambda                                        | EC2                                       |**

**| ------------------- | ------------------------------------------------- | ----------------------------------------- |**

**| Server management   | None, fully managed                               | Full control over OS and software         |**

**| Scaling             | Automatic                                         | Manual or Auto Scaling Groups             |**

**| Pricing             | Pay per invocation and duration                   | Pay for uptime and instance type          |**

**| Runtime flexibility | Limited to supported languages or custom runtimes | Any OS/language possible                  |**

**| Use case            | Event-driven, short-lived tasks                   | Long-running applications, custom servers |**



**---**



**## 19. Can Lambda run Docker containers? How?**



**Yes, Lambda supports container images up to 10 GB. You can:**



**\* Build a Docker image with your application code and dependencies.**

**\* Push it to \*\*Amazon ECR\*\*.**

**\* Deploy Lambda function using the container image.**

**\* Supports the same triggers and scaling as regular Lambda functions.**



**---**



**## 20. How can you integrate Lambda with other AWS services like S3, API Gateway, DynamoDB, and SNS?**



**\* \*\*S3\*\*: Trigger Lambda on object creation, deletion, or modification.**

**\* \*\*API Gateway\*\*: Connect HTTP endpoints to Lambda for serverless APIs.**

**\* \*\*DynamoDB Streams\*\*: Trigger Lambda on table data changes.**

**\* \*\*SNS\*\*: Trigger Lambda when messages are published to a topic.**

**\* \*\*SQS\*\*: Poll messages and process asynchronously.**

**\* \*\*CloudWatch Events / EventBridge\*\*: Schedule Lambda functions or react to events from other AWS services.**



**---**



**\*\*End of AWS Lambda FAQ\*\***

1\) **How would you deploy Lambda functions across multiple environments securely?**



To deploy Lambda functions securely across multiple environments, I would separate environments using different AWS accounts or VPCs. I’d use CI/CD pipelines to promote functions from dev to test to production. Sensitive data would be stored in Secrets Manager or encrypted environment variables. I’d enable Lambda versioning and use aliases per environment for safe promotion and rollback. Functions would run with least-privilege IAM roles, in private subnets if they need VPC access, with monitoring via CloudWatch and CloudTrail to maintain security and compliance.



==============================================================================================================================================================================





