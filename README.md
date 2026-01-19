# Network Modernization: SDN Deployment across restaurant 60 sites 

## The problem
Retail environments can sometimes lag behind the rest of the world when it comes to technology adoption. When I was brought on to help this company update their infrastructure, networks were completely non-standard, were largely using consumer grade networking gear, and required on-site intervention in order to change configurations and troubleshoot errors. They had grown to 60 retail locations who were relatively spread out across the state but didn’t have networking infrastructure to support their growth. While the devices were inexpensive, the labor to support them and the downtime resulting from their lack of reliability far outweighed the savings of getting these consumer grade tools. 

## A solution
Balancing their frugality as a core value and their need for solid networking gear that will *just work* in their increasingly busy and internet-powered kitchens, I selected the ecosystem of TP-Link’s Omada to be the backbone of their new, modern SDN. They needed a reliable kit, they wanted to fully *own* the equipment, and they wanted to host the software controller themselves. Many solutions were considered but ultimately Omada was the appropriate choice. 

## Implementation
I engineered the deployment from initial design ideas to overseeing the full roll-out across the entire company. 

### Omada Software Controller hosting
Debian VM via GCP 

### Omada hardware stack
Gateway: ER605<br/>
Switching: SG2210P, SG2218P, SG2428P<br/>
AP: EAP613(US)<br/>

### Configuration standards 
#### VLAN
* VLAN 0 - management / omada hardware only<br/>
* VLAN 10 - guest, client isolation, only accessible via WLAN guest SSID<br/>
* VLAN 20 - isolated devices, client isolation, for devices outside of establishment configuration, i.e., jukebox managed by outside service. Only accessible via physical connection, restricted to isolated port on the gateway.<br/>
* VLAN 30 - POS network, MAC whitelist, very limited DHCP only for maintenance. Accessibly both via WLAN SSID and physical connection. <br/>
* VLAN 40 - Phone & camera network, wider DCHP pool, for devices under in-house management. Only accessible through physical connection<br/>
* VLAN 50 - employee/manager network. Only accessibly via WLAN<br/>

#### ACL 
Standard firewall rules preventing communication across VLANs, specifically for the protection of the protection of VLAN 30, the POS network

### Deployment
Pre-provisioned by my team via “Gold Image” configuration strategy. Technicians (and sometimes myself if previous infrastructure was expected to be difficult to clean up) needed to only hook everything up and it would come online with WAN connection. 

The process took place over the course of eight months, where we kept a slow but steady roll-out pace. This deployment was balanced against support requirements, ensuring that we were keeping our stores online and happy while we made our way through the company, overhauling their networks. 

## Outcomes
* This initiative virtually eliminated site visits to just reboot something or make sure something was correctly plugged in–we knew if it was or wasn’t because we could see it on the dashboard
* The SDN provided deep insight into how networks were actually being utilized, leading to operational changes and improvments
* The SDN allowed for content filtering to be utilized, ending a significant network abuse issue that was not previously tracked or even known about. 
* The equipment **just worked**, and unprecedented uptime and stability continues to enable a growing investment in internet-based business (online order, VoIP phones, DoorDash)
* IT staff knows about network issues before store staff notice, and can start working on solutions right away, and are not waiting to be told about issues. 
