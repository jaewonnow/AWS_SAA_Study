# Week 1: IAM, EC2, and S3 Basics - Practice Questions

Based on the provided PDF, here are 30 recommended questions focusing on IAM, EC2, and basic S3 concepts suitable for Week 1.

### Question 1 (PDF Q#3)
**Topic:** IAM / S3 Access
**Question:**
A company uses AWS Organizations to manage multiple AWS accounts for different departments. The management account has an Amazon S3 bucket that contains project reports. The company wants to limit access to this S3 bucket to only users of accounts within the organization in AWS Organizations. Which solution meets these requirements with the LEAST amount of operational overhead?
**Options:**
A. Add the aws PrincipalOrgID global condition key with a reference to the organization ID to the S3 bucket policy.
B. Create an organizational unit (OU) for each department. Add the aws:PrincipalOrgPaths global condition key to the S3 bucket policy.
C. Use AWS CloudTrail to monitor the CreateAccount, InviteAccountToOrganization, LeaveOrganization, and RemoveAccountFromOrganization events. Update the S3 bucket policy accordingly.
D. Tag each user that needs access to the S3 bucket. Add the aws:PrincipalTag global condition key to the S3 bucket policy.

### Question 2 (PDF Q#17)
**Topic:** IAM / EC2 Access
**Question:**
A company is implementing a new business application. The application runs on two Amazon EC2 instances and uses an Amazon S3 bucket for document storage. A solutions architect needs to ensure that the EC2 instances can access the S3 bucket. What should the solutions architect do to meet this requirement?
**Options:**
A. Create an IAM role that grants access to the S3 bucket. Attach the role to the EC2 instances.
B. Create an IAM policy that grants access to the S3 bucket. Attach the policy to the EC2 instances.
C. Create an IAM group that grants access to the S3 bucket. Attach the group to the EC2 instances.
D. Create an IAM user that grants access to the S3 bucket. Attach the user account to the EC2 instances.

### Question 3 (PDF Q#37)
**Topic:** EC2 Administration / Security
**Question:**
A company recently launched a variety of new workloads on Amazon EC2 instances in its AWS account. The company needs to create a strategy to access and administer the instances remotely and securely. The company needs to implement a repeatable process that works with native AWS services and follows the AWS Well-Architected Framework. Which solution will meet these requirements with the LEAST operational overhead?
**Options:**
A. Use the EC2 serial console to directly access the terminal interface of each instance for administration.
B. Attach the appropriate IAM role to each existing instance and new instance. Use AWS Systems Manager Session Manager to establish a remote SSH session.
C. Create an administrative SSH key pair. Load the public key into each EC2 instance. Deploy a bastion host in a public subnet to provide a tunnel for administration of each instance.
D. Establish an AWS Site-to-Site VPN connection. Instruct administrators to use their local on-premises machines to connect directly to the instances by using SSH keys across the VPN tunnel.

### Question 4 (PDF Q#84)
**Topic:** EC2 Pricing Models
**Question:**
A company wants to reduce the cost of its existing three-tier web architecture. The web, application, and database servers are running on Amazon EC2 instances for the development, test, and production environments. The EC2 instances average 30% CPU utilization during peak hours and 10% CPU utilization during non-peak hours. The production EC2 instances run 24 hours a day. The development and test EC2 instances run for at least 8 hours each day. The company plans to implement automation to stop the development and test EC2 instances when they are not in use. Which EC2 instance purchasing solution will meet the company's requirements MOST cost-effectively?
**Options:**
A. Use Spot Instances for the production EC2 instances. Use Reserved Instances for the development and test EC2 instances.
B. Use Reserved Instances for the production EC2 instances. Use On-Demand Instances for the development and test EC2 instances.
C. Use Spot blocks for the production EC2 instances. Use Reserved Instances for the development and test EC2 instances.
D. Use On-Demand Instances for the production EC2 instances. Use Spot blocks for the development and test EC2 instances.

### Question 5 (PDF Q#96)
**Topic:** IAM Policy
**Question:**
An Amazon EC2 administrator created the following policy associated with an IAM group containing several users:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:TerminateInstances",
      "Resource": "*",
      "Condition": {
        "IpAddress": { "aws:SourceIp": "10.100.100.0/24" }
      }
    },
    {
      "Effect": "Deny",
      "Action": "ec2:*",
      "Resource": "*",
      "Condition": {
        "StringNotEquals": { "ec2:Region": "us-east-1" }
      }
    }
  ]
}
```
What is the effect of this policy?
**Options:**
A. Users can terminate an EC2 instance in any AWS Region except us-east-1.
B. Users can terminate an EC2 instance with the IP address 10.100.100.1 in the us-east-1 Region.
C. Users can terminate an EC2 instance in the us-east-1 Region when the user's source IP is 10.100.100.254.
D. Users cannot terminate an EC2 instance in the us-east-1 Region when the user's source IP is 10.100.100.254.

### Question 6 (PDF Q#127)
**Topic:** EC2 / EBS / S3 Storage Choice
**Question:**
A media company is evaluating the possibility of moving its systems to the AWS Cloud. The company needs at least 10 TB of storage with the maximum possible I/O performance for video processing, 300 TB of very durable storage for storing media content, and 900 TB of storage to meet requirements for archival media that is not in use anymore. Which set of services should a solutions architect recommend to meet these requirements?
**Options:**
A. Amazon EBS for maximum performance, Amazon S3 for durable data storage, and Amazon S3 Glacier for archival storage
B. Amazon EBS for maximum performance, Amazon EFS for durable data storage, and Amazon S3 Glacier for archival storage
C. Amazon EC2 instance store for maximum performance, Amazon EFS for durable data storage, and Amazon S3 for archival storage
D. Amazon EC2 instance store for maximum performance, Amazon S3 for durable data storage, and Amazon S3 Glacier for archival storage

### Question 7 (PDF Q#543)
**Topic:** Cost Management / Savings Plans
**Question:**
A company runs Amazon EC2 instances in multiple AWS accounts that are individually billed. The company recently purchased a Savings Plan. Because of changes in the company’s business requirements, the company has decommissioned a large number of EC2 instances. The company wants to use its Savings Plan discounts on its other AWS accounts. Which combination of steps will meet these requirements? (Choose two.)
**Options:**
A. From the AWS Account Management Console of the management account, turn on discount sharing from the billing preferences section.
B. From the AWS Account Management Console of the account that purchased the existing Savings Plan, turn on discount sharing from the billing preferences section. Include all accounts.
C. From the AWS Organizations management account, use AWS Resource Access Manager (AWS RAM) to share the Savings Plan with other accounts.
D. Create an organization in AWS Organizations in a new payer account. Invite the other AWS accounts to join the organization from the management account.
E. Create an organization in AWS Organizations in the existing AWS account with the existing EC2 instances and Savings Plan. Invite the other AWS accounts to join the organization from the management account.

### Question 8 (PDF Q#24)
**Topic:** EC2 Cost Analysis
**Question:**
A company observes an increase in Amazon EC2 costs in its most recent bill. The billing team notices unwanted vertical scaling of instance types for a couple of EC2 instances. A solutions architect needs to create a graph comparing the last 2 months of EC2 costs and perform an in-depth analysis to identify the root cause of the vertical scaling. How should the solutions architect generate the information with the LEAST operational overhead?
**Options:**
A. Use AWS Budgets to create a budget report and compare EC2 costs based on instance types.
B. Use Cost Explorer's granular filtering feature to perform an in-depth analysis of EC2 costs based on instance types.
C. Use graphs from the AWS Billing and Cost Management dashboard to compare EC2 costs based on instance types for the last 2 months.
D. Use AWS Cost and Usage Reports to create a report and send it to an Amazon S3 bucket. Use Amazon QuickSight with Amazon S3 as a source to generate an interactive graph based on instance types.

### Question 9 (PDF Q#47)
**Topic:** EC2 Capacity
**Question:**
A company needs guaranteed Amazon EC2 capacity in three specific Availability Zones in a specific AWS Region for an upcoming event that will last 1 week. What should the company do to guarantee the EC2 capacity?
**Options:**
A. Purchase Reserved Instances that specify the Region needed.
B. Create an On-Demand Capacity Reservation that specifies the Region needed.
C. Purchase Reserved Instances that specify the Region and three Availability Zones needed.
D. Create an On-Demand Capacity Reservation that specifies the Region and three Availability Zones needed.

### Question 10 (PDF Q#50)
**Topic:** Systems Manager / EC2 Patching
**Question:**
A company has a production workload that runs on 1,000 Amazon EC2 Linux instances. The workload is powered by third-party software. The company needs to patch the third-party software on all EC2 instances as quickly as possible to remediate a critical security vulnerability. What should a solutions architect do to meet these requirements?
**Options:**
A. Create an AWS Lambda function to apply the patch to all EC2 instances.
B. Configure AWS Systems Manager Patch Manager to apply the patch to all EC2 instances.
C. Schedule an AWS Systems Manager maintenance window to apply the patch to all EC2 instances.
D. Use AWS Systems Manager Run Command to run a custom command that applies the patch to all EC2 instances.

### Question 11 (PDF Q#54)
**Topic:** EC2 / Storage / File Sharing
**Question:**
A company runs multiple Windows workloads on AWS. The company's employees use Windows file shares that are hosted on two Amazon EC2 instances. The file shares synchronize data between themselves and maintain duplicate copies. The company wants a highly available and durable storage solution that preserves how users currently access the files. What should a solutions architect do to meet these requirements?
**Options:**
A. Migrate all the data to Amazon S3. Set up IAM authentication for users to access files.
B. Set up an Amazon S3 File Gateway. Mount the S3 File Gateway on the existing EC2 instances.
C. Extend the file share environment to Amazon FSx for Windows File Server with a Multi-AZ configuration. Migrate all the data to FSx for Windows File Server.
D. Extend the file share environment to Amazon Elastic File System (Amazon EFS) with a Multi-AZ configuration. Migrate all the data to Amazon EFS.

### Question 12 (PDF Q#68)
**Topic:** Hybrid Connectivity (Networking/EC2 context)
**Question:**
A solutions architect is designing a new hybrid architecture to extend a company's on-premises infrastructure to AWS. The company requires a highly available connection with consistent low latency to an AWS Region. The company needs to minimize costs and is willing to accept slower traffic if the primary connection fails. What should the solutions architect do to meet these requirements?
**Options:**
A. Provision an AWS Direct Connect connection to a Region. Provision a VPN connection as a backup if the primary Direct Connect connection fails.
B. Provision a VPN tunnel connection to a Region for private connectivity. Provision a second VPN tunnel for private connectivity and as a backup if the primary VPN connection fails.
C. Provision an AWS Direct Connect connection to a Region. Provision a second Direct Connect connection to the same Region as a backup if the primary Direct Connect connection fails.
D. Provision an AWS Direct Connect connection to a Region. Use the Direct Connect failover attribute from the AWS CLI to automatically create a backup connection if the primary Direct Connect connection fails.

### Question 13 (PDF Q#124)
**Topic:** EC2 / Batch Processing
**Question:**
A company has a highly dynamic batch processing job that uses many Amazon EC2 instances to complete it. The job is stateless in nature, can be started and stopped at any given time with no negative impact, and typically takes upwards of 60 minutes total to complete. The company has asked a solutions architect to design a scalable and cost-effective solution that meets the requirements of the job. What should the solutions architect recommend?
**Options:**
A. Implement EC2 Spot Instances.
B. Purchase EC2 Reserved Instances.
C. Implement EC2 On-Demand Instances.
D. Implement the processing on AWS Lambda.

### Question 14 (PDF Q#128)
**Topic:** EC2 / Containers
**Question:**
A company wants to run applications in containers in the AWS Cloud. These applications are stateless and can tolerate disruptions within the underlying infrastructure. The company needs a solution that minimizes cost and operational overhead. What should a solutions architect do to meet these requirements?
**Options:**
A. Use Spot Instances in an Amazon EC2 Auto Scaling group to run the application containers.
B. Use Spot Instances in an Amazon Elastic Kubernetes Service (Amazon EKS) managed node group.
C. Use On-Demand Instances in an Amazon EC2 Auto Scaling group to run the application containers.
D. Use On-Demand Instances in an Amazon Elastic Kubernetes Service (Amazon EKS) managed node group.

### Question 15 (PDF Q#140)
**Topic:** Cost Optimization (EC2/Fargate/Lambda)
**Question:**
A solutions architect needs to help a company optimize the cost of running an application on AWS. The application will use Amazon EC2 instances, AWS Fargate, and AWS Lambda for compute within the architecture. The EC2 instances will run the data ingestion layer of the application. EC2 usage will be sporadic and unpredictable. Workloads that run on EC2 instances can be interrupted at any time. The application front end will run on Fargate, and Lambda will serve the API layer. The front-end utilization and API layer utilization will be predictable over the course of the next year. Which combination of purchasing options will provide the MOST cost-effective solution for hosting this application? (Choose two.)
**Options:**
A. Use Spot Instances for the data ingestion layer
B. Use On-Demand Instances for the data ingestion layer
C. Purchase a 1-year Compute Savings Plan for the front end and API layer.
D. Purchase 1-year All Upfront Reserved instances for the data ingestion layer.
E. Purchase a 1-year EC2 instance Savings Plan for the front end and API layer.

### Question 16 (PDF Q#167)
**Topic:** EC2 Spot vs Reserved
**Question:**
A company runs a production application on a fleet of Amazon EC2 instances. The application reads the data from an Amazon SQS queue and processes the messages in parallel. The message volume is unpredictable and often has intermittent traffic. This application should continually process messages without any downtime. Which solution meets these requirements MOST cost-effectively?
**Options:**
A. Use Spot Instances exclusively to handle the maximum capacity required.
B. Use Reserved Instances exclusively to handle the maximum capacity required.
C. Use Reserved Instances for the baseline capacity and use Spot Instances to handle additional capacity.
D. Use Reserved Instances for the baseline capacity and use On-Demand Instances to handle additional capacity.

### Question 17 (PDF Q#219)
**Topic:** EC2 Performance / Instance Types
**Question:**
A company’s application is having performance issues. The application is stateful and needs to complete in-memory tasks on Amazon EC2 instances. The company used AWS CloudFormation to deploy infrastructure and used the M5 EC2 instance family. As traffic increased, the application performance degraded. Users are reporting delays when the users attempt to access the application. Which solution will resolve these issues in the MOST operationally efficient way?
**Options:**
A. Replace the EC2 instances with T3 EC2 instances that run in an Auto Scaling group. Make the changes by using the AWS Management Console.
B. Modify the CloudFormation templates to run the EC2 instances in an Auto Scaling group. Increase the desired capacity and the maximum capacity of the Auto Scaling group manually when an increase is necessary.
C. Modify the CloudFormation templates. Replace the EC2 instances with R5 EC2 instances. Use Amazon CloudWatch built-in EC2 memory metrics to track the application performance for future capacity planning.
D. Modify the CloudFormation templates. Replace the EC2 instances with R5 EC2 instances. Deploy the Amazon CloudWatch agent on the EC2 instances to generate custom application latency metrics for future capacity planning.

### Question 18 (PDF Q#231)
**Topic:** EC2 Networking / Security
**Question:**
An application runs on an Amazon EC2 instance that has an Elastic IP address in VPC A. The application requires access to a database in VPC B. Both VPCs are in the same AWS account. Which solution will provide the required access MOST securely?
**Options:**
A. Create a DB instance security group that allows all traffic from the public IP address of the application server in VPC A.
B. Configure a VPC peering connection between VPC A and VPC B.
C. Make the DB instance publicly accessible. Assign a public IP address to the DB instance.
D. Launch an EC2 instance with an Elastic IP address into VPC B. Proxy all requests through the new EC2 instance.

### Question 19 (PDF Q#242)
**Topic:** Route 53 / EC2
**Question:**
A company hosts its web application on AWS using seven Amazon EC2 instances. The company requires that the IP addresses of all healthy EC2 instances be returned in response to DNS queries. Which policy should be used to meet this requirement?
**Options:**
A. Simple routing policy
B. Latency routing policy
C. Multivalue routing policy
D. Geolocation routing policy

### Question 20 (PDF Q#248)
**Topic:** EC2 CPU Scaling
**Question:**
A company runs analytics software on Amazon EC2 instances. The software accepts job requests from users to process data that has been uploaded to Amazon S3. Users report that some submitted data is not being processed Amazon CloudWatch reveals that the EC2 instances have a consistent CPU utilization at or near 100%. The company wants to improve system performance and scale the system based on user load. What should a solutions architect do to meet these requirements?
**Options:**
A. Create a copy of the instance. Place all instances behind an Application Load Balancer.
B. Create an S3 VPC endpoint for Amazon S3. Update the software to reference the endpoint.
C. Stop the EC2 instances. Modify the instance type to one with a more powerful CPU and more memory. Restart the instances.
D. Route incoming requests to Amazon Simple Queue Service (Amazon SQS). Configure an EC2 Auto Scaling group based on queue size. Update the software to read from the queue.

### Question 21 (PDF Q#251)
**Topic:** VPC / NAT
**Question:**
An Amazon EC2 instance is located in a private subnet in a new VPC. This subnet does not have outbound internet access, but the EC2 instance needs the ability to download monthly security updates from an outside vendor. What should a solutions architect do to meet these requirements?
**Options:**
A. Create an internet gateway, and attach it to the VPC. Configure the private subnet route table to use the internet gateway as the default route.
B. Create a NAT gateway, and place it in a public subnet. Configure the private subnet route table to use the NAT gateway as the default route.
C. Create a NAT instance, and place it in the same subnet where the EC2 instance is located. Configure the private subnet route table to use the NAT instance as the default route.
D. Create an internet gateway, and attach it to the VPC. Create a NAT instance, and place it in the same subnet where the EC2 instance is located. Configure the private subnet route table to use the internet gateway as the default route.

### Question 22 (PDF Q#253)
**Topic:** IAM Policies
**Question:**
A solutions architect has created two IAM policies: Policy1 and Policy2. Both policies are attached to an IAM group. A cloud engineer is added as an IAM user to the IAM group. Which action will the cloud engineer be able to perform?
*(See PDF for Policy JSON - Policy 1 allows Allow, Policy 2 Denies)*
**Options:**
A. Deleting IAM users
B. Deleting directories
C. Deleting Amazon EC2 instances
D. Deleting logs from Amazon CloudWatch Logs

### Question 23 (PDF Q#288)
**Topic:** EC2 / Shared Storage
**Question:**
A company is migrating a Linux-based web server group to AWS. The web servers must access files in a shared file store for some content. The company must not make any changes to the application. What should a solutions architect do to meet these requirements?
**Options:**
A. Create an Amazon S3 Standard bucket with access to the web servers.
B. Configure an Amazon CloudFront distribution with an Amazon S3 bucket as the origin.
C. Create an Amazon Elastic File System (Amazon EFS) file system. Mount the EFS file system on all web servers.
D. Configure a General Purpose SSD (gp3) Amazon Elastic Block Store (Amazon EBS) volume. Mount the EBS volume to all web servers.

### Question 24 (PDF Q#316)
**Topic:** EC2 / SQS / Cost
**Question:**
A company uses an Amazon EC2 instance to run a script to poll for and process messages in an Amazon Simple Queue Service (Amazon SQS) queue. The company wants to reduce operational costs while maintaining its ability to process a growing number of messages that are added to the queue. What should a solutions architect recommend to meet these requirements?
**Options:**
A. Increase the size of the EC2 instance to process messages faster.
B. Use Amazon EventBridge to turn off the EC2 instance when the instance is underutilized.
C. Migrate the script on the EC2 instance to an AWS Lambda function with the appropriate runtime.
D. Use AWS Systems Manager Run Command to run the script on demand.

### Question 25 (PDF Q#319)
**Topic:** EC2 Access (SSH)
**Question:**
A company has hundreds of Amazon EC2 Linux-based instances in the AWS Cloud. Systems administrators have used shared SSH keys to manage the instances. After a recent audit, the company’s security team is mandating the removal of all shared keys. A solutions architect must design a solution that provides secure access to the EC2 instances. Which solution will meet this requirement with the LEAST amount of administrative overhead?
**Options:**
A. Use AWS Systems Manager Session Manager to connect to the EC2 instances.
B. Use AWS Security Token Service (AWS STS) to generate one-time SSH keys on demand.
C. Allow shared SSH access to a set of bastion instances. Configure all other instances to allow only SSH access from the bastion instances.
D. Use an Amazon Cognito custom authorizer to authenticate users. Invoke an AWS Lambda function to generate a temporary SSH key.

### Question 26 (PDF Q#320)
**Topic:** EC2 / Data Ingestion
**Question:**
A company is using a fleet of Amazon EC2 instances to ingest data from on-premises data sources. The data is in JSON format and ingestion rates can be as high as 1 MB/s. When an EC2 instance is rebooted, the data in-flight is lost. The company’s data science team wants to query ingested data in near-real time. Which solution provides near-real-time data querying that is scalable with minimal data loss?
**Options:**
A. Publish data to Amazon Kinesis Data Streams, Use Kinesis Data Analytics to query the data.
B. Publish data to Amazon Kinesis Data Firehose with Amazon Redshift as the destination. Use Amazon Redshift to query the data.
C. Store ingested data in an EC2 instance store. Publish data to Amazon Kinesis Data Firehose with Amazon S3 as the destination. Use Amazon Athena to query the data.
D. Store ingested data in an Amazon Elastic Block Store (Amazon EBS) volume. Publish data to Amazon ElastiCache for Redis. Subscribe to the Redis channel to query the data.

### Question 27 (PDF Q#323)
**Topic:** EC2 vs Serverless for IoT
**Question:**
A company’s facility has badge readers at every entrance throughout the building. When badges are scanned, the readers send a message over HTTPS to indicate who attempted to access that particular entrance. A solutions architect must design a system to process these messages from the sensors. The solution must be highly available, and the results must be made available for the company’s security team to analyze. Which system architecture should the solutions architect recommend?
**Options:**
A. Launch an Amazon EC2 instance to serve as the HTTPS endpoint and to process the messages. Configure the EC2 instance to save the results to an Amazon S3 bucket.
B. Create an HTTPS endpoint in Amazon API Gateway. Configure the API Gateway endpoint to invoke an AWS Lambda function to process the messages and save the results to an Amazon DynamoDB table.
C. Use Amazon Route 53 to direct incoming sensor messages to an AWS Lambda function. Configure the Lambda function to process the messages and save the results to an Amazon DynamoDB table.
D. Create a gateway VPC endpoint for Amazon S3. Configure a Site-to-Site VPN connection from the facility network to the VPC so that sensor data can be written directly to an S3 bucket by way of the VPC endpoint.

### Question 28 (PDF Q#333)
**Topic:** EC2 Auto Scaling
**Question:**
A company’s application runs on Amazon EC2 instances behind an Application Load Balancer (ALB). The instances run in an Amazon EC2 Auto Scaling group across multiple Availability Zones. On the first day of every month at midnight, the application becomes much slower when the month-end financial calculation batch runs. This causes the CPU utilization of the EC2 instances to immediately peak to 100%, which disrupts the application. What should a solutions architect recommend to ensure the application is able to handle the workload and avoid downtime?
**Options:**
A. Configure an Amazon CloudFront distribution in front of the ALB.
B. Configure an EC2 Auto Scaling simple scaling policy based on CPU utilization.
C. Configure an EC2 Auto Scaling scheduled scaling policy based on the monthly schedule.
D. Configure Amazon ElastiCache to remove some of the workload from the EC2 instances.

### Question 29 (PDF Q#335)
**Topic:** EC2 Initialization Latency
**Question:**
A company is experiencing sudden increases in demand. The company needs to provision large Amazon EC2 instances from an Amazon Machine Image (AMI). The instances will run in an Auto Scaling group. The company needs a solution that provides minimum initialization latency to meet the demand. Which solution meets these requirements?
**Options:**
A. Use the aws ec2 register-image command to create an AMI from a snapshot. Use AWS Step Functions to replace the AMI in the Auto Scaling group.
B. Enable Amazon Elastic Block Store (Amazon EBS) fast snapshot restore on a snapshot. Provision an AMI by using the snapshot. Replace the AMI in the Auto Scaling group with the new AMI.
C. Enable AMI creation and define lifecycle rules in Amazon Data Lifecycle Manager (Amazon DLM). Create an AWS Lambda function that modifies the AMI in the Auto Scaling group.
D. Use Amazon EventBridge to invoke AWS Backup lifecycle policies that provision AMIs. Configure Auto Scaling group capacity limits as an event source in EventBridge.

### Question 30 (PDF Q#394)
**Topic:** EBS Performance
**Question:**
A company is running a multi-tier ecommerce web application in the AWS Cloud. The application runs on Amazon EC2 instances with an Amazon RDS for MySQL Multi-AZ DB instance. Amazon RDS is configured with the latest generation DB instance with 2,000 GB of storage in a General Purpose SSD (gp3) Amazon Elastic Block Store (Amazon EBS) volume. The database performance affects the application during periods of high demand. A database administrator analyzes the logs in Amazon CloudWatch Logs and discovers that the application performance always degrades when the number of read and write IOPS is higher than 20,000. What should a solutions architect do to improve the application performance?
**Options:**
A. Replace the volume with a magnetic volume.
B. Increase the number of IOPS on the gp3 volume.
C. Replace the volume with a Provisioned IOPS SSD (io2) volume.
D. Replace the 2,000 GB gp3 volume with two 1,000 GB gp3 volumes.
