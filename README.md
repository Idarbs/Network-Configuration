# Networking Project
This project showcases my ability to configure networks and network devices. It also showcases my knowledge on topics such as: Dynamic Routing, Inter-VLAN Routing, IPv4 & IPv6, Spanning Tree, DHCP, First-Hop Redundancy, EtherChannels, Port Security, Logging Messages, DNS, and More. <br/>

# Overview
<img width="1543" height="505" alt="image" src="https://github.com/user-attachments/assets/4e1c898b-d3d4-4871-9bc7-12147a6d1571" /><br/>
Feel free to check out the Packet Tracer file to see every network device's configuration! <br/>

## Table Of Contents

- [ROAS Configuration](#ROAS)
- [Office Configuration](#Office)
- [Collapsed Core & IPv6 Configuration](#Collapsed)
- [OSPF Configurations](#OSPF)
- [PAT Configuration](#PAT)
- [Known Issues & Misconfigurations](#Issues_And_Misconfigurations)

# ROAS
<img width="592" height="383" alt="image" src="https://github.com/user-attachments/assets/991c1a0d-980d-4561-877a-472a8a0c64f2" /><br/>
3 subnets and 3 VLANs, the router takes care of the inter-VLAN routing. Unused Interfaces are shutdown as well.


Subinterfaces are configured for each VLAN to allow for Inter-VLAN Routing. Each subinterface uses the first available IP Address in that subnet. Each PC has connectivity and can also contact the DNS server.<br/>
<img width="514" height="275" alt="image" src="https://github.com/user-attachments/assets/560dc73b-7d6f-41e7-8b1f-12983f1841a3" /><br/>
The Router forwards all DNS Requests to the DNS Server, and this allows the PCs to ping each other using names.<br/>
<img width="408" height="222" alt="image" src="https://github.com/user-attachments/assets/2fc63978-60c4-425f-abf2-a30c8d5937e5" /><br/>
<img width="400" height="219" alt="image" src="https://github.com/user-attachments/assets/e42eca55-2346-452d-ba6a-309a795d1e5b" /><br/>
Port Security is enabled on the access switch; only 1 device is allowed on each interface, and the MAC Address is stored on the device. Violation Mode is also enabled, so that the interface stays up and sends messages. <br/>
<img width="428" height="121" alt="image" src="https://github.com/user-attachments/assets/a3326f1d-98c3-409f-94cd-a09e0baa44e1" /><br/>

# Office
<img width="563" height="634" alt="image" src="https://github.com/user-attachments/assets/44b7b5f1-36e4-48d2-9ca2-3b4fedc8ca2a" /><br/>
Multiple hosts connected to access switches, with a couple of servers running, and two routers configured with HSRP as well as being DHCP servers.<br/>
VTP is enabled on the switches, all of them running version 2, and 3 of three switches running in client mode, and one switch running in server mode.
The servers have manually configured addresses; the first 10 usable IP addresses are excluded from the DHCP pool. <br/>
The default gateways of the end hosts are configured to be the Virtual IP Address used by both routers. Router 2 is configured as the active router, and Router 3 is configured as the standby router. Preemption is also enabled.<br/>
<img width="502" height="400" alt="image" src="https://github.com/user-attachments/assets/0f477a59-2110-4ae9-9e56-d420b94ccdca" /><br/>
<img width="512" height="350" alt="image" src="https://github.com/user-attachments/assets/0001f96f-04c2-4931-ae07-6f69db236323" /><br/>
<img width="413" height="200" alt="image" src="https://github.com/user-attachments/assets/da363e33-d047-46a0-97f4-d5da92a2980a" /><br/>


Logging is also enabled and is sent to the server from the routers. All alerts will be sent to the server regardless of severity. <br/>
<img width="659" height="564" alt="image" src="https://github.com/user-attachments/assets/8fda4907-b288-4f7b-b8b2-e8533988fcf9" /><br/>

The Routers are also able to access the FTP server and download files from it. <br/>
<img width="383" height="133" alt="image" src="https://github.com/user-attachments/assets/99e5e24c-6a32-4e5a-97f8-265fa316cd55" /><br/>
NOTE: This screenshot was taken prior to the manual configuration of the server's IP Address (which is why the IP Address is different from the one in the overview of the network). <br/>
<img width="446" height="155" alt="image" src="https://github.com/user-attachments/assets/c21a5d16-e50b-4c9f-9b84-6e412d58dcd0" /><br/>

<img width="572" height="262" alt="image" src="https://github.com/user-attachments/assets/8599f657-7074-4dd2-bd92-6af9f4bcdbd4" /><br/>
Rapid-PVST is enabled on all switches. All the switches have the default priority. Switch 2 becomes the Root Bridge because it has the lowest MAC Address out of the 4 switches.<br/>

<img width="434" height="298" alt="image" src="https://github.com/user-attachments/assets/9792d320-4599-4b1a-b5cb-d43649efdbdb" /><br/>
Port Security is enabled on both access switches, with a maximum of 1 MAC Address per interface, with the one exception being the interface that has the end host and the VoIP phone.<br/>
DHCP Snooping is also enabled on all the switches, with the interfaces connected to end hosts being untrusted and the interfaces connected to other network devices being trusted.<br/>

# Collapsed
<img width="655" height="622" alt="image" src="https://github.com/user-attachments/assets/51b894cf-23c3-42d6-a890-1ebbb86624c1" /> <br/>
This is a standard two-tier campus design, 3 access switches, and 2 distribution switches. There are 3 VLANs, and the distribution switches handle the Inter-VLAN routing. <br/>
Each SVI uses the first available address of the respective VLAN Subnet, and all hosts can ping each other. <br/>
<img width="408" height="193" alt="image" src="https://github.com/user-attachments/assets/5aae82d6-6928-44cb-88dd-37a2e1e7ccfb" /><br/>
<img width="426" height="194" alt="image" src="https://github.com/user-attachments/assets/7423cdc1-c7a5-4873-92a4-fbf5102b1594" /><br/>
<img width="408" height="197" alt="image" src="https://github.com/user-attachments/assets/eb365f07-5cdf-49a3-a215-c11fe2c50b0b" /><br/>

A Layer 3 Etherchannel is also configured for load balancing between the distribution switches, as well as OSPFv3 enabled on the routers and distribution switches. An NTP Server is also supposed to be enabled on the network, but due to Packet Tracer's limitations, IPv6 NTP is not supported. <br/>
HSRP would have also been configured on each SVI to allow for redundancy between the two distribution switches in case one fails. <br/>
This network in particular has a lot of issues, which are further discussed in Known Issues & Misconfigurations. <br/>

# OSPF
<img width="791" height="269" alt="image" src="https://github.com/user-attachments/assets/b598f8d3-1099-428b-b195-3e2041fd77bb" /><br/>
OSPF has been configured and allows hosts in ROAS and the Office network to communicate with each other. <br/>
There are multiple OSPF routers to allow for redundancy. <br/>
Both sides can communicate with each other. <br/>
Each interface in the OSPF routers uses a /30 mask, as well as has its network types set as point-to-point to skip the BR/BDR elections. <br/>
For the SVIs in the ROAS network, they are advertised, and this allows each host in each VLAN to communicate with others outside their network. <br/>
Since HSRP is configured in the office network, both routers have interfaces connected to OSPF routers in case one of the other fails, and they need to reach the outside networks. <br/>

# PAT
 <img width="403" height="154" alt="image" src="https://github.com/user-attachments/assets/92918406-67c5-4853-bf91-d2f6abd35e07" /> <br/>
 PAT is configured on this network. PAT allows for multiple end hosts to use the same IP Address, which allows us to conserve IP Addresses. <br/>
 The ACL configured on the router allows for any host in the 172.31.10.0 subnet to have its IP Address translated.
 Both end hosts use private Class B IP Addresses inside the network, but use the Router's outside IP Address when communicating with other end hosts in other networks.<br/>
 Before it exits the network, the packet source is the end host's private IP Address.<br/>
 <img width="612" height="727" alt="image" src="https://github.com/user-attachments/assets/fcf3364b-bd9b-4b5c-ad55-0f1a27547bc8" /><br/>
 The source of the IP Address is now using the Router's outside IP Address as it travels throughout the network.<br/>
 <img width="569" height="742" alt="image" src="https://github.com/user-attachments/assets/5919cf73-46df-4197-9d7d-d503dd05fc64" /><br/>
 When the reply is sent back to the host, it uses the Router's IP Addresses as its destination IP.<br/>
 <img width="575" height="706" alt="image" src="https://github.com/user-attachments/assets/9925c0a3-2219-41f2-9783-b78cd273adf7" /><br/>
 Finally, when the packet arrives back at the router, it swaps out the destination IP Address to the host's private IP Address.<br/>
 <img width="572" height="729" alt="image" src="https://github.com/user-attachments/assets/39a6f453-59e9-425b-99ad-18cdf4aa38b8" /><br/>

 # Issues_And_Misconfigurations
 - IPv6 Hosts occasionally lose connectivity; some PCs can ping each other, while others cannot. Reopening the labs fixes it (sometimes).
 - When putting the SVIs in OSPv3 areas, hosts lose connectivity. Removing the areas and reopening the lab seems to fix the connectivity, but this also means the SVIs cannot be advertised.
 - HSRP for IPv6 isn't supported (from what I know), meaning SVIs are not currently redundant.
 - NTP for IPv6 cannot be configured (CLI does not give the option to input an IPv6 address).
 - When opening the lab, the first few pings won't work (ARP takes a while).
 - FTP downloads are slow (I'm assuming this is a packet tracer issue).
 - OSPv3 for IPv6 isn't configured properly.
 - Due to how large the lab is, it can sometimes act weird, especially when it has been open for a while.
 - Because of how large the lab is, when using simulation mode, it is flooded with NDP, STP, OSPF, HSRP, and other protocols, making it hard to see the specific packet you are looking for.
 - DHCP will sometimes give PCs different addresses than before (PC0 will get 10.32.0.11, other times it will get 10.32.0.12); it's not really an issue, just something to note.
 - End hosts using DHCP have to be manually set to DHCP mode every time the lab is opened.
