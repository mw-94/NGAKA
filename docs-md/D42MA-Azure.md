# How to Deploy Device42 on Azure: Main Appliance

## 1.) Go to the Azure Marketplace

Look for Device42 – Visualize Your Entire IT Infrastructure and click on “Get it now”.

## 2.) Fill in virtual machine details

You will need to specify the following:

- Resource group
- Virtual machine name
- Size of VM – please note that you should choose something with at least 4 GB RAM and 2 CPU (recommended 4 vCPU/8GB) or else you will get out of memory errors.
- Administrator account – choose Authentication Type as Password. Note: This field has no bearing on Device42 deployment.
- Networking
- Disks
## 3.) Click on Review & Create.

After validation, deployment should start.

The Azure deployment creates the following resources by default:

- Microsoft.Network/networkInterfaces
- Microsoft.Network/publicIpAddresses
- Microsoft.Network/networkSecurityGroups
- Microsoft.Compute/virtualMachines
## 4.) Configure the network security group

Allow the following inbound ports:

- 404 – ssh access
- 443 – Web GUI and API access
- 4343 – appliance manager SSL port
## 5.) Enable the VM serial console

## 6.) Get your Device42 Azure VM’s instance ID

Run the following command in the Azure Shell to get the vmId

    az vm show –name <VM Name> –resource-group <resource group name>


![1](media/D42MA-Azure_1.png?raw=true "We’ll need value from vmId.")

## 7.) Login to the Device42 console

Go to the serial console of your Device42 Azure VM or use ssh port 404 to login with username device42 and the password as the vmId value from previous step.  

You will be prompted to set admin password and appliance manager d42admin password.
Once this is set, you can change the device42 console user password to something of your own choosing or keep it as is.  

You should now have a fully functioning Device42 Main Appliance hosted on Microsoft Azure. The default version currently is set to 15.17.02. You will need to update this version to the latest and supply your own license for full, up to date functionality.
