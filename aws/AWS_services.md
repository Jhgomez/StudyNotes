{\rtf1\ansi\ansicpg1252\cocoartf2757
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\margl1440\margr1440\vieww30040\viewh16360\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 \
Cloud services\
\
CloudFormation\
Is a service that gives developers and businesses an easy way to create a collection(stack or stack set) of related AWS and/or third-party resources, and provision and manage them in an orderly and predictable fashion, that means you have the options to use the service-managed permission which means this service will automatically deploy the collection of resources to accounts in the organizational unit(OU) that this is applied/deployed or you can use the self-managed permissions. We can create things like a budget, threshold, set threshold warnings and alerts(SNS), and a lambda function and subscription that will execute when the threshold is near or reach the limit(ciritlcal) by using a JSON or YAML  file in which we describe the resources we want to create.\
\
CloudWatch\
Is a monitoring service for AWS resources and applications. Enables you to monitor your complete stack(applications, infrastructure, network and services) and use alarms, logs, and events data to take automated actions and reduce time of resolution.\
\
Budgets\
Is a service located under \'93AWS cost and management\'94 used to create custom budgets to track your usage and cost. It supports email or SNS(simple notification service) when actual or forecasted cost and usage exceeds the defined threshold. Integrated with cost explorers(you\'92re management account has to enable them), AWS chatbot to use it with slack or Amazon Chime room and AWS Service Catalog so that you can track cost on your approved AWS portafolios and products.\
\
Service Control Policies\
You can use this feature which is available in the account \'93Organization\'94 section. This feature enables central administration over the permissions available within the accounts in your organization. This helps ensure that your accounts stay within your organizations access control guidelines.\
\
IAM(Identity and Access management)\
Is a service located in \'93Security, Identify, & Compliance\'94 and it manages access to AWS resources. The root/management account is not commonly the one we want to use all the time and instead we usually another user/account and we do it using this service. \
\
IAM Identity Center\
Service located in \'93Security, Identify, & Compliance\'94. Manages workforce(users) user access to multiple AWS account and cloud applications.\
\
EC2\
This service is located in the \'93compute\'94 section and is used to launch virtual servers for running applications on the AWS infrastructure. Here we work with AMI(amazon machine image) which are the virtual computer setup we create/start to use as a server also auto-scaling groups which is set up to create AMIs, we can set up a minimum/maximun of servers running and the rules that has to be met in order for it to auto launch a new server for example if the cpu usage is too much and similar parameters. We also work with ELB(Elastic Load Balancer) they allow us to put a load balancer in front of our EC2 instances(servers) they will balance the traffic, that comes to your app, between different instances(servers) which usually will run in different AZs(Availability zone/data center) so performance is not impacted by distributing the load/input.\
\
SS3(Simple Storage Service)\
Is located in \'93storage\'94 section and it provides scalable storage in the cloud.\
\
CloudFront\
Located in \'93Networking and Content Delivery\'94 section, this service is used as a CDN(Content Delivery Network/ Content distribution network) which is a geographically distributed network of proxy servers and their data centers. Its goal is to provide high availability and performance by distributing the service spatially relative to end users. This means given a static content, for example: video files, music, files, it will copy that content to multiple edge locations around the world so when someone tries to access the content it will go to the nearby edge location as opposed to go really far away to get that content. So basically it help us deliver content securely with low latency and high transfer speed.\
\
AWS Trusted Advisor\
Service located under \'93Management & Governance\'94, it advises you on security, saving money, performance, service limits and fault tolerance. You can think of it like an automated checklist of best practices on AWS.\
\
	Cost Optimizations: The most common topics in this section it will advise you on are:\
		Idle Load Balancers\
		Unassociated Elastic IP Addresses\
\
	Security: A common topic it can advise you on is:\
		MFA on Root Account\
		IAM Access Key Rotation\
\
	Performance: A common topic it can advise you on is:\
		High utilization Amazon EC2 instances\
	\
	Fault Tolerance: A common topic it can advise you on is:\
		Amazon RDS Backpus\
\
	Service Limits: Some topics it can advise you on are:\
		VPC \
\
AWS Cost Explorer\
Is a service located under \'93AWS Cost Management\'94 section that lets you visualize, understand, and manage your AWS costs and usage over time. If there is multiple accounts in an AWS organization, costs will be consolidated in the master account.\
\
AWS Resource Groups and Tagging\
Resource Groups is service available in \'93Management & Governance\'93 Tags are words or phrases that act as metadata for organizing your AWS resources and Resource Groups are a collection of resources that share one or more tags. It helps you organize and consolidate information based on your project and the resources that you use. Resource groups can display details about a group of resources Resource Groups can display details about a group of resource based on: Metrics, Alarms, configuration.\
\
AWS Cost and Usage Report\
This is not a service, this is a feature. Generate a detailed spreadsheet, enabling you to better analyze and understand your AWS costs.\
\
Web ACL(Access control list)\
This is not a service from amazon, this is actually software developed to run in AWS cloud which gives you fined-grained control over all of the HTTP(S) web requests that your protected resource responds to. You can protect CloudFront, Amazon API Gateway, Application Load Balancer, AWS AppSync, Amazon Cognito, AWS App Runner and AWS Verified Access resources\
\
WAF Rules(Web Application Firewall Rules)\
Defines how to inspect HTTP(S) web requests and the action to take on a request when it matches the inspector criteria. You define rules only in the context of a rule group or web ACL. Rules don\'92t exist in AWS WAF on their own.\
\
RDS(Relational Database Service)\
\
Lambda\
Service located in the \'93Compute\'94 section. This service lets us run code without thinking about the server\
\
Route53\
\
Amazon API gateway\
\
\
\'97\'97\
Projects\
https://www.youtube.com/watch?v=5RVT3BN9Iws 3 projects in AWS to include in Resume\
\
Deploy a Wordpress Website on AWS\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
}