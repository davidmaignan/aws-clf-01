# AWS Certified Cloud Practioner - CLF-C01

Youtube: https://www.youtube.com/watch?v=SOTamWNgDKc
Cheat sheets, practice exams, flash cards: https://www.exampro.co/clf-c01

## Benefits

- Agility
- Pay as you go
- Economy of scale
- Global Reach
- Security
- Reliability (Cloud architecture)
- High Availabitliy (Cloud architecture)
- Scalability (Cloud architecture)
- Elasticity (Cloud architecture)
- Fault Tolerence
- Disaster Recovery

## Six Advantages to Cloud

1. Trade capital expense for variable expense (pay on demand)
2. Benefit from massive economies of scale (sharing cost with other customers)
3. Stop guessing capacity (scale up / down)
4. Increase speed / agility: Launch ressources within few clicks
5. Stop spending money on running/maintaining data centers (focus on customers)
6. Go global in minutes (Deploy app in multiple regions in few clicks)

[Six advantages to cloud](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html)



| Key | Description |
| -- | -- |
| Cost-effective | pay for what you consume, no up-front cost |
| Global | anywhere in the world |
| Secure | cloud provider takes care of physical security. Services can be secure by default, configurable to a granular level |
| Reliable | Data backup, disaster recovery, data replication, fault tolerance |
| Scalable | in/de-crease resources and servcies on demand |
| Elastic | Automate scaling during spikes/drop in demand |
| Current | hardware is mananged, patched, upgraded and replaced by the cloud provider without interuption | 

## Overview

| Key | Description | 
| -- | -- |
| Regions | 25 |
| Availability zones | 81 |
| Direct connection locations | 108 |
| Points of presence | 275+ |
| Local zone | 11 |
| Wavelength zones | 17 | 


[AWS global infrastucture](https://aws.amazon.com/about-aws/global-infrastructure/)

- Each region has three Availabitily zones
- New services always available first in US-EAST
- Not all services are available in all regions
- Billing information appears in US-EAST-1
- Cost vary per region

#### Choose a region
1. Regulatory compliance
2. Cost of AWS in this region
3. What AWS services are available in this region
4. What is the distance with my end users

#### Regional vs Global services

AWS scopes their AWS management console on a selected retion

> Global services: S3, CloudFront, Route53, IAM

#### Availability Zones (AZ)
Physical location made up of one or more datacenter
Generaly contains 3 availability zones
Datacenters within a region are isolated from each other but close enough to provide low latency
Common practice to run workloads in at least 3 AZs to ensure services remain available in case one or two datacenters fail.

> us-east-1a, us-east-1b, ... (letter represent AZ)

You never choose the AZ when launching resources. You can choose the Subnet which is associater to the AZ
Availability zone can have multiple physical locations
All traffic between AZs is encrypter. AZs are within 100km of each other

#### Fault Tolerance - Fault domain

A fault domain is a section of a network that is vulnerable to damage if a critical device or system fails. The purpose of a fault domain is that if a failure occurs. It will **not cascade outside that domain**, limiting the possible damage

- specific servers in a rack
- an entire rack in a datacenter
- an entire room in a datacenter
- the entire data center building

> An AWS region would be a Fault level (us-east-1) - A AZ would be a  Fault domain (us-east-1a | us-east-1b)

- Each AWS region is completely isolated from the other regions
- Each AZ is isolated but AZ in a region are connected through low-latency links
- Each AZ is designed as an independent failure zone

##### Failure zone
- Available zones are physically separated within a metropolitan region, lower risk flood plains
- discrete uninterruptilble power supply, backup generation facilities
- data centers in different AZ supplied by independant substations / reduce power grid collapse

Multiple AZ for High Availability: protection against: power outage, lighting strikes, tornadoes, earthquakes, ...

#### Global Network

Interconnections between AWS global infrastructure. Backbone of infrastructure. Private expressway between datacenters
Aws Global accelerator, AWS S3 Transfer acceleration: uses edge locations as an on-ramp to quickly reach ASW resources in other regions by traversing the fast AWS Global Network
Amazone CloudFront (CDN): uses edge locations as an off-ramp to provide at the Edge storage and compute near the end user
VPC endpoints: ensuring resources stay within AWS network and do not travers over public internet

#### POP (point of presence)
Intermediate location between an AWS region and the end user, and this location could be a datacenter or collection of hardware

It can be own by AWS or Trusted Partner.
- Edge locations
- Regional edge caches 
- Regional Edge locations


#### AWS services using POP/Edge location
- Amazon CloudFront: is a Content Delivery network (CDN). You point your website to CloudFront so that it will route request to nearest EdgeLocation cache. Allow you to choose an origin (webserver, storage) that will be source of cached. 

- Amazon S# Transfert acceleration: allows you to generate a special URL that can be used by end users to upload files to a nearby Edge Location. Once a file is uploaded to an Edge Location, it can move much faster withinn the ASW Network to reach S3

- AWS Global Accelerator: can fin the optimal pah from the end user to your web-servers. GA are deployed within Edge locations so you send user traffic to and Edge Location instead of directly to your web-application


#### AWS Direct Connect
It's a private/dedicated connection between your datacenter, office, co-location and AWS
1. Lower bandwith: 50-500 mbps
2. Hight bandwith: 1-10 gbps

- help reduce network cost
- increase bandwith throughput / great for high traffic network
- more consistent network experience
- reliable / secure

#### Direct Connect Locations

Trusted partnered datacenters that you can etablish a dedicated high speed, low latency connection from your on-premise to AWS (eg: Allied Data Centers - 250 front street west - Toronto)

#### Local Zones
Datacenters located very close to a densely populated area to provide single-digit millisecond low latency performances (eg: 7ms) for that area. Only for specific services (EC2 instances T3, C5, R5,...), EBS, FSx, Load Balancer, VPC
eg: **us-west-2-lax-1a**

#### Wavelength Zones
Allows for edge-computing on 5G networks. Application will have ultra-low latency being as colse as possible to the users.
You create a subnet tied to a WaveLength zone and then you can launch Virtual Machines to the edge of the targeted 5G network

#### Data Residency
Physical or geographic location of where an organization or cloud resources reside.

- Compliance boundaries: legal requiremnet where data/cloud resources are allowed to reside
- Data Sovereignty: jurisdictional control or legal authority that can be asserted over data because it's physical location is whithin jurisdictional boundaries

- AWS Outposts: physical rack of servers in your data center
- AWS Config: a policy as Code servcie. Create rule to continuous check AWS resources configuration with alert if deviate.
- IAM Policies: denay access to specific region. Service Control Policy permissions applied to an organization

#### AWS for Government
- military
- law enforcement
- infrastructure
- public transit
- public education
- health care
- government itself

**FedRamp**: Federal risk and authorization Management Program. Provied an isolated region to run FedRAMP workloads. Host sensitive Controlled Unclassified Information and other types of regulated workloads
- Only operated by employees who are US citizens
- Only accessible to US entities and root account holders who pass a screening process

> FedRamp, DOJ/CJIS, ITAR, EAR, DoD, ...

#### AWS in China
Completely isolate intentionnaly from AWS Global to meet regulatory compliance for Mainland China. Need an ICP licence

#### Sustainability
> Climate Pledge: https://sustainability.aboutamazon.com

1. Renewable energy
2. Buy REC's GO's
3. Cloud efficiency
4. Water stewardship (cooling with recycle waterd)


#### AWS Ground station
Control satellite communications, process data, scale operations. Ground station to contact, select start and end time with a satellite
- weather forecasting
- surface imaging
- communications
- video broadcasts


#### AWS Outposts
Run aws services on premises. Aws delivers full rack of servers provided by AWS.

#### Terminologies
- Solution architect: role in technicla organization, that architects a technical solution using multiples systems via researching documentation, experimentation
- Cloud architect: a solution architect that is focused solely on architecting solutions using cloud services

##### High availability
Service remain available by ensuring there is no single point of failure and/or ensure a certain level of performance.
Workload accross multiple Available Zones ensures that if AZs become unvailable, service remains available. 
Elastic Load Balancer: distribute traffic to multiple servers. If some becomes unvailable ELB reroute traffic to only available one

#### High Scalability
Ability to increase your capacity based on the increasing demand of traffic, memory, computing power
- vertical scalin: bigger server
- horizontal scaling: more servers

#### High Elasticity
**Automatically** increase/decrease capacity
- scaling out: add more servers
- scaling in: removing underutilized servers

#### Highly fault tolerant
No single point of failure. Shift traffic to a redundant system in case primary system fails. 
- RDS multi-AZ: duplicate standby database in another Availaility Zone

#### High Durability
Recover from a disaster (Disaster Recovery). 
- CloudEndure Disaster Recovery: continously repliccates your machines into a low-cost stating area in your AWS account/prefered region enabling gase and reliable recovery in case of IT data center failures.

##### Business Continuity Plan (BCP)
Document how a business will continue to operate during an unplanned disruption in services

- Recovery Point objective: Maximum acceptable amount of data loss after an unplanned incident
- Recovery Time Objective: Maximum amount of downtime your business can tolerate without incurring a significat financial loss

##### Disaster Recovery Options

Low ------------------------------------------------------------------------- High

Backup/restore   -   pilot light        -        warm standby      -       Multisite/active

- Backup: restore to a new infrastructure (Hours) - Lower priority. Restore data after event. Cost 1
- Pilot light: data is replicated to another region with minimal services (10 minutes). Less stringent RTO & RPO. Core services. Cost 2
- Warm standby: scale down copy of your infra running ready to scale up (Minutes). Business critical services. Cost 3
- Multi-site: scale up copy of your infra in another region (real-time). Mission critical services. Cost 4


#### RTO
Recovery Time objective is the maximum acceptable delay between the interruption of service and restoration of services. This objective determines what is considered an acceptable time window when service is unavailable and is defined by the organisation.

[Establishing RPO and RTO Targets for Cloud Applications](https://aws.amazon.com/blogs/mt/establishing-rpo-and-rto-targets-for-cloud-applications/)

#### RPO
Recovery point objective is the maximum acceptable amount of time since the last data recovery point. This objective determines what is considered an acceptable loss of data between the last recovery point and the interuption of service and is defined by the organisation.


## Amazon Bracket


## AWS API / Management Console


## ARNs

Amazon resource names uniquely identity AWS ressources

```
arn:partition:service:region:account-id:resource-id
arn:partition:service:region:account-id:resource-type/resource-id
arn:partition:service:region:account-id:resource-type:resource-id
```
- partition: asw - aws regions
- service: ec2, s3
- region: us-east-1
- accountId: 123456




## AWS Cloudshell
it's a browser based shell built into the aws management console


## Infrastructure as code (IaC)

script to automate create, update, destroy cloud infrastructure

- iac is a blueprint of your infrastructure
- iac allows you to easily share, version or inventory your cloud infra

- AWS cloudformation (CFN): 
    - declarative,
    - explicit, 
    - verbose, 
    - zero chance of misconfiguration
    - json/yaml/xml

- AWS Cloud Development Kit (CDK)
    - imperative
    - implicit
    - less verbose
    - programmable

## CloudFormation
allows you to write infrastructure as code in json/yaml. It's is simple but lead to larger files, limited in some regards to creating dynamic or repeatable infrastructure compared to CDK



# KodeKloud

### Economics of CC

1. Free Tier
Free services means that certain services are always free, and some are free for 12 months after new account creation

2. On-Demand
On demand is full pricing and pay as you go, but no contract and flexible

3. Reservations
Contracts that you enter with Amazon for 1|3 year contract

4. Volume discount
S3 - the more you use the lower it costs per unit

5. Price Drops
129 price drops since 2006


### Cloud design principles

More at [AWS Architecture Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html)

Book: Code Complete - Steve MacConnell

1. Design for failure
2. Decouple components
3. Implement elasticity (scale out|in base on demands)
4. Think parallel

### Shared responsability model

## Security

1. Preventative services

#### AWS web application Firewall
Protection for any http based application, listen to incoming http request, monitor attack vector 
- Define set of rules WEB ACL:
- ressource to monitor
- define inspection critaria: IP, country of origin, regex match of request, malicious code (SQL injection, XSS) malicious code)
- action: Allow, Block, Count, CAPTCHA

#### AWS Shield
Protection against DDOS attack (flooding a server with huge amount of requests)

#### Network firewalls
Monitor traffic entering / leaving a VPC.

2. Detective services

#### Amazon inspector: 
Scans workloads running on AWS for vulnerabitilies and undesired network exposure. Automatically discover EC2 instances, containers images in ECR, lambda functions. When vulnerabilites are found, it generates a report with the findings. Re-runs scans whenever changes that could introduce new vulnerabilites (install new package, patch, new cve published)

#### Amazon GuardDuty
Enable with few clicks in AWS management console. Continuously monitor: abnormal api activity, Attempts to disable AWS CloudFront logging, Potential unauthorized deployment, compromised instances. S3 Bucket compromise. Detect threats with machine learning and abnormal detection to identify potential threats. Review findings into event management or trigger AWS lambda function for automated remediation.

#### Amazon Detective
Ingest data from VCP flow logs, CloudTrail logs, GuardDuty findings. Create visualization to show resource behaviors and interactions over time

#### AWS config
Track and audits the configuration of AWS resources over time. Eg: Attached new security group to ecs. Attached EBS volume. Modify Http rules for WAF: all get logs in AWS config

#### Security Hub
Centralized AWS inspector & Guard Duty in central location. Automate security checks perform validation against AWS security best practices.

#### CloudTrail
Track user activity within an AWS account. Anytime a user performs an actcion within AWS, an event is logged in CloudTrail (eg: modifying security policies, access/create/delete a service, modify a config, ...)

#### Security Lake
Log aggregator with storage and query parquet format - ocsf open cybersecurity schema framework. 

#### AWS Macie
Service uses pattern matching and machine learning to automatically discover sensitive data and generate an inventory report of S3 buckets and scan objects for sensitive data. Notify you for all findings

3. Management services

#### Firewall Manager

Centralized and share policies of AWS shield, WAS, AWS network Firewall between multiple accounts (dev, qa, prod)

#### Resource Access Manager
Share resources like private subnet between multiple accounts

#### AWS Cognito
Customer identity and access management for mobile and web applications. Signup, login without social authentications to any app. Manage all user credentials.

#### IAM
Manage acess resources for user group and roles though policies.

#### IAM identity center
Manage users throught multiple accounts. Grant access for different accounts

#### Secrets Manager
Store secrets, credentials for applications. Automatic rotation for secrets

#### AWS Certificate Manager (ACM)
Provisions, manages, and deploys SSL/TLS certificates for AWS resources

#### AWS Private Certficate Authority
Create a private CA to manage private certificates within an organization. Encrypt traffic with private certificate for internal use.

#### Key Management Service (KMS)
Create and manage (allow/deny access) encryptions keys to encrypt data with key for sensitive data 

#### Cloud Hardware Security Module (HSM)
HSM place to securily store cryptographic keys - Data is sent to HSM to Encryption/Decryption. Provides customer with hardware security modules in the cloud

