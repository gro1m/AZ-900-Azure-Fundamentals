# AZ-900-Azure-Fundamentals

## Motivation for Cloud
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
* availability
* fault tolerance
* scalability -> 1 VM to 100 VMs in some seconds
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

public cloud:
* secure network-connection
* no capex
* pay-what-you-use
* fast

private cloud:
* own datacenter
* own ressource

hybrid cloud:
* public + private cloud
* highest flexibility

## Types of Cloud Services
* IaaS: Infrastructure as a Service
* PaaS: Platform as a Service
* SaaS: Software as a Service

### IaaS
need to manage updates of the following:
* Server
* VMs
* Storage
* Operating System
* networks
Example: Virtual Machine.

### PaaS
need to manage the following:
* application
Amount of CPUs etc. does not need to be managed
Example: Azure Container services

### SaaS
software ready to use hosted in the cloud.
Example: Office 365.
Need to manage:
* Data & Access
Example: Word Online , where to store data and who has access

## Core Concepts
region:
* collection of data centers
* a ressource has to mapped onto a region

NOTE: For AI Services not all regions may be available!

There are 50+ regions in 140 countries.

region pairs:
* same services, same legal jurisdiction
* Microsoft tries to separate them at least 300 miles apart, i.e. if catastrophe hits one region, you could transfer it to the region pair

geographies:
* discrete markets
* have same data residency and same compliance boundaries

resource groups:
* container for multiple ressources that have the same lifecycle
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

## Core Azure service and products
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

## Availability Options for VMs
* single VM: 99.9%
* availability set: 99.95%
  * multiple copies of a VM in the same region
  * fault domain (FD): select cpu family, cluster that supports cpu family
  * update domain (UD): inside cluster single server/rack
  * e.g. 5 UD and 3 FD: VM is on 3 clusters on 5 servers
* availability zone: 99.99%
  * physically separated zones inside a region that means: separate electricity, cooling and network, e.g. network: Swisscom, Sunrise
* region pairs: multi-region disaster recovery

## Container services
a container is a minimal version of a VM, a VM image is typically quite big.
Azure Container services -> PaaS offering to upload.
Azure Kubernetes services -> administer big amount of containers (orchestrator)

## Azure network services ("Router to which you attach VMs")
* Azure Virtual Network
* Azure Load Balancer
* VPN Gateway
* Azure Application Gateway - on DNS level
* Content Delivery Network 
  * goes through Azure Backbone (WAN-Link via undersea network cables that belong to Microsoft)
  * Example: Web application from Europe puts in onto a US edge device (marked as small rectangles). After 30 or 90 days fetch from original place. white routes means there is an availability zone (threee separate zones with independent electricity, cooling and network infrastructure)
* Brazil is not a paired region, i.e. is not used as backup.

structured data -> SQL-databases (tables), relational databases
semi-structured data -> NoSQL-databases (JSON, BLOBs, books, blogs, HTML)
unstructured data

## Azure storage services
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

## Azure database services
Azure Cosmos DB:
* extremely performant, extremely expensive
Azure SQL DB:
* last Version of Microsoft SQL DB.



