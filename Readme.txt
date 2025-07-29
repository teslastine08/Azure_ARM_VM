Creat Azure Profile
Install Azure ARM tools in local environment
Creat the Json Files in a designated directory
run and deploy the Azure environment: New-AzResourceGroupDeployment -Name RDP -ResourceGroupName sre-ank-08 -TemplateFile .\RDP.json -TemplateParameterFile .\RDP_Parameters.json

(VM name mustnot contain any special characters)

Overall Structure
The template is divided into:

parameters – values passed during deployment (e.g., username, location)

resources – actual Azure resources created (like VM, NSG, NIC, etc.)

outputs – useful info returned after deployment (e.g., public IP)

These are inputs you provide during deployment:

vmName: Name of the VM (e.g., "rdp-vm")

adminUsername: Windows admin username (e.g., "ankan08")

adminPassword: Secure password

location: Azure region (e.g., "eastus")

vmSize: Size/Type of VM (default is "Standard_B1s")

Creates a dynamic public IP so you can RDP to the VM.
Defines a virtual network (10.0.0.0/16) and a subnet (10.0.0.0/24) — like a private LAN for your VM.
Connects the VM to:

The subnet inside the VNet

The public IP (so it can be accessed from the internet)

The NSG (Network Security Group) — to allow/deny traffic like RDP

This is the actual Windows Server 2022 VM.

OS profile: Sets computer name, admin username, and password

Storage profile: Defines the OS disk (uses latest Windows Server image)

Hardware profile: Sets the VM size

Network profile: Attaches the NIC created above

Acts like a firewall. This NSG:

Allows inbound TCP traffic on port 3389 (RDP)

Blocks all else by default

After deployment, Azure will return the public IP address of the VM so you can RDP into it.
