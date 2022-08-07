# **Cloud Computing**

- using network of remote servers hosted on internet to store, manage and process data, rather than a local server or PC
### Benefits of using cloud computing over on-premise:
1. no upfront-cost (paying for data centers and servers), just pay on-demand(pay how much we use)
2. share the cost with other people to enjoy savings
3. easy to scale up or down to meet the current need
4. increase speed and agility (launch resources within a few clicks in minutes), don have to wait for IT to implement the solution
5. can focus on customers, instead of spending money and time on running and maintaining data centers
6. able to deploy app in multiple regions across the world, provide low latency and better experience

### Types of Cloud Computing:
1. **SaaS (Software as a Service)**
-> straight use the product, no need to worry how its deployed and maintained (eg: gmail, office365)
2. **PaaS (Platform as a Service)**
-> no need to worry about the infrastructure, can focus on the deployment and management of the app (eg:heroku)
3. **IaaS (Infrastructure as a Service)**
-> provide access to networking features, computing resources and data storage (eg:AWS,GCP,Azure)

### Cloud Computing Deployment:
1. **Fully Cloud** -> Startups, New projects and companies
2. **Hybird (Cloud + On-Premise)** -> Banks, FinTech, Large Professional Service Providers
3. **On-Premise** (using virtualization and resource management tools, sometime called "private cloud") -> Public Sector (Government), Hospitals (sensitive data), Insurance Companies

### AWS Global Infrastructure
1. **Regions**
- Physcial location in the world with multiple **Availabiltiy Zones (AZ)**
- every region is isolated and independant of other regions in terms on **location,power,water supply**
- each **region** has at least 2 **AZ**, AWS largest
- AWS largest region is **US-EAST**
- **US-EAST-1** is the region to check billing information
- not all services are availabe in all regions
2. **Availabiltiy Zones (AZ)**
- owned and operated by AWS
- **AZ** is represented by **Region Code**, eg: us-east-1**a**
- **Multi-AZ** distribute our instances accross multiple AZs, allowing failover configuration for handling requests when one goes down
- **<10ms** latency between **AZ**
3. **Edge Location**: 
- Datacenter owned by trusted partner of **AWS** which has a direct connection to AWS network
- These locations serve requests for **CloudFront** and **Route53**, requests going to either of these services will be routed to the nearest **Edge Location** automatically
- **S3 Transfer Acceleration** traffic and **API Gateway** endpoint traffic uses AWS Edge Network
- Allow low latency no matter where the end user is geographically located

![alt text](https://miro.medium.com/max/574/1*TEJ_LssGeBc8NoYQ0BsUMg.png)

### GovCloud(US)
- AWS GovVloud Regions can host sensitive **COntrolled Unclassified Information** and other regulated workloads
- only opertaed by employees who are U.S Citizens
- only accessible to U.S entities and root account holders who pass a screening process

# **AWS Management Console + UI**

- When we first create the AWS account we are the **ROOT** user
- **ROOT** user is like admin, when we want to work in group we need to create more user and assign them different access

1. **Billing Preferences** => Go to -> Your Account -> My Billing Dashboard -> Billing Preferences (on left hand side) -> Tick the necessary boxes and click **Save Preferences**
2. **Budgets** => Go to **Home Management Console** -> Search **AWS Budgets** (cost 2 cents per day for budgets)
3. **Alarms** => Go to **Home Management Console** -> Search **CloudWatch** -> Go to Billing (on left hand side) -> Might need to change region at the top right to **US-EAST-1**

### **Identity Access Management (IAM)**
Things need to do:
1. Activate Multi-Factor Authentication (MFA) on AWS root account (in case of account or password leakage)
2. Create individual IAM users => Go to **Manage Users** -> Add User -> Generally set them as **Power user**
3. user groups to assign permissions
4. Apply IAM password policy (force users created password to meet certain criteria)=> go to **Manage password policy** -> **set password policy** under password policy

# **Launch a Server**

1. Go to **Home Management Console** Search bar
2. Search for **EC2 (Elastic Compute Cloud 2)**
3. Click **Launch Instance** under **Create Instance** (**Instance == Server**)
4. Choose the OS (Linux,RedHat)
5. Choose the size of the server
6. Create IAM Role (Select EC2, usually select **AmazonEC2RoleforSSM** (**SSM == Simple System Manager**)), then re-select the role created in the drop down
7. Choose Storage size
8. Launch Instances

# **Shut down a server**

1. Go to **actions**
2. go to **Instance State**
3. Select **Terminate** OR **Stop**

# **Connect to a sever**

- **Thorugh SSH browser-based connection**
1. Right click on any instances
2. Select **connect**
3. Select **EC2 Instance Connect**

- **Through Simple System Manager**
1. Search **SSH** in the search bar
2. Select **Session Manager** on the left-hand side
3. Then select **Start Session** on right hand side
- Session Manager provides more visibility than SSH

# **Amazon Machine Image (AMI)**
- AMI is like a snapshot of the server
- contains the software configuration (OS, App Server, and App) required to launch the instance
- can select AMI provided by AWS, or user community, or **marketplace**, or even own AMI
- when we have AMI, if we want to launch another copy of the server we can just launch using the AMI
1. Go to **Actions**
2. Select **Image**
3. Select **Create Image** (can still create when the server stop running)

# **Auto Scaling Group**
- Auto Scaling Group is to ensure multiple instances or server is running, and to meet the demand traffic
- For example the traffic metrics show traffic is high it will auto spin up new servers, and when the demand gets lower then it will remove servers
1. Go to **EC2 Dashboard**
2. Go to **Auto Scaling** on left-hand side
3. Select **Auto Scaling Groups**
4. Click **Create Auto Scaling Group**
5. **Group Size** is the min number of servers should be running at all time

# **Elastic Load Balancer**
- put load balancer in front of instances
- when traffic come into our app, it will flow through the load balancer, and it will evenly distribute that traffic to multiple instances, these instances generally will be running in different **AZ**
1. Go to **EC2 Dashbaord**
2. Go to **Load Balancing** on left-hand side
3. Select **Load Balancers**
4. Usually will select **Application Load Balancer**
5. **Target Gorup** contians reference to instances which we want to route traffic to
- every load balancer has a **DNS Name**, all traffic will be route to the **DNS Name** (like a domain), then to the listeners, where the listeners listen on a particular port
- If delete **Load Balancer**, need to manually delete the instances, unlike **Auto Scaling** where it will automatically delete the instances when terminating the **Auto Scaling Group**

# **Simple Storage Service (S3)**
- S3 doesnt require region selection
- **Bucket** is a place to store our files, it is region-specific
- Bucket name is globally unqiue

# **CloudFront**
- **CloudFront** is a CDN, content distribution network
- lets say we have files that would like to share globally, and want to share to as fast as possible (make the shortest route to end user)
- CDN takes static content and copy to multiple edge locations around the world
1. Search **CloudFront** in the search bar
2. Click **Create Distribution**
3. Click **Get Started**
- **CloudFront** also has a domain name, traffic will hit the domain name, then it will route the traffic to the nearest edge location

# **Relational Database Service (RDS)**

1. Go to **Search bar** and search for **RDS**
2. Click **Databases** on left-hand-side
3. Click **Create database** on right-hand-side
- **Prices from expensive to cheap** => Production -> Dev/Test -> Free Tier (free for 750 hours)
4. **Endpoint & Port** is needed to connect to the database

# **Lambda**
- Lambda allows us to create functions that runs for a small amount of time (15mins)
1. Go to **Search bar** and search for **Lambda**
2. Click **Create function** on right-hand-side
3. Then click **create function**
4. Edit the function and click **test**

# **EC2 Pricing Models**

1. **On-Demand (Least commitment) => Pay what you use**
- low cost, flexible
- only par per hour or per minute
- cannot be interrupted
- **use cases:** for first time apps, short-term

2. **Spot (up tp 90%) Biggest Savings => Use what is left**
- suitabel for app that have flexible start and end times, or feasible at very low compute costs
- **use cases:** can handle interruptions (server randomly stopping and starting)
- **use cases:** for non-critical background jobs
- trade off: instances can be terminated at any given time
- if AWS terminate the instances we wont be charged for that partial hour
- ideal when workload cannot be interrupted

3. **Reserved (up to 75%) best Long-term => Book and use**
- steady state or predictable usage
- can resell unused reserved instances
- reduced pricing is based on **Term X Class Offering X Payment Option**
- Payment Terms: 1 or 3 years
- Payment options: All upfront / Partial Upfront / No Upfront
- Class Offerings:
- (a) **Standard** -> up to 75% reduced pricing compared to on-demand, cannot change isntance attributes 
- (b) **Convertible** -> Up to 54% reduced pricing compared to on-demand, allows to change instances attributes if greater or equal in value
- (c) **Scheduled** reserve instances for specific time periods (eg: few hours every week), saving vary

4. **Dedicated (Most Expensive) => Use an entire server**
- dedicated servers
- can be on-demand reserved (up tp 70% off)
- **use cases:** when require isolate hardware (enterprise requirements)
- when have **strict-bound-licensing** that wont support multi-tenancy or cloud deployments
- can be on-demand or reserved

### Multi-Tenant
- multiple customers running workloads on the same hardware
- **virtual isolation** is what sepeartes the customers (think apartment)

### Single Tenant
- single customer has dedicated hardware
- **Phyiscal isolation** is what seperates customers (think house)

# **AWS Free Services**

1. TOTALLY FREE:
- IAM (Identity Access Management)
- Amazon VPC
- Organizations & COnsolidated Billing
- AWS Cost Explorer

2. FREE BUT MIGHT COST EXTRA MONEY DEPENDS ON REQUIRMENT AND USAGE
- Auto Scaling
- CloudFormation
- Elastic Beanstalk
- Opsworks
- Amplify
- AppSync
- CpdeStar

# **AWS Support Plans**

1. Basic
- Email support only
- for billing and Account
- 7 Trusted Advisor Checks
- 0 USD/month

2. Developer
- All Basic previlege
- Teach Support via email
- No 3rd party support
- General Guidance (< 24 hrs)
- System Impaired (< 12 hrs)
- 20 USD/month

3. Business
- All Developer previlege
- Tech Support via chat & Phone (24/7)
- Production System impaired (fixed < 4 hrs)
- production system down (fixed < 1 hrs)
- can do screen sharing, let them remotely solve for us
- All Trusted Advisor Checks
- 100 USD/month

4. Enterprise
- All Business previlege
- Business Critical System Down (fixed < 15m)
- **Personal Concierge** & **Technical Account Manager**
- 15,000 USD/month

![alt text](https://awsnewbies.com/wp-content/uploads/2018/09/supportplans.png)

### **Business and Enterprise will help 3rd party issues that aren't database-related**
### **FOR EXAM NEED TO KNOW THE PRICING AND RESPONSE TIME FOR EACH TIER!!!**

# **Create a Support Case**
1. Go to **Support Center**
2. Click on **Create case**

# **AWS Marketplace**
- a market with **thousands** of software listings from independant software vendors
- can find, buy, test, and deploy software that already runs on AWS
- can be free or can have **associated charge**, the charge goes to the service provider
- eg: OS, Security, Networking, Storage, BI, Databases, Dev Ops, ML
- can also sell service or software at AWS marketplace

# **Marketplace Subscription**
- when we want to use a marketplace resource, we will launch it within the context of what services we're using

# **AWS Trusted Advisor**
- advises us on **security, saving money, performance, service limits, and fault tolerance**
- it's like an automated checklist of best practises on AWS
- **BASIC or DEVELOPER** can have 7 free **Advisor Checks**
- **BUSINESS or ENTERPRISE** can have unlimtied

1. Cost Optimization
- **Idle Load Balancers** => idle non-used load balancers
- **Unassociated Elastic IP Address** => release non-used static IP address

2. Performances
- **High Utilization Amazon EC2 Instances** => if it detects high CPU utilization on an instance, it will recommned to use a larger instance to get better performance

3. Security
- **MFA on Root Account** => Set up Multi-Factor Authentication
- **IAM Access Key Rotation** => recommed to rotate keys used by users to keep things secure

4. Fault Tolerance
- **Amazon RDS Backups** => Suggest to turn on backups occasionally

5. Service Limits
- **VPC**

### How to view Trusted Advisor?
1. Go to **Trusted Advisor Management**
2. View suggestions recommended by **Trusted Advisors**
3. Can set up weekly basis email notification on the **suggestions and advices**

# **Consolidated Billing**

- let's say there's 1 **master account** and many **member accounts** in an organization
- all **member accounts** billing information is going to be sent to the **master account**
- **master account** is responsible for paying all the charges
- consolidated billing feature is **FREE**
- can use **Cost Explorer** to visualize usage for consolidated billing

# **Consolidated Billing Volume Discounts**
- the more we use something the more we are going to save
- **consolidated billing** let us take advantage of colume discounts because it take volume usage from multiple accounts and treat it as one

# **AWS Cost Explorer**

- tool that helps us visualize, understand, and manage AWS cost and usage over time
- if we have multiple accounts in one organization, all the costs will be consolidated into the master account

# **AWS Budgets**
- a service that help plans service suage, service costs and instances reservations
- first 2 budgets is Free-of-charge, roughly $0.02 per day
- can set alert if we exceed defined budget **(Cost, Ussage, Reservation)**
- can tracked at **monthly, quarterly, yearly** levels
- alerts support **EC2,RDS,Redshift & ElastiCache** reservations

1. Go to **AWS Budgets**
2. Click **Create a budget** on the right-hand-side
3. Do the necessary settings and click **Configure alert**
4. Click **Confirm Budget**

# **Total Cost of Ownership (TCO) Calculator**
- allows user to estimate how much can be saved when moving from on-premise to AWS
- provides detail set of reports that can be used in **executive presentations** or as a **persuasion tool**, to convince the management to mirate infrstructure to AWS

# **AWS Landing Zone**
- Helps enterprises quickly set-up AWS multi-account
- provides a **baseline environment** to get started with multi-account architecture
- **Account Vending Machine (AVM)** creates new accounts via **Service Catalog Template**, and uses **Single Sign-On (SSO)** for managing and accessing accounts
- environment is customizable to allow customers to implement own account baseliness throught Landing Zone conifguration and update pipeline

# **Resources Groups and Tagging**
- **Tags** => words or phrases that act as metadata for organizing AWS resources
- **Resource Groups** => group of resources that share one or more tag, helps organize consolidated information based on project
1. Search **EC2** in the searchbar
2. Launch any instanes
3. After creating instances, go to drop-down list in **resource groups** in the dashboard

# **AWS Quick Starts**
- **prebuilt templates** by AWS and AWS partners to help deploy popular stacks on AWS
- reduces manual procedures into just a few steps
- references that enables us to spin up a fully functional architecture in less than an hour

# **AWS Cost and usage Report**
- generate a detailed spreadhseet that enables us to better analyze and understand our AWS costs
1. Go to **My billing dashboard**
2. Go to **Cost & Usage Reports** on the left-hand-side
3. Click **Create report**
4. First report will be delivered to **S3 bucket** after creation
5. Go the the bucket created, then **cost and usage** folder, find the report inside there

# **AWS Organizations and Accounts**
- when first sign up for AWS, we are creating a single account
- the first user we're logged is the root user
- we can promote the account into an organization, that will allow us to create multiple accounts within that organization
- the reason for this is because we might want to isolate different departments within our company, and have fine tuned control over what they have access to
- **Organizations**: allow us to centrally manage billing, control access, compliance, security, and share resource across AWS accounts
- **Root Account User**: single sign-in identity that has complete access to AWS services and resources in an account, each account has 1 **Root Account User**
- **Organization Units**: group of AWS accounts within an organization which can also contain other organizational units, creating a hierarchy
- **Service Control Policies**: give central control over the allowed permission for all accounts in the organization, helping to ensure the account stay within our organization's guideline
1. Go to **Identity and Access Management (IAM)**
2. Click **Organization Activity** under **AWS Organizations** on the left-hand-side
3. If havent create search **AWS Organizations** in the search bar
4. Create a new policy
5. Enable **service control policies** at root account
6. Then attach the desired policy for the **Organization Units** that we want

![alt text](https://docs.aws.amazon.com/organizations/latest/userguide/images/AccountOuDiagram.png)

# **AWS Networking**
- **Region**: geographical location of our network
- **AZ**: data center of the AWS resources
- **Virtual Private Cloud (VPC)**: a logically isolated section of the AWS Cloud where we can launch AWS resources
- **Internet Gateway**: Enable access to the internet (act as a door to the internet)
- **Route tables**: determine where network traffic from our subnets are directed
- **NACLs**: acts as firewall at subnet level
- **Security gorups**: act as firewall at instance level
- **Subnets**: a logical partition of an IP network into multiple, smaller network segments
- Public Subnet is accessible to the internet, whereas private subnet is not
- usually things need to be secure are put in private subnets

# **AWS Databases Services**
- **DynamoDB** - NoSQL *key/value* db
- **DocumentDB** - NoSQL *Document* db that is MongoDB compatible
- **RDS** - *Relational* db that supports **MYSQL,Postgres,Maria DB,Oravle,Microsoft SQL server, Aurora**
- **Aurora**: MYSQL (5x faster) and PSQL (3x faster) db **fully managed**
- **Aurora Serverless**: only runs when we need it, like AWS lambda
- **Neptune** - *Managed graph* db
- **Redshift** - *Columnar* db, *petabyte* warehouse
- **ElastiCache** - *Redis* or *Memcached* db

### exam only need to know **DynamoDB, RDS, Aurora and Redshift**

# **Provisioning Services**
- provisioning is the allocation or creation of resources and services to a customer
- **Elastic Beanstalk**: service for deploying and scaling web app and service
- **OpsWorks**: configuration management services that provides managed instances of **Chef** and **Puppet**
- **CloudFormation**: Infrastructure as code, **JSON** or **YAML**, define all AWS resources that we need and how to configure them
- **AWS QuickStart**: packages than can launch and configure AWS compute, network, storage, and other services required to deploy a workload on AWS
- **AWS Marketplace**: a digital market of software listings and services where we can use to find, buy, test and deploy software

# **AWS Computing Services**
- **EC2**: Elastic Compute Cloud, highly configurable server (can configure for CPU, memory, network, OS)
- **ECS**: Elastic Container Service **(Docker as a Service)** highly scalable, high-performance container orchestration service that supports Docker containers, pay for EC2 instances
- **Fargate**: Microservices where we don need to worry about the infrastructure, pay per task
- **EKS**: Kubernetes as a Service, easy to deploy, manage and scalre containerized app using Kubernetes
- **Lambda**: serverless function that runs code without provisioning or managing servers, only pay for the compute time we consume
- **Elastic Beanstalk**: orchestrates various AWS srevices, including EC2, S3, Simple Notification Services (SNS), CloudWatch, autoscaling, and Elastic Load Balancers
- **AWS Batch**: plans, schedules, and executes the batch computing workloads across the full range of AWS compute services and features, such as Amazon EC2 and Spot Instances

# **AWS Storage Services**
- **S3**: Simple Storage Service - object storage (hard drive in the cloud)
- **S3 Glacier**: low cost storage for archiving and long-term backup, need to wait for some time to access those files
- **Storage Gateway**: hybrid cloud storage with local caching
- **EBS**: Elastic Block Storage, hard drive cloud attached to EC2 instances
- **EFS**: Elastic File Storage,m file storage mountableto multiple EC2 instances at the same time
- **Snowball**: physically migrate lots of data via a computer suitcase
- **Snowball Edge**: a better version of snowball - 100TB
- **Snowmobile**: shipping container, pulled by a semi-trailer truck
- **EBS** can only attached to 1 EC2, where **EFS** can attach to multiple EC2

# **Business Centric Services**
- **Amazon Connect**: Call center, cloud-based call center service
- **Workspaces**: Virtual Remote Desktop, service for Windows or Linux desktops configuration
- **WorkDocs**: content creation and collaboration service
- **Chime**: platform for online meetings and video conferencing
- **WorkMail**: manage business email
- **pinpoint**: marketting campaign management system that we can use for sending targeted email, SMS, push notifications and voice messages
- **SES (Simple Email Service)**: clooud-based email sending services to send marketting notifications and email
- **QuickSight**: BI service that connect multiple datasource and visualize data in the form of graphs with little to no programming knowledge

# **Enterprise Integration**
- **Direct Connect**: network connection from our premise to AWS (like a direct fibre optic cable running straight to AWS)
- **Virtual Private Network (VPN)**: establish a secure connection to AWS network
- **Site-to-Site VPN**: connects our on-premise to AWS network
- **Client VPN**: connects a client(laptop) to AWS network
- **Storage Gateway**: hybrid storage service that enables on-premises apps to use AWS cloud storage, can use for backup and archiving, disaster recovery, clpoud data processing, storage tiering and migration
- **Active Directory**: AWS directory service, enables our directory-aware workloads and AWS resources to use managed Active Directory in the AWS Cloud

# **Logging Services**
- **CloudTrail**: logs all API calls (SDK,CLI) between AWS services
- **CloudWatch Logs**: performance data about AWS services (CPU utilization, memory, network), applications log (Rails,Nginx), Lambda logs
- **CloudWatch Metrics**: Represents a time-ordered set of data points (variable to monitor)
- **CloudWarch Events**: trigger an event based on condition (take snapshot of server every hour)
- **CloudWatch Alarms**: trigger notifications based on metrics(graphs)
- **CloudWatch Dashboard**: cerate visualization based on metrics(graphs)

# **Abbrevations**
1. IAM - Identity and Access Management
2. S3 - Simple Storage Service
3. SWF - Simple Workflow Service
4. SNS - Simple Notification Service
5. SQS - Simple Queue Service
6. SES - Simple Email Service
7. SSM - Simple Systems Manager
8. RDS - Relational Database Service
9. VPC - Virtual Private Cloud
10. VPN - Virtual private network
11. CFN - cloudformation
12. WAF - Web Application Firewall
13. MQ - Amazon ActiveMQ
14. ASG - Auto Scaling Groups
15. TAM - Technical Account Manager
16. ELB - Elastic Load Balancer
17. ALB - Application load balancer
18. NLB - network load balancer
19. EC2 - elastic cloud compute
20. ECS - elastic container service
21. ECR - elastic container repository
22. EBS - elastic block storage
23. EFS - elastic file storage
24. EMR - elastic MapReduce
25. EB - Elastic Beanstalk
26. ES - ElasticSearch
27. EKS - Elastic Kubernetes Service
28. MKS - Managed Kafka Service
29. RI - reserved instances

# **Shared Responsbility Model**
- user is responsible for security in the Cloud (Data Configuration)
- AWS is responsible for Secrity of the Cloud (Hardware, Operation of Managed Servcies, Global Infrastructure)

![alt text](https://d1.awsstatic.com/security-center/Shared_Responsibility_Model_V2.59d1eccec334b366627e9295b304202faf7b899b.jpg)

# **AWS Compliance Programs**
- compliance programs are a set of internal policies and procedures of a company to comply with laws, rules, and regulations to uphold business reputation
- **Health Insurance Portability and Accountability Act (HIPAA)**: US legislation that provides data privacy and security provisions for safeguarding medical info (hospital must be HIPAA Compliant)
- **The Payment Card Industry Data Security Standard (PCI DSS)**: when want to sell thing online, need to handle credit card info, must be PCI DSS compliant

# **AWS Artifact**
- can access to AWS security and compliance reports to prove if AWS meets a compliance
1. Search **artifact** in the search bar

# **Amazon Inspector**
- **hardening**: act of eliminating as many security risks as possible
- AWS Inspector runs a security benchmark against specific EC2 instances (can perform both entwork and host assessments)
1. Install AWS agent on EC2 instances
2. run an assessment for the assessment target
3. review the findings and remediate security issues

# **AWS Web Application Firewall (WAF)**
- protect our web app from common web exploits
- write our own rules to ALLOW or DENy traffic based on contents of HTTP requests
- use a **ruleset** from a trusted AWS security partner
- WAF can be attached to either **CloudFront** or **Application Load Balancer**

# **AWS Shield**
- a managed DDoS protection service that safeguards apps on AWS
- customers benefit from the automatic protections of AWS Shield Standard for free
- when we route traffic through Route53 or CloudFront we are using AWS Shield Standard
- Protects against Layer 3,4,7 attacks (3-network,4-transport,7-application)
- **Shield Standard**: protection against most common DDoS attack, automatically available on all AWS services
- **Shield Advanced (3000 USD/year)**: additional protection against larger or more sophisticated attacks, visbility into attacks (reports and historical data), and 24/7 access to DDoS experts for complex cases, available on: 
1. Amazon Route 53, Amazon CloudFront
2. Elastic Load Balancing
3. AWS Global Accelerator
4. Elastic IP (Amazon EC2 and NLB)

# **Penetration testing**
- Can perform PenTesting on AWS
- permitted services:
1. EC2 instances, NAT gateways and ELB
2. RDS
3. CloudFront
4. Aurora
5. API Gateways
6. AWS Lambda and Lambda@Edge functions
7. Lightsail resources
8. Elastic Beanstalk environments
- Prohibited activities:
1. DNS zone walking via Amazon Route 53 Hosted Zones
2. DoS & DDoS
3. Port flooding
4. protocol flooding
5. request flooding (login request flooding & API request flooding)
- for other simulated events, need to submit a request to AWS, could take up to 7 days

# **Amazon Guard Duty**
- IDS/ IPS (intrusion detection system and intrusion protection system) => devide or software that monitors a network or systems for malicious activity or policy violations
- **Guard Duty** is a threat detection service that monitos for malicious and suspicious activity or unauthorized behaviour
- uses machine learning to analyze the following AWS logs:
1. CloudTrail Logs
2. VPC Flow Logs
3. DNS Logs
- will alert us of findings which we can automate a incident response via CloudWatch Events or 3rd party services

# **Key Management Services (KMS)**
- service that makes it easy for us to create and control the encryption keys used to encrypt the data
- KMS is a multi-tenant HSM (hardware security module), multiple users are sharing the same hardware, with each virtually isolated from each other
- HSM is a hardware specifically for storing keys within memory, never write them to disk
- many AWS services are integrated to use KMS to encrypt data with a simple checkbox
- KMS uses Envelope Encryption => 3 layers of security (Master key protects -> Data key protects -> Data)

# **Amazon Macie**
- Macie is a service that monitors **S3 data access** activity for anomalies, and generate detailed alerts when it detectss risk of unauthorized access or data leaks
- works by using machin learning to analyze the **CloudTrail** logs
- will identify the most at-risk users which could lead to a compromise
- Macie has a variety of alerts:
1. Anonymized Access
2. Location Anomaly
3. Config Compliace
4. Credentials Loss
5. Open Permissions
6. Privilege Escalation
7. Ransomware
8. Service Disruption
9. Suspicious Access
10. Data Compliance
11. File Hosting
12. Identity Enumeration
13. Information Loss

# **Security Groups vs NACLs**
- **Security Groups**: 
1. acts as fireweall at **instances** level
2. implicitly denies all traffic
3. user creates ALLOW rule
4. eg: Allow an EC2 instances access on port 22 for SSH
- **network access control lists (NACLs)**:
1. acts as firewall as the subnet level
2. user create ALLOW and DNY rules
3. eg: vlock a specific IP address known for abuse

![alt text](https://static.javatpoint.com/tutorial/aws/images/aws-nacl-vs-security-group.png)

# **AWS Virtual Private Network (VPN)**
- allow us to establish a secure and private tunnel from our network or device to the AWS global network
- **AWS Site-to-Site VPN**: connects on-premise network or branch office site to VPC (connecting an entire office or network to AWS)
- **AWS Client VPN**: connects users to AWS or on-premise networks (connect only certain employees or devices to AWS)

# **AWS Cloud Services**
- **CloudFormation**: infrastructure as code, set up services via templating script
- **CloudTrail**: logs all APi calls between AWS services
- **CloudFront**: CDN, create cached copy of our app and copies to server located near end-users who tries to visit our app
- **CloudWatch**: 