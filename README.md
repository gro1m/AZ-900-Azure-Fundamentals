# AZ-900-Azure-Fundamentals
Exam page: https://www.microsoft.com/en-us/learning/exam-az-900.aspx
* 1 Understand cloud concepts (15-20%)
* 2 Understand core Azure services (30-35%)
* 3 Understand security, privacy, compliance and trust
* 4 Understand Azure pricing and support

## 1 Understand cloud concepts 
renting ressources.
ressources are:
* compute power
* storage 
* secure network connections
* analytics

cloud providers:
* Microsoft
* Amazon
* Google

Main terms:
* availability (Azure Load Balancer, Traffic Manager)
* fault tolerance
* scalability -> 1 VM to 100 VMs in some seconds (Virtual Machine scale sets)
* elasticity -> amount of VMs by demand
* global reach -> services near to place of use
* predictive cost considerations
* disaster recovery
* security
* economies of scale -> smaller costs, as provider can scale better and stronger (data centers)

capital expenditure (capex):
* build infrastructure at beginning (lot of upfront cost), then reduce costs.

operational expenditure (opex):
* consumption-based model: only pay for effectively needed services; you need to pay immediately!
* example: Black Friday

### different cloud models
public cloud:
* example: Microsoft Azure
* physical infrastructure managed by cloud provider, e.g. Microsoft.
* secure network-connection
* no capex
* pay-what-you-use
* fast

private cloud:
* physical infrastracture is managed by your company.
* motivation: own infrastructure and data.
* own datacenter
* own ressource

hybrid cloud:
* connect cloud solution with on-premise infrastructure.
* public + private cloud
* highest flexibility

### Types of Cloud Services
* IaaS: Infrastructure as a Service
* PaaS: Platform as a Service
* SaaS: Software as a Service

#### IaaS
Example: Virtual Machine (stored on physical server hosted in a cloud provider's datacenter)
need to manage updates of the following:
* Server
* VMs
* Storage
* Operating System
* networks

#### PaaS
Example: Azure Container services, Database management system e.g. Azure SQL Database
need to manage the following:
* application
Amount of CPUs etc. does not need to be managed

#### SaaS
software ready to use hosted in the cloud.
Example: Office 365.
Need to manage:
* Data & Access
Example: Word Online , where to store data and who has access

### Core Concepts
region:
* collection of data centers
* a ressource has to mapped onto a region

NOTE: For AI Services not all regions may be available!

There are 50+ regions in 140 countries:
https://azure.microsoft.com/en-us/global-infrastructure/regions/

availability zones:
* Unique physical locations within a region. Each zone is made up of one or more datacenters equipped with independent power, cooling, and networking.

* Azure Free Account:
- 12 months of popular free services + $200 credit for 30 days + 25+services which are always free.
- https://azure.microsoft.com/en-us/free/

* Azure Portal:

region pairs:
* same services, same legal jurisdiction
* Microsoft tries to separate them at least 300 miles apart, i.e. if catastrophe hits one region, you could transfer it to the region pair

geographies:
* discrete markets
* have same data residency and same compliance boundaries

resource:
* manageable item that can be created in Azure
* e.g. WebApp, VM, SQL Database ...
* e.g. VM can be assigned to another resource, the NSG.

resource groups:
* holds related resources
* container for multiple resources that have the same lifecycle
* no hierarchical structures
* aggregates ressources in a manageable unit.

Above Management group there is the tenants directory (tenant = own company)

Azure Resource Manager:
* manages access to Azure
* Management Groups: 
  - groups of subscriptions
  - rules for multiple subscriptions (for example only Swiss datacenters allowed)
* subscription:
  - here billing information is stored
* resource groups:
  - belong to exactly one subscription
* resource:
  - has to be in a resource group

## 2 Understand core Azure services
1) Azure Compute services 
* IaaS
* disks, processors, storage, network, operating system
2) VM scale set
* automatic scaling of identical VMs (e.g. Black Friday)
3) App services
* PaaS
* Applikation (e.g. no load balancing)
4) Functions
* code in cloud that only costs when in use
* compute actions based on an event

### Availability Options for VMs
* single VM: 99.9%
* availability set: 99.95%
  * multiple copies of a VM in the same region
  * fault domain (FD): select cpu family, cluster that supports cpu family
  * update domain (UD): inside cluster single server/rack
  * e.g. 5 UD and 3 FD: VM is on 3 clusters on 5 servers
* availability zone: 99.99%
  * physically separated zones inside a region that means: separate electricity, cooling and network, e.g. network: Swisscom, Sunrise
* region pairs: multi-region disaster recovery

### Virtual Machine
- gets assigned a Network interface (separate resource)
- network interface gets assigned a private IP address
- can have multiple disks for storage (this are VHD files)
- by default gets OS disk, but you can also assign data disks
- can control traffic flow by Network Security Groups.
- in summary creates in the same resource group:
  - Virtual Network
  - Virtual Machine
  - Disk
  - Network interface
  - Public IP address
  - Network security group

### Container services
a container is a minimal version of a VM, a VM image is typically quite big.
Azure Container services -> PaaS offering to upload.
Azure Kubernetes services -> administer big amount of containers (orchestrator)

### Azure network services ("Router to which you attach VMs")
* Azure Virtual Network
  - allows yout define your own network in Azure
  - can consist of multiple subnets
  - needs to be assigned an address space, e.g. 10.0.0.0/16.
  - subnet address space has to be subset of address space of Virtual Network, e.g. 10.0.1.0/24 and 10.0.2.0/24. VMs created in Subnet.
  - each machine in the subnet will get a private IP address, e.g. 10.0.1.4 and 10.0.2.4
  - a public address (allows to connect to Internet) can also be assigned to VM e.g. 40.11.112.4 and e.g. 50.1.200.4
  - Virtual Network Peering between networks so that VMs can communicate across VNets.
* Azure Load Balancer
* VPN Gateway
* Azure Application Gateway - on DNS level
* Content Delivery Network 
  * goes through Azure Backbone (WAN-Link via undersea network cables that belong to Microsoft)
  * Example: Web application from Europe puts in onto a US edge device (marked as small rectangles). After 30 or 90 days fetch from original place. white routes means there is an availability zone (threee separate zones with independent electricity, cooling and network infrastructure)
* Brazil is not a paired region, i.e. is not used as backup.

### Virtual Machine Scale Sets
* allows you to scale your infrastracture based on demand
* infrastracture can scale out when demand increased
* infrastructure can scale in when demand decreases.
* Scale Sets can also be applied to Azure Web Apps.
* scales number of virtual machines based on threshold
* adds element of high availability to your infrastructure.
* machines in scale set can be behind Load Balancer or an Application Gateway.
* Linux tool for stress tests on https://www.tecmint.com/linux-cpu-load-stress-test-with-stress-ng-tool/
: 
```bash
sudo apt get install stress
sudo stress --cpu 100
```

### Azure Load Balancer
* works at Network Layer (Layer 4)
* provides high availability for your applications
* fully-managed service in Azure
* allows you to distribute traffic to your backend Virtual machines.
* ensures equal distribution of requests to VMs.
* internal load balancer - only balance traffic from within VNet.
* public load balancer - balance internet traffic to VMs.
* 2 pricing tiers: Basic (only one VM, availability set or scale set) and Standard (as many VMs as you want)
* User-Web Server: public load balancer + Web Server-Database Server: internal load balancer.
* backend pool are the Virtual machines
* health probe: use to check whether backend VM is healthy or not.
  configuration parameters:
  * protocol on which to check, e.g. TCP
  * Port Number
* load balancing rules:
  * how to route traffic
  * redirect traffic to backend pool
  * you enable Session Persistence - client IPs can be directed to the same backend VMs.
  * interval for the health probe
  
### Azure Application Gateway
* load balancer works at Layer 7 - Application Layer
* fully-managed service
* you can also add Web Application Firewall to protect web applications against SQL injections, cross-scriptiong attacks etc.
* example: url-based routing (i.e. request to subpages of website are sent onto different VMs)


### Azure storage services
IaaS:
* VM -> disk is created and stored in storage account
* network storage -> file share
* disks / files
PaaS:
* Containers: 
  * Block Blobs (small images) 
  * Page Blobs (data is loaded step-by-step)
  * append blobs (e.g. log files)
* Tables:
  * key-value lookup (NoSQL solutions, scale in the peta-domain of data)
* Queues (Message Queues), e.g. jobs might use a VM sequentially so that there is not a problem with dealing a huge amount of requests.

* Blob Storage
  - object storage
  - store unstructured data e.g. files, videos, images, log files
  - need to create a Storage Account and inside Containers you store objects
  - hot storage tier - data accessed frequently
  - cool tier: infrequently accessed data
  - archive tier: rarely accessed data (can only be set at object level, not at Container level) - objects cannot be accessed in this tier.
* File Storage
  - allows file retrieval via the Server Message Block protocol
  - can mount file shares on Windows, Linux and Mac based machines
  - do not need file servers.
* Table Storage
  - used for storing structured NoSQL data
  - key attribute store
  - cost-effective option for storage of table like user data for applications.
* Queue storage
  - used for storage and retrieval of message
  - when you want to decouple components of an application
  - a single message in the queue can be up to 64KB in size
  - can store millions of messages in the queue.

* Account kind (version)
  - v2 -> access tier option
  - v1 -> does not have all options
  - Blob Storage -> only blob storage
  
* Change access level:
  - Blob (anonymous read access for blob only) enables to get it via URL

Performance: no standard disks
Account kind: Storage Version 2 , Version 1 only Containers available

Replication: 
e.g. West Europe.
* locally-redundant storage: -> 3 copies
* zone-redundant storage: separate electricity, cooling and network
* geo-redundant storage: six copies in West-Europe and North-Europe (region pairs)
* read-access geo-redundant storage: second endpoint has read access

Access tier:
* hot: for a lot of data accesses: storage expensive, access cheap
* cool: for small data access: storage cheap, access expensive
* archive: storage very cheap, access very expensive (stored on magnetic tape)

### Azure database services
#### Data structure
structured data -> SQL-databases (tables), relational databases
semi-structured data -> NoSQL-databases (JSON, BLOBs, books, blogs, HTML)
unstructured data

#### Azure Cosmos DB
* multi-model database:
  - you can create CosmosDB account and has support for different APIs (Table, SQL, MongoDB, Cassandra, Gremlin, etc.)
* low-latency access
* instant replication of data across regions
* scales automatically based on demand
* fully managed and serverless service
* 99.999% availability for reads and write
* ability to scal from thousands to hundreds of millions or requests/sec
* guarantess less than 10 ms latencies for reads and writes at 99% percentile.

#### Azure SQL Database
* PaaS from Microsoft SQL Server
* 99.99% of availability.

#### Azure SQL Data Warehouse
* Enterprise Data Warehouse on Azure.
* Used to store petabytes of data.
* perfect data store when you want end-to-end big data solution on Azure
* data is stored in relational tables using columnar storage 
  * reduces storage costs
  * improves query performance
* you can perform query analysis over large data sets
* not for transactional data (use SQL Database).

#### Azure Content Delivery Network (CDN)
* effective delivery of web content to users
* users around the world get a seemless experience in terms of latency, response.
* popular content can be cached.
* edge servers (point of presence): deliver content
  * contacts origin to get resource if it does not have it and then caches it based on TTL (Time to live).
* you need to create a CDN profile and then a CDN endpoint.
* you can attach multiple endpoints to a CDN profile.


#### Azure DataBase Migration

### Azure Marketplace
  * Microsoft products

### Azure solutions
#### Internet of Things (IoT)
* data collecting devices send their data to Azure IoT Hub
* Azure IoT Hub manages the data of the IoT devices
* Azure IoT Central is a SaaS solution for IoT devices that is based on Azure IoT Hub techniques
* IoT Hub name has to be globally unique
#### Big data and analytics
Azure Synaptic Analytics:
  * Data Warehousing and Big Data (Analysis)
Azure HD Insight:
  * cost-efficient, simplified processing of data
Azure Data Lake Analytics:
  * simplification of data in the data lake
#### Artificial Intelligence
Azure Machine Learning Service:
* cloud-based environment tool
Azure Machine Learning Studio:
* SaaS offering from Azure Machine Learning Service
Cognitive Services:
* LUIS (language understanding intelligent service)
#### Serverless computing
* only pay at runtime
* Azure Functions: 
  * pay per executing Code Snippets
  * select a trigger
* Azure Log Functions
  * automatically orcherstrated tasks
* Azure Event Grid
#### DevOps
* Azure DevOps:
  * pipelines, Git repositories, Kanban boards, extensive automated cloud-based load-testing
* Azure DevTest Labs:
  * test environment => cost of an environment
#### Azure App Service 
* PaaS (create WebApp)
* multiple languages, frameworks
* DevOps optimization
* global scalability with high availability
* security
* VisualStudio Integration
etc.
#### Azure management tools
* az cli
#### Azure Advisor
* Security
  
### Azure VPN Gateway
* used to connect your on-premise network to an Azure network in an encrypted manner.
* Point to Site Connection:
  - connect workstations to an Azure Virtual Network
  - you need to install a VPN client
  - you need to make use of certificates for authenticating clients
  - typically for limited number of clients
* Site to Site Connection
  - used to connect on-premise networks to Azure networks.
  - traffic encrypted using IPSec protocol
  - on-premise network needs a VPN device with an IP address that is routable over the Internet.
  
### Azure Web App
- PaaS for hosting web apps using Azure App Service.
- not responsible for machine setup, web server setup, security updates
- underlying servers can be Windows or Linux.

### Azure Functions
- serverless compute service
- only pay what you use
- use C#, F#, Node.js, Java or PHP
- integrates with other Azure services
- code upload to Azure Functions
- can have input and output bindings:
  - input binding: whenever an object is add to BLOB storage, invoke the function
  - output binding: function can add data to Azure table storage
- costing: consumption plan or App Service Plan
- consumption plan: 
  - charged for the number of execution, execution time, memory used.
  - maximum allowable execution time is 5 minutes
- App Service Plan
  - have instances allocated
  - have the function running longer time
  - more memory

### Azure Logic Apps
* helps to automate and orchestrate tasks
* helps to build workflows (with various templates) - do not need to worry about the infrastructure
* fully managed and serverless service
* workflow can be integrated with Azure services and 3rd party apps
  * connectors to e.g. BLOB storage, Azure Functions, Azure Service Bus
* workflows can be built via Visual Designer
* Some connectors like Blob storage can trigger Azure Logic Apps.
* Action: what to do when an event is triggered -> email to IT Administrator, Azure Function

### Azure Management Tools
* Azure Portal
* PowerShell 
  * can run on Windows, Mac OS, Linux
* Azure Command Line Interface

## 3 Understand Security, Privacy, Compliance and Trust
* physical security
  * datacenter (hardware) <- prevent that someone can enter with a USB stick
* identity and access
  * identification, authentication and authorization
* perimeter layer
  * firewall
* network
  * traffic
* compute
  * VM protection
* application
  * prevent SQL injection etc.
* data
### Perimeter Layer
#### Azure Firewall
* FaaS: Firewall as a SErvice - inbound/outbound protection
#### Azure DDoS
* Distributed Denial of Service - bombardment of the service with requests
### Network Layer
* Network Security Group (NSGs) 
  * "internetcable with some features"
  * consists of rules for inbound and outbound traffic
  * used to control traffic into your subnet or Virtual Machine
  * traffic within a Virtual Network is automatically allowed
  * you need to explicitly allow traffic from the Internet
  * VMs inside same virtual net can connect via the private IP address
  * can be applied to Network Interface Card or the subnet itself
  * rule can be either an IP address, a CIDR block, service tag or application security group
  * you define port numbers for the rule
  * you define the protocol
  * you decide whether to allow or deny the action

### Core Azure identity services
#### Azure Active Directory (AD)
* authentication: identifies person
* authorization: determines access levels
1. SSO: Single-Sign-On (device is deposited)
2. application management: give access to applications
3. authentication
4. B2B
5. B2C
6. device management

* Azure Multi-Factor Authentication:
3 factors: 
  * something you know (password)
  * something you possess (key, mobile authenticator app)
  * something you are (fingerprint)
 
#### Security Tools and features
* Azure Security Center
* Azure Key Vault
  * password and certificates securely stored
  * backed by hardware security modules (MSMs)
  * cannot be moved
* AIP: Azure Information Protection
* ATP: Azure Advanced Threat

#### Governance
* Azure Policy -> SLAs:
  * policy initiations -> definitions
  * can be assignedon level *Management Group*, *Subscription*, *Ressource*
* Role-based access control (RBAC):
  * on resource group
  * deny assignments always stronger than role assignments
* Resource locks
  * protect your Azure resources from accidental deletion or modification
* Azure Blueprints
  * via subscription
  * audits, deployments etc
  * subscription governance: billing, access control, limits -> can be hard
* Tags
  * Metadata for Azure ressources (name-value pair)
* Azure Monitor
  * metrics
  * activity log
* Azure Service Health
  * status, e.g. stopped (deallocated -> no ressources -> no costs), running (ip-address -> available)
* Privacy statement
  * defines how data is protected
* Trust Center
* Service Trust Portal (STP)
* Compliance Manager
  * compares ressources against own policies
* Azure Government services meets needs from US agencies
* Azure Government physically isolated from non-governmental US deployments
* Azure China 21Vianet: physically separated instance and managed by 21Vianet

## 4 Pricing/Support Plan
subscription offers:
 * free
 * pay-as-you-go
 * enterprise agreement
 * student/teacher
 * account can have more than one subscription
Azure free account:
 * 12 months + 200$ credit for first 30 days 
web-direct
cloud solution providers
ressource type: resource-specific costs
services: depends on subscription
location: most expensive -> Brazil, cheapest -> West US 1,2
bandwidth: data transfer

pricing calculator
total cost of ownership calculator

azure reservations: reserve ressources in advance -> pay less
tags: lets you mark cost owner

Azure Cost Management:
  * reporting
  * data environment
  * Budgets
  * Alerting
  * Recommendations
  
Cost Management and Billing:
  * Cost analysis by location, tag, resource group
  
Support plan
  * Basic (always, default)
  * Developer (24-hr-answer from support)
  * Standard (instant answer)
  * Professional Direct
  * Premier: support engineers + technical account manager + implementation support
  
Support channels:
  * MSDN: Microsoft Developer Network
  * Stack Overflow
  * Server Fault
  * Microsoft Azure General Feedback
  * @AzureSupport
  * Knowledge Center
  
  
SLA          | Downtime (Month) | Downtime (Year)
------------ | -------------    | ---------------
99.9%        | 43.2 mins        |  8.76 h
99.95%       | 21.6 mins        |  4.38 h
99.99%       |  4.32 mins       | 52.56 mins

composite SLA is obtained by multiplying individual SLAs.

private preview: 
  * Azure feature available to certain Azure customers for evaluation purposes

public preview:

preview.portal.azure.com


## 5 Lessons learned and References from practice tests
- PowerShell and Azure CLI support is not for Android OS
- PowerShell can be run on Linux only when PowerShell Core and Azure CLI is installed.
- PowerShell can be installed on MacOS: https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6
- If you are looking at storing data that is not frequently used use Azure Data Lake. Also needed for PowerBI.
Azure SQL, Azure PostgreSQL or Cosmos DB for frequently accessed data.

* https://docs.microsoft.com/en-us/azure/active-directory/develop/authentication-vs-authorization
- Authentication is the process of proving you are who you say you are. Authentication is sometimes shortened to AuthN. Microsoft identity platform implements the OpenID Connect protocol for handling authentication.

- Authorization is the act of granting an authenticated party permission to do something. It specifies what data you're allowed to access and what you can do with that data. Authorization is sometimes shortened to AuthZ. Microsoft identity platform implements the OAuth 2.0 protocol for handling authorization.

- Virtual Machine Scale Sets: https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/overview

- Azure Privileged Identity Management: https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/overview

- Azure Application Insights: https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6

- https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/overview: You can have resources (e.g. storage) in same resource groups, but different locations.

- https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources: (resource group) tags are not inherited.

- permissions are inherited

- https://docs.microsoft.com/en-us/azure/advisor/advisor-security-recommendations: Azure Security gives security recommendations, not Azure Advisor

- https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/overview: Azure Resource Manager ideal solution if you have to deploy the same type of resource repeatedly.

- https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-mfasettings: configure MFA

- https://docs.microsoft.com/en-us/azure/active-directory/identity-protection/overview-identity-protection

- https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/lock-resources: Azure Locks are used to prevent accidental modification or deletion of resources.

- https://docs.microsoft.com/en-us/azure/governance/policy/overview: Azure Policy

- https://docs.microsoft.com/en-us/azure/key-vault/general/basic-concepts: Azure Key Vault used for security purposes such as key and secret management.

- support plans: https://azure.microsoft.com/en-us/support/plans/

- Azure Pricing FAQ: https://azure.microsoft.com/en-us/pricing/faq/

- Azure Cost Management + Billing: https://azure.microsoft.com/en-us/pricing/details/cost-management/

- Cloudyn service: https://docs.microsoft.com/en-us/azure/cost-management-billing/cloudyn/overview

- Pricing calculator: https://azure.microsoft.com/en-us/pricing/calculator/

- Azure Resiliency: https://azure.microsoft.com/en-us/features/resiliency/

- https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-storage-tiers?tabs=azure-portal

- Azure Service Bus: https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview

- Azure Reservations: https://docs.microsoft.com/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations

- https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits

- Azure Policy: https://docs.microsoft.com/en-us/azure/governance/policy/overview

- Azure Role-Based Access Control: https://docs.microsoft.com/en-us/azure/role-based-access-control/overview

- https://docs.microsoft.com/en-us/azure/governance/management-groups/

- Azure Functions: https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview

- Azure Logic Apps: https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-overview
  




