# Azure Portal + Misc. Notes

## Azure Portal

- Access the portal at portal.azure.com

## Azure Cloud Shell

- Allows users to choose between bash and PowerShell to manage Azure resources.
- Is temporary and requires a new or existing Azure File share to be mounted.
- Offers an integrated graphical text editor (open-source Monaco Editor).
- Automatically authenticates for easy access to Azure resources.
- Sessions time out after 20 mins of inactivity.
- Runs on a temporary host provided on a per-session, per-user basis.
- Requires a resource group, storage account, and Azure File share.
- Uses the same Azure file share for bash and PowerShell.
- Assigned to one machine per user account.
- Persists $HOME using a 5-GB image held in your file share.
- Permissions are set as a regular Linux user in Bash.

## Azure PowerShell

- Available in the cloud using Azure Cloud Shell or locally using PowerShell for Windows, Linux, or macOS.
- Can be used in two modes, either locally, or in the cloud:
    - Interactive: manually enter each command one at a time.
    - Scripting: execute a script containing multiple commands.

Note: The base PS product comes in two variants:
- Windows PowerShell
- PowerShell 7.x
  - Can be installed on Windows, macOS, and Linux.
 
Important: to install PowerShell on macOS and Linux, you will use a package manager (HomeBrew on macOS).
  - The package manager to use on Linux will depend on the distro you use.

    - Ubuntu & Debian: apt-get
    - Red Hat & CentOS: yum
    - OpenSUSE: zypper
    - Fedora: dnf



### Az Module

Allows you to work with the following Azure features:

- Containers
- DNS
- Event Hub
- ML
- Resource groups
- Storage
- VMs
- and more.

This module replaced the AzureRM module in December 2018, however, it ships with backwards compatibility with the AzureRM module. 

https://learn.microsoft.com/en-us/powershell/azure/what-is-azure-powershell?view=azps-10.0.0


## Azure CLI

- Used locally instead of in a web browser - available on Linux, macOS, and Windows through a terminal, command-line prompt, or script.
- Can be used in two modes, either locally, or in the cloud:
    - Interactive: manually enter each command one at a time.
    - Scripting: execute a script containing multiple commands.
- Commands are structured in groups and subgroups.
    - Groups represent Azure services.
    - Subgroups divide commands into logical groupings for each service.
 
To find commands needed for a specific service:

```powershell
az find blob
```

To get more details about the command needed:

```powershell
az storage blob --help
```

 To restart a VM:

```powershell
az vm restart -g MyResourceGroup -n MyVm
```

### Azure CLI Reference

https://learn.microsoft.com/en-us/cli/azure/


## Azure Zones/Regions/Geography

A region is a geographical area comprising at least one datacenter, but usually multiple. Datacenters are isolated from each other in close proximity & combined nnected via low-latency networks to enable fsster and seamless communication. 

- Regions offer compliance & resilency options. 
- Regions offer the flexibility to deploy resources to regions that are close to an organization's customers. 
- Regions ensure data residency. 
- Some services are region specific or limited to some regions upon launching. 
- Upon deploying resources in Azure, you will be asked to select a region in most cases. 
- Azure AD, Traffic Manager, and DNS don't need a region. the region will show as Global. 
- Regions are paired with another region in the same geography to create "regional pairs."

An Azure geography is an area that consists of one or more Azure regions. 

Examples include, but are not limited to:

- The US: consists of several regions; East US, Central US, West US, etc. 
- India
- The UK

# Terminology

## Azure resource terms & additional notes

Resource: a manageable item available through Azure. 
- Examples of resources include, but are not limited to:
    - VMs
    - Storage accounts
    - Databases
    - VNets
    - Web apps

Resource group: a container that holds related resources for Azure solutions. 
- All resources for the solution can be included, or only the resources you want to manage as a group. This allows you to decide how to allocate resources based on what makes sense for the organization.
    - Note: Resource groups cannot be renamed, but they can have resources from multiple regions.


Resource provider: a service that supplies resources to deploy and manage through Azure Resource Manager (ARM). 
- Each resource provider offers the ability to work with the deployed resources.
- Examples of resource providers are:
     - Microsoft.Compute, this supplies the VM resource
     - Microsoft.Storage, this supplies the storage account resources
     - Microsoft.Web, this supplies web app resources
     - Microsoft.KeyVault, this provides the ability to store keys & secrets

Template: a JSON file which defines one, or more, resources to deploy to a resource group. 
- Also defines any dependencies between deployed resources.
- Provides the benefit of deploying resources consistently and repeatedly. 

Declarative syntax: provides the ability to create what you intend, without having to write scripts to achieve it. 
- ARM templates are an example of this syntax. Within the file, you'll define the properties required for the infrastructure to be deployed in Azure.
