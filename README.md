# Azure Vwan lab with SpokeFW - vnet2vnet and S2S

This creates a vwan with a hub and a couple of spoke vnets with VM's and a firewall vnet all connected to the vhub, and the spokes are peered to the FW vnet as well. All internet and spoke to spoke and spoke to onprem traffic is pointed to the Azure firewall in the firewall vnet by a custom route table on the hub that the spokes are associated to. The default able has routes to reach the spokes via the firewall.  This creates a log analytics workspace and diagnostic settings for the firewall logs. You'll be prompted for the resource group name, location where you want the resources created, your public ip and username and password to use for the VM's. NSG's are placed on the default subnets of each vnet allowing RDP access from your public ip and route tables are added sending traffic to your public ip to the internet. This also creates a logic app that will delete the resource group in 24hrs.

One thing to be aware of, you cannot simply delete the resource group and have it remove all the resources on this one. You either need to delete the spoke1 and spoke2 vnet connections to the hub, or just run the "labdelete" logic app and it will take care of it all.

The topology will look like this:

![wvanlabwithspokefw--vnet2vnets2s](https://github.com/user-attachments/assets/497173be-80ed-49cb-a5e8-0f12e3ceb0d6)


You can run Terraform right from the Azure cloud shell by cloning this git repository with "git clone https://github.com/quiveringbacon/AzureVwanlabwithSpokeFW-vnet2vnetandS2S.git ./terraform".

Then, "cd terraform" then, "terraform init" and finally "terraform apply -auto-approve" to deploy.
