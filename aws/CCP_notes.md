# Cloud Practitioner(CCP)

Basic certification, light weight version of the certified architect solution, most people taking it are in sales and management due to the certification focus on billing and business-centric concepts which will allow to understand the reasons why you should use AWS

Content:

* **Cloud Concepts**:
	Define AWS cloud and its value propositions, identify aspect of AWS cloud economics, list cloud architecture design principles

* **Security**:
	AWS security service, shared responsibility model

* **Technology**:
	Core AWS services and other services, global infrastructure(regions, azs, edge locations)

* **Billing and pricing**:
	Compare and contrast different pricing models, recognize account structures in relating to EVA's billing and pricing, identify resource for billing support

We can use the following resources(Search in google): 

- Overview of AWs
- Architecting for the Cloud: AWS Best Practices 
- How AWS pricing works
- Cost management in the AWS Cloud
- Just go to the web page and compare/read about the support plans


# Cloud Concepts

### What is cloud computing?

Is the practice of using network of remote servers hosted on the internet to store, manage, and process data, rather than a local server or personal computer.

GCP and Azure are similar solutions to AWS, they all are cloud providers, which are solutions to run workloads. Previous to cloud providers this was done purely On-premise, but now we have three options, on-premise, hybrid(using both cloud and premise) and cloud. On-premise means 

- you own your own server(software and hardware)
- you need IT staff/personnel to configure the servers and applications
- you pay or rent the real-estate to house these fiscal servers
- you take all the risk

But now companies are using more cloud providers than on-premise solutions, Using cloud providers means:

- Someone else owns the servers
- Someone else hire the IT personnel
- Someone else pays/rents the real-estate
- You're responsible for configuring your cloud services and code that you deploy on to those services, and cloud providers takes care of the rest

### 6 Benefits of Cloud Computing/Cloud Providers over On-Premise

1. Trade capital expense for variable expense: No upfront-cost, instead of paying for data centers and servers instead, pay-on demand, meaning, pay only when you consume computing resources

2. Benefits for massive economies of scale: You're sharing the cost with thousands of customers to get unbeatable savings

3. Stop guessing capacity: You don't need to guess what the infrastructure capacity needs to be, instead of paying for underutilized servers, you can scale up or down to meet the current need.

4. Increase speed and agility: Launch resources within a few clicks in minutes, instead of waiting for the IT staff to implement to solution/configuration of the server

5. Stop spending on running and maintaining data centers: Focus on customers rather than the heavy lifting of racking, stacking and powering servers.

6. Go global in minutes: Deploy your app in different regions around the world with a few clicks.

### Types of cloud computing
 
- SssS(for customers): Software as a service, a complete product that is run and managed by the service provider. Don't worry about how the service is
	maintained, it just works and remains available. Examples: Salesforce, Gmail, Microsoft365,

- PaaS(for developers): Platform as service, removes the need for your organization to manage the underlying infrastructure, don't worry about provisioning,
configuring or understanding the hardware or OS. You can focus on the deployment and management of your app. Examples: Elastic Beanstalk(AWS), Heroku,
Engines(google)

- IaaS(for Administrators): infrastructure as a service. The building block for cloud IT. Provides access to networking features, computers and data storage space.
Don't worry about IT staff, data centers or hardware. Examples: AWS, google cloud platform, Microsoft Azure. With all the resources we can access in this
service we can build our own PaaS on top of this service/tools, also we can build our own SaaS on top of the PaaS or IaaS.

### Cloud Computing Deployment Models
	
* **Cloud**:
	Fully utilizing cloud computing. Examples: Squarespace, dropbox, basecamp. It is very well suited for start-up because it's extremely low-cost. Great for SaaS
	offerings where they don't need to deal with regulatory bodies or just the nature of the app is not too complicated. 

* **On-Premise**:
	Deploying resources on-premises, using virtualization and resource management tools, is sometimes called "private cloud". They use data centers, used in
	government, hospitals and large enterprises with heavy regulations like insurance companies.

* **Hybrid**:
	Uses both cloud and on-premise resources. It is used by banks, fintech, etc. Usually legacy code lives on-premise

### Global Infrastructure

3 years back there was 69 availabllity zones within 22 geographic regions around the world. There is regions which is a physical location in the world with multiple availability zones, also Availability zones are one or more discrete data centers and edge location which is a data center owned by trusted partner of was.

- **Regions**: Geographically distinct location with multiple data centers(AZs). They are physically isolated from and independent from other regions in terms of location and power supply, each one has at least two AZs, largest region is US-east and service almost always become available in this regions. Not all services	are available in all regions. US-east-1 is the region where you see all your billing info.

- **Availability** Zones/AZs (Data Centers): Data center in which AWS services run. Identified by a region code followed by letter identifier. Multi-AZ is when you're
distributing your instances across multiple AZs which allows failover configurations for handling requests when one goes down. There is a set latency between
AZs of <10ms.

- **Edge Locations**: Data centers own by a partner of AWS which has a connection to AWS network. This locations serve requests for CloudFront and Route53.
Request going to either of these services will be routed to the nearest edge location automatically. S3TransferAcceleration traffic and APIGateway endpoint
traffic also use the the AWS edge network. This allows for low latency no matter where the user is located.

- **GovCloud Regions(US)**: Special type of region which allow customers to host sensitive controlled unclessified info and other type of regulated workloads. Can
only be operated by US citizens and US soil, only accessible to US entities. 

### EC2 pricing model

- **On-Demand (Least commitment/cheapest)**: Low cost and flexible, for first time apps or experiment, short-term, spiky unpredictable workloads or run an
	experiment. Charged by the hour or by minute of use(Varies based on EC2 instances types). No upfront payment and no long term commitment

- **Reserved Instances (Best Long-term)**: Steady state or predictable usage, commit to EC2 over a 1 or 3 year term, allows reselling unused reserved instances.

- **Spot(Biggest Savings up to 90%)**: request extra/spare computing capacity, flexible commitment(start and end time), can handle interruptions, for non-critical
	background jobs. Similar to discounts when an airline makes discounts to fill vacant seats in a flight, AWS will offer discounts to maximize utility of their idle
	servers(unused resoures). The instance can be terminated by AWS at anytime if a customer paying a higher price needs it.

- **Dedicated(most expensive)**: Dedicated servers, can be on-demand or reserved(up to 70% off), when you need a gxuarantee of isolate hardware(enterprise
	requirement). Multi-tenat when multiple customers run their workload in the same server and Virtual Isolation is what separates the customers. Single tenant is
	when each customer runs their workload in a separate server/hardware

### Billing And Pricing

#### Free Services: 
- IAM
- VPC
- Organizations & Consolidation Billing
- AWS Cost Explorer

Free but Can Provision other AWS services which are not free

- **Auto Scaling** (probably will be on the exam so make sure to explain it could use some services which cost money)
- **CloudFormation** (probably will be on the exam so make sure to explain it could use some services which cost money)
- **Elastic Beanstalk** (probably will be on the exam so make sure to explain it could use some services which cost money)
- **Opsworks**
- **Amplify**
- **AppSync**
- **CodeStar**

#### AWS support plans

AWS has 4 different support plans, the basic support plan is the default. The basic support plan gives support via email for billing & account and technical info however this feature is available in all plans

~ means the hours within the email will be responded 

- **Basic**: Free, only benefit is email support for billing & account and technical , 7 trusted Advisor checks

- **Developer(20USD/month)**:Tech support via email 24~, no third party support,  general guidance support 24~,  system impaired support ~12, 7 trusted
	Advisor checks

- **Business(100USD/month)**: third party support, Tech support via email 24~, Tech support via chat/phone anytime 24/7,  general guidance support 24~, system
	impaired support 12~, Production System Impaired 4hrs, Production system down 1hr, all trusted advisor checks

- **Enterprise(15,000)**: third party support, Tech support via email ~24, Tech support via chat/phone anytime 24/7,  general guidance support 24~, system impaired
	support 12~, production System Impaired ~4, Production system down ~1, all trusted advisor checks, business-critical System Down ~15min, Personal
	concierge, TAM

### AWS Marketplace
Digital catalogue with thousands of software listings from independent software vendors. Easily find, buy, test and deploy software that already runs on AWS. Products can be offered as: Amazon Machine Images(AMIS), AWS Cloudformation templates, Software as a service(SaaS) offerings, Web ACL, AWS WAF rules


### AWS Trusted Advisor
Tool that advises you on security, saving money, performance, service limits and fault tolerance. You can think of it like an automated checklist of best practices on AWS.

- **Cost Optimizations**: The most common topics in this section it will advise you on are:
	- Idle Load Balancers
	- Unassociated Elastic IP Addresses

- **Security**: A common topic it can advise you on is:
	- MFA on Root Account
	- IAM Access Key Rotation

- **Performance**: A common topic it can advise you on is:
		High utilization Amazon EC2 instances
	
- **Fault Tolerance**: A common topic it can advise you on is:
		Amazon RDS Backpus

- **Service Limits**: Some topics it can advise you on are:
		VPC
		
### Consolidating Billing(Not service but a feature instead under the billing dashboard)
This feature is turned on by default whenever you're using service organizations and you have multiple accounts. It generates one bill for all your accounts, it treats all accounts in an organization as if they were one account. A master account can be designated to pay the charges of all other member accounts. This feature is offered at no cost usually. You can use cost explorer to visualize usage for consolidating billing per account.

* **Volume Discounts**:
There is discounts for many services, it means that the more you use as service the more you save. Consolidated billing lets you take advantage of Volume Discounts

### Cost Explorer
Lets you visualize, understand, and manage your AWS costs and usage over time. If there is multiple accounts in your AWS organizations the costs will be consolidated in the master accounts. Default reports help you gain insight into your cost drivers and usage trends, but you can make your custom reports

### Budgets
Is a service that gives you the ability to plan your service usage, service costs and instance reservations. Gives you the ability to set up alerts if you exceed or are approaching your defined budget. You can create cost, usage or reservation budgets. Can be tracked monthly quarterly or yearly level, with customizable start and end dates. They support EC2, RDS, Redshift, and ElasticCache reservations.

### TCO calculator
Total Cost of Ownership, allows to calculate savings when moving to AWS from on-premise. Provides detail set of reports that can be used in executive presentations. 

### AWS Landing Zone
Helps "Enterprises" quickly set-up a secure, AWS multi-account. This is not a service itself. Provides you with a baseline environment to get started with a multi-account architecture. So its basically a tool that will help you set up the architecture you need in your organization but the cost is a little high. This is all done via:

#### AWS Account Vending Machine
Automatically provisions and configure new accounts via Service Catalog Template, uses single sign-on(SSO) for managing and accessing accounts.


### AWS Resource Groups and Tagging
Resource Groups is service available in "Management & Governance" Tags are words or phrases that act as metadata for organizing your AWS resources and Resource Groups are a collection of resources that share one or more tags. It helps you organize and consolidate information based on your project and the resources that you use. Resource groups can display details about a group of resources Resource Groups can display details about a group of resource based on: Metrics, Alarms, configuration.

### AWS Quickstarts
It's not a device but h move down 300 lineselps deploy popular stacks on AWS. Reduce hundred of manual procedures into just a few steps.

### AWS Cost and Usage Report
This is not a service and can be found under the billing console. Generates a detailed spreadsheet, enabling you to better analyze and understand your AWS costs. Places the report into S3, Athena can be use to our the report into a queryable database, or use Quicksight to visualize your billing data as graphs

### Organizations and Accounts
- **Organizations**: Allow you to centrally manage billing, control access, compliance, security, and share resources across your AWS accounts
	
- **Root Account User**: Is a single sign-in identity that has complete access to all AWS services and resources in an account, each account has a root account user.

- **Organizations Units**: are a group of AWS accounts within an organization which can also contain other organizational units - creating hierarchy

- **Service Control Policies**: Give Central control over the allowed permissions for all accounts in your organization, helping to ensure your accounts stay within
	your organization's guideline

### AWS Networking
AWS Account contains Region which contains VPC which contains Availability Zones which contains a public subnet(it could contain a EC2 instance) and a private subnet(It could contain RDS DB service). The subnets receive information from a Internet gateway(enables access to the internet), the traffic from the subnets mentioned before get to a Route Tables which determined where the network traffic from the subnets are directed, it also exists NACLs which act as a firewall at the  server level(subnet) and they control access in and out to the subnets

### DataBase Services

- **DynamoDB** - NoSQL key/value database

- **DocumentDB** - NoSQL Document database that is MongoDB compatible

- **RDS** - Relational Database service that supports multiple engines like MySQL, Postgres, MariaDb, Oracle, micorosot SQL server, Aurora

	- **Aurora** - MySQL(5x fasterr)  and PSQL(3x faster) database fully managed

	- **Aurora Serverless** - Only runs when you need it, like AWS Lambda

- **Neptune** - Managed Graph Database

- **Redshift** - Columnar database, petabyte warehouse

- **ElastiCache** - Redis or, Memcached database
 
### Provisioning Services
Is the allocation or creation of resources and services to a customer

- **Elastic Beanstalk** - Service for deploying and scaling web applications and services developed with Java, .NET, PHP, Node.js, Python, Ruby, Go and Docker

- **OpsWorks** - Configuration management service that provides managed instances of Chef and Puppet

- **CloudFormation** - Infrastructure as code, JSON or YAML

- **AWS QuickStart** - Pre-made packages that can launch and configure your AWS compute, network, storage and other services required to deploy a workload on
AWS

- **AWS MarketPlace** - A digital catalogue of thousands of software listings from independent software vendors you can used to find, buy, test, and deploy software

### Computing Services
	
- **EC2** - Every service is using EC2 under the hood, Highly configurable server. For example CPU, Memory, OS

- **ECS** -Elastic Container Service, Docker as a service highly scalable, high performance container orchestration service that supports Docker containers, pay for
EC2 instances

- **Fargate** - Microservices where you don't think about the infrastructure. Play per task

- **EKS** - Kubernetes as a Service easy to deploy, manage and scale. Containerized apps using Kubernetes

- **Lambada** - Serverless functions run code without provisioning or managing servers. You pay only for the compute time you consume

- **Elastic Beanstalk** - Orchestrates various AWS services, like, EC2, S3. SNS, CloudWatch, Autoscalling And Elastic Load Balancers. Helps to develop, deliver full	stack web app

- **AWS Batch** - Plans, schedules your batch computing workloads across the full range of AWS compute services and features, such as Amazon EC2 and Spot
Instances

### Storage Services
- **S3(Simple Storage Service)** - Object storage, you can think of as an hard drive in the cloud, like a virtual hard drive with "unlimited" capacity/space

- **S3 Glacier** - similar to S3 but Low cost storage for archiving and long-term backup, is not expensive but tradeoff is it takes a lot of time sometimes to access the
files and there is a retrieval cost.

- **Storage Gateway** - Hybrid cloud storage with local caching. Think of it as an extension of your on-premise storage into the cloud. Can be used as a backup
solution for your local storage. 

- **EBS(Elastic Block Storage)** - Hard drive in the cloud you attach to EC2 instances. You can choose what hard drive you want it to be, so ti can be a SSD(solid
state drive), HHD etc

- **EFS(Elastic File Storage)** - File storage mountable to multiple EC2 instances at the same time, like a file system which you can mount to multiple EC2 instances
at same time

- **Snowball** - Physically migrate lots of data via a computer suitcase 50-80 TB. Is allows you to move lots of data around very quickly from on-premise network into
AWS or viceversa. When you order/allocate/reserve a snowball what you will get is something similar to a computer in the form of a suitcase with a lot of hard
drives in it which will you will upload your data quickly to that snowball and it will be delivered to S3. There is two types of snowballs

	- **Snowball Edge** - A better version of snowball, like snowball but with more features and space - 100TB, it can process data as its being inserted into
	snowball
	
	- **Snowmobile** - Shipping container, pulled by a semi-trailer truck, so it is just a giant snowball, or like a datacenter on wheels, metaphorically an AWS trailer
`	that is driven to your on-premise which you hook up to and then is driven back to AWS - 100 PB

### Business Centric Services

- **Amazon Connect** - Call center - Cloud-base call center service you can set up in just a few clicks - base on the same proven system used by Amazon customer
service teams. You can accept inbound calls, dial outbound calls and record calls and store them in S3, You can create workflows to route calls based on a set
of rules

- **Work Spaces** - Virtual Remote Desktop - Secure managed service for provisioning either Windows or linux desktops in just a few minutes which quickly scales
up to thousands of desktops. 

- **WorkDocs** - A content creation and collaboration service - easily easily create, edit, and share content saved centrally in AWS (the AWS version of sharepoint)

- **Chime** - AWS platform for online meetings, video conferencing, and business calling wich elastically scales to meet your capacity needs.

- **WorkMail** - Managed business email - contacts, and calendar service with support for existing desktop and mobile email email client applications.

- **Pinpoint** - Maketing campaign management system you can use for sending targeted email, SMS, push notifications, and voice messages

- **SES** - Simple Email Service - A cloud-based email sending service designed for marketers and application developers to send marketing, notification, and
emails. It is different for pinpoint in the sense that it could be used in smilier scenarios to sending an email notification/confirmation when someone registers in
the app and supports HTLM emails

- **QuickSight** - A business Intelligence (BI) service. Connect multiple datasource and quickly visualize data in the form of graphs with little to no programming
knowledge

### Enterprise Integration Services
Is about going hybrid, meaning bringing your on-prem and your AWS network together.
	
- **Direct Connect** - Dedicated Gigabit network connection from your premises to AWS. Imagine having a direct fibre optic cable running straight to AWS

- **VPN** - Establish a secure connection to your AWS network
	- **Site-to-site VPN** - Connecting your on-premise to your AWS network 
	- **Client VPN** - Connecting a Client(laptop/desktop) to your AWS network

- **Storage Gateway** - A hybrid storage service that enables your on-premises applications to use AWS cloud storage. You can use this for backup and archiving,
disaster recovery, cloud data processing, storage tiering, and migration.

- **Active Directory** - The AWS Directory Service for Microsoft Active Directory also known as AWS Managed Microsoft AD - Enables your directory-aware
workloads and AWS resources to use managed Active Directory in the AWS Cloud.

### Logging Services

- **CloudTrail** - Logs all API calls(SDK, CLI) between AWS services, helps us know who we should blame, you can get the following info from this service:

	- Who created this bucket?
	- Who spun up that expensive EC2 instance?
	- Who launched this SageMaker Notebook?
	- Detect developer misconfiguration
	- Detect malicious actors
	- Automate responses

- **CloudWatch** - Is a collection of multiple Services. It stores logs

	- **Cloudwatch Logs** - Performance data about AWS Services eg. CPU utilization, memory, network, application Logs eg. Rails, Nginx. Lambda Logs

	- **CloudWatch Metrics** - Represents a time-ordered set of data points. A variable to monitor
	
	- **CloudWatch Events** - Trigger an event based on a condition eg. Every hour take snapshot of server

	- **CloudWatch Alarms** - Triggers notifications based on metrics

	- **CloudWatch Dashboard** - Create visualizations based on metrics
	
### Initialisms

- IAM - identity and access management
- S3 - Simple storage service
- SWF - Simple workflow service
- SNS - simple notification service
- SQS - simple queue service
- SES - simple email service
- SSM - simple systems manager
- RDS - relational database service
- VPC - virtual private cloud
- VPN - virtual private network
- CFN - CloudFormation
- WAF - Web Application firewall
- MQ - Amazon ActiveMQ
- ASG - Auto scaling groups
- TAM - Technical account manager
- ELB - Elastic load balancer
- ALB - Application load balancer
- NLB - network load balancer
- EC2 - elastic cloud compute
- ECS - elastic container service
- ECR - elastic container repository
- EBS - elastic block storage
- EFS - elastic file storage
- EMR - elastic MapReduce
- EB - elastic Beanstalk
- ES - elastic search
- EKS - elastic kubernetes service
- MKS - managed Kafka service
- IoT - internet of things
- RI - reserved instances

### Shared responsibility model

Deals with security "of" and "in" the cloud

- **In** - Happens in data and configuration. Means you're responsible to secure the data that you upload to the cloud you should/can turn on monitoring services	which you would be responsible to configure also. You would be responsible to secure/configure the following: Customer data, platforms, applications, IAM,	operating systems, Network and firewall, client-side encryption, and data integrity authentication, server-side encryption(File system and/or), networking traffic 	protection(encryption, integrity, identity)

- **Of** - happens in hardware, operation of managed services and global infrastructure AWS is responsible for security of the cloud, so AWS is responsible to 	secure/configure: Software, compute, storage, database, networking, Hardware/AWS global infrastructure, region, AZ's, edge locations

### AWS compliance programs

They are a set of internal policies and procedures of a company to comply with laws, rules, and regulations or to uphold business regulation.
	
- Health Insurance Portability and Accountability Act(HIPAA) - is a USA legislation that provides data privacy and security provisions for safeguarding medical info

- Payment Card Industry Data Security Standard (PCI DSS) - when you want to sell things online and you need to handle credit card info

### (Security) AWS Artifact

How do we prove AWS meets a compliance? 

We use this service to generate reports that proves and explain how/what AWS is doing to comply with a program/certificate.

### (Security) Amazon Inspector (Security)

`Hardening is the act of eliminating as many security risks as possible`

#### How do we prove an EC2 instance is harden?

Inspector runs a security benchmark against specific EC2 instances. You can run a variety of security benchmarks.

Can perform both network and host assessments
1. Install AWS agent on your EC2 instances.
2. Run an assessment for your assessment target.
3. Review your findings and remediate security issues.

A very popular benchmark you can run is by CIS which has 699 checks.

### AWS Web Application Firewall(WAF) (Security)

AWS WAF protect your web applications, it allows you to write your own rules to allow or deny traffic based on the contents of an HTTP request. Use ruleset from a trusted AWS Security Partner in the AWS WAF rules marketplace. WAF can be attached to either CloudFront or an Application Load Balancer. Protect web applications from attacks covered in the OWASP Top 10 most dangerous attacks:
1. Injection
2. Broken Authentication
3. Sensitive data exposure
4. XML External Entities (XXE)
5. Broken Access control
6. Security misconfigurations
7. Cross Site Scripting (XSS)
8. Insecure Deserialization
9. Using Components with known vulnerabilities
10. Insufficient logging and monitoring

### AWS Shield (Security)

Is a managed DDoS (Distributed Denial of Service) protections service that safeguards applications running on AWS. DDoS attacks are a malicious attempt to disrupt normal traffic by flooding a website with a large amount of fake traffic. Service is offered at no cost and automatically used by all services.

When you route your traffic through Route53 or CloudFront you are using AWS Shield Standard. Protects you against Layer 3, 4 and 7 attacks where 7 is application, 4 is transport and 3 is network.

You can get the Shield Standard(free) version or a Shield Advance(3000USD/year)

### Penetration Testing
We can perform pentesting on AWS in some service and others are not permitted.

### AWS Guard Duty (Security)
Intrusion detection system and intrusion protection system. A device or software application that monitors a network or systems for malicious activity or policy violations. It is an IDS(Interaction detection system) and a IPS(Intrusion protection system)

Guard duty is a threat detection service that continuously monitors for malicious, suspicious activity and unauthorized behavior. It uses machine learning to analyze the following AWS logs: 
- CloudTrail Logs
- VPC Flow Logs
- DNS logs

It will alert you on findings which you can automate a incident response via cloudwatch events or with 3rd Party Services

### Key Management Service(KMS). (Security)
Managed service that makes it easy for you to create and control the encryption keys used to encrypt your data.

- KMS is a multi-tenant HSM(Hardware security module)
- Many AWS services are integrated to use KMS to encrypt your data wit a simple checkbox
- KMS uses Envelope Encryption

#### Envelope Encryption
When you encrypt your data, your data is protected, but you have to protect your encryption key. When you encrypt your data key with a master key as an additional layer of security.

### Amazon Macie
Is a Fully managed service that continuously  monitors S3 data access activity for anomalies, and generates detailed alerts when it detects risk of unauthorized access or inadvertent data leaks. Uses Machine Learning to analyze your cloud trail logs. It will identify your most at-risk users which could lead to a compromise.

Has a variety of alerts like: Anonymized Access, Config Compliance, Credential Loss, Location Anomaly, Open Permissions, Ransomware etc

### Security Groups vs NACLs
	
- **Security Groups** - Acts as a firewall at the instance level, implicitly denies all traffic. You create Allow rules. Eg. Allow an EC2 instance access on port 22 for SSH

- **NACLs(Network Access Control List)** - Acts as a firewall at the subnet level. You create allow and deny rules. Eg Blocks specific IP address known for abuse.

This means an instance will be protected with a security group, and a subnet which lives inside the instance will be protected with a NACL

### AWS VPN
Lets you establish a secure and private tunnel from your network or device to your AWS global network.

- **AWS Site-to-Site VPN** - Securely connects on-premises network or branch 
- **AWS Client VPN** - Securely connect users to AWS or on premises networks 

### Cloud Services

- **Direct Connect** - Dedicated Fiber Options connections from Data center to AWS. A large enterprise has their own datacenter and they need an insanely fast	connection directly to AWS. If you need security apply a VPN connect on-top of Direct Connect

- **Amazon Connect** - Call center service. Get a toll free number, accept inbound and outbound calls, setup automated phone systems.

- **Media Connect** - New version of Elastic Transcoder, Coverts videos to different video types. You have 1000 of videos and you either need to format them in a 	different format, maybe you need to apply watermarks or insert introductions video in front of every video.

#### Elastic Transcoder Vs Media Convert
Both do same thing, they transcode videos, but media convert is the new version and with new features

### SNS vs SQS (Comparison)

- **SNS Simple Notifications Service** - Located under "application integration" Sends notifications to subscribers of topics via multiple protocol eg. HTTP, Email,	SQS, SMS. Is generally used for sending plain text emails which is triggered via other AWS services like billing alarms. Can retry sending in case of failure for	http(s). Good for web hooks, simple internal emails, triggering lambda functions.

- **SQS Simple Queue Service** - Places messages into a queue. Applications pull queue using AWS SDK. Can retain a message for up to 14 days, send them in 	sequential order or in parallel, ensure only message is sent, ensure messages are delivered at least once. It's good for delayed tasks, queueing up emails.

### Amazon Inspector vs AWS Trusted Advisor
Both services have a security component involved in them.

- **Amazon Inspector** - Audits a single EC2 instance that you've selected. Generates a report from a long list of security checks i.e. 699checks

- **Trusted Advisor** - Doesn't generate out a PDF report. Gives you a holistic view of recommendations across multiple services and best practices.

### ALB vs NLB vs CLB
Before ALB and NLB all there was is classic load balancer and then it was renamed to elastic load balancer. You can attach the amazon certification manager to the load balancers so you can apply SSL/TLS and get HTTPS traffic

- **Application Load Balancer** - Layer 7 requests, HTTP(S) traffic. Routing rules, more usability from one load balancer. Can attach WAF

- **Network Load Balancer** - Layer 4 IP protocol data. TCP and TLS where extreme performance is required. Capable of handling millions of requests per second 	while maintaining ultra-low latencies. Optimized for sudden volatile traffic patterns while using a single static IP address per Availability Zone

- **Classic Load Balancer(Old)** - Layer 4 and 7. Intended for applications that were built within the EC2-Classic network, doesn't use target groups

### SNS Vs. SES

- **Simple Notification Service** - Is a more practical and internal option. Sends notifications to subscribers of topic via multiple protocol. Eg, HTTP, Email, SQS, 
SMS and lambdas. Generally used for sending plain text emails which is triggered via other AWS services. A good example is billing alarms. A lot of services
can trigger SNS so it is a very common exam question. You need to know what are Topics and Subscriptions regarding SNS

- **Simple Email Service** - Is a more professional option and is more suitable for marketing. Cloud base email service. Eg. SendGrid(not amazon service). SES 
sends html email while SNS cannot do that. This service can receive inbound emails, create email templates. It features custom domain name email. Allows 
you to monitor your email reputation.

### Artifact vs Inspector
They both compile up PDF reports

- **AWS Artifact** - The report is focused on explaining why an enterprise should trust AWS. Generates a security report that is based on global compliance frameworks
such as: Service Organization Control(SOC), Payment Card Industry (PCI)

- **AWS Inspector** - The report evaluates if an EC2 instance is secure and to proves how is or not secure. Runs a script that analyzes a EC2 instance, then 	generates a PDF report telling you which security checks passed. Audit tool for security of EC2 instances






}