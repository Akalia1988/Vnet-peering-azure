# Vnet-peering-azure

Issues we had before implementing VNET peering. 
our databases are living on VMs within different regions our API Applications and azure functions were associated to different VNET hence they couldnt communicate with our backend database unless we whitelist public IP's which were not an option. 

•	IP Address whitelisting through IaaS VMs’s Network interface is not scalable
•	All PaaS and IaaS provisioned resources are publicly exposed
•	SQL database instances running on VM’s “should” be migrated to DaaS/PaaS equivalents
•	Publicly expose API Management interface that supports internally accessible service backends.

Solution was proposed is below along with architectural design. 

![image](https://user-images.githubusercontent.com/58148717/104051727-36c56e80-51ae-11eb-86db-e69039f2cbb8.png)

Benefits are below

VNET peering for same region
VNET peering for global region
1) Network Traffic between Peered virtual Network is private
2) Low Latency(Immediate/quick response) and high bandwidth connection
3) Traffic is routed directly through the Microsoft backbone infr and not through gateway or public internet so no spoofing
4) Peering is not transitive i.e if VNet1 is peered with VNET2 and VNET2 is peered with VNET3. Then VNET1 cannot talk to VNET3. We have to expliciltly establish peering
5) Private IP ranges which we shall be selecting for VNET peering shouldnt overlap.

After VNET integration we were able to connect with our backend resources via private network and our webapps are communication via Private network. 

Below is the diagram of end product. 

![image](https://user-images.githubusercontent.com/58148717/104052490-6d4fb900-51af-11eb-89f8-bb604097764e.png)




