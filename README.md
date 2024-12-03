# Azure IaaS Infrastructure Deployment using Azure CLI

## Tools Used 
- Azure CLI: Command-line tool to manage Azure resources.
- Azure Virtual Machines: Created a Windows Server 2019 Datacenter VM.
- Azure Virtual Network (VNet): Set up for secure networking.
- Azure Network Security Groups (NSGs): Configured to manage inbound traffic.
- Azure Public IP: Used for external connectivity.
- Azure Storage Account: Set up for data storage.
- Azure App Service Plan: Created for potential web hosting.
- Azure SQL Database: Provisioned with a dedicated SQL server.


[![My Skills](https://skillicons.dev/icons?i=azure,vscode&perline=2)](https://skillicons.dev)


## Description 
In this project, I used Azure CLI to provision and configure a cloud infrastructure. The goal was to demonstrate my ability to manage Azure resources programmatically and 
create a robust environment for hosting applications or services.

### Key Components Deployed:

- **Resource Group**: Centralized resource management within a specific region.
- **Networking**:
- Virtual Network (VNet) with a subnet.
- Network Security Group (NSG) with rules to allow HTTP traffic.
- Public IP for VM access.
- **Compute**: A Windows Server 2019 Datacenter VM for application hosting.
- **Storage**: A storage account for managing data or application files.
- **App Service Plan**: Provisioned to host potential web apps.
- **Database**: Azure SQL Database for relational data storage.

## Deployment Workflow

Below are the Azure CLI commands used to deploy the infrastructure, with explanations for each step.
1. Log in to Azure

        az login

2. Create a Resource Group

        az group create --name iacazcli --location westus


3. Create a Virtual Network (VNet)

       az network vnet create --name vnazcli --resource-group iacazcli --address-prefixes 18.0.0.0/16


4. Add a Subnet to the VNet

        az network vnet subnet create --name subazcli --resource-group iacazcli --vnet-name vnazcli --address-prefixes 18.0.34.0/24

5. Create a Network Security Group (NSG)

        az network nsg create --name nsgazcli --resource-group iacazcli


6. Add an HTTP Allow Rule to the NSG

        az network nsg rule create --name AlloHttpInbound --nsg-name nsgazcli --resource-group iacazcli --priority 100 --source-address-prefixes '*' --source-port-ranges '*' --destination-address-prefixes '*' --destination-port-ranges 80 --access Allow --protocol Tcp


7. Associate the NSG with the Subnet

        az network vnet subnet update --resource-group iacazcli --name subazcli --vnet-name vnazcli --network-security-group nsgazcli


8. Create a Public IP Address

        az network public-ip create --resource-group iacazcli --name pubipazcli --sku Basic --allocation-method Dynamic --location westus

9. Create a Network Interface Card (NIC)

        az network nic create --name nicazcli --resource-group iacazcli --subnet subazcli --location westus --public-ip-address pubipazcli --vnet-name vnazcli


10. Create a Virtual Machine

        az vm create --name vmazcli --resource-group iacazcli --location westus --size Standard_B2s --admin-username student --admin-password "@AdminPasswd1" --nics nicazcli --image Win2019Datacenter


11. Create a Storage Account

        az storage account create --name saccountazcli --resource-group iacazcli --location westus --sku Standard_LRS

12. Create an App Service Plan

        az appservice plan create --resource-group iacazcli --name applanazcli --is-linux --number-of-workers 4 --sku S2


13. Create a SQL Server

        az sql server create -l westus -g iacazcli -n sqlserverazcli -u student -p "@PasswdAdmin2"


14. Create a SQL Database

        az sql db create -g iacazcli -s sqlserverazcli -n mydbazcli --service-objective S0


## Evidence 

![Azure CLI](https://github.com/OLekgetho/Images/blob/main/Azure%20CLI/AZURE%20CLI.png)



## Outcome
This project successfully demonstrates my ability to:
- Use Azure CLI for Infrastructure as Code (IaC) tasks.
- Configure a secure and scalable environment for applications.
- Deploy cloud infrastructure components efficiently and systematically.


## Skills Gained
- Azure CLI: Proficiency in resource creation and management.
- Networking: Configuring VNets, subnets, and NSG rules.
- Database Setup: Deploying and managing Azure SQL resources.
- Cloud Resource Deployment: Comprehensive understanding of Azure IaaS services.
