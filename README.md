# Home Lab Networking
This project showcases my ability to configure networks and network devices. It also showcases my knowledge on topics such as: Dynamic Routing, Inter-VLAN Routing, IPv4 & IPv6, Spanning Tree, DHCP, First-Hop Redundancy, EtherChannels, Port Security, Logging Messages, DNS, and More.

## Table Of Contents

- [ROAS Configuration](#ROAS)
- [Office Configuration](#Office)
- [Collapsed Core & IPv6 Configuration](#Collapsed)
- [OSPF Configurations](#OPSF)
- [PAT Configuration](#PAT)
- [Known Issues & Misconfigurations](#Issues)

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
The servers have manually configured addresses; the first 10 usable IP addresses are excluded from the DHCP pool. <br/>
The default gateways of the end hosts are configured to be the Virtual IP used by both routers. Router 2 is configured as the active router, and Router 3 is configured as the standby router. Preemption is also enabled.<br/>
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
DHCP Snooping is also enabled on all the switches, with the interfaces connected to end hosts being untrusted, and the interfaces connected to other network devices being trusted.<br/>

# Collapsed
<img width="655" height="622" alt="image" src="https://github.com/user-attachments/assets/51b894cf-23c3-42d6-a890-1ebbb86624c1" /> <br/>
This is a standard two-tier campus design, 3 access switches, and 2 distribution switches. There are 3 VLANs, and the distribution switches handle the Inter-VLAN routing. <br/>
Each SVI uses the first available address of the respective VLAN Subnet, and all hosts can ping each other. <br/>
<img width="408" height="193" alt="image" src="https://github.com/user-attachments/assets/5aae82d6-6928-44cb-88dd-37a2e1e7ccfb" /><br/>
<img width="426" height="194" alt="image" src="https://github.com/user-attachments/assets/7423cdc1-c7a5-4873-92a4-fbf5102b1594" /><br/>
<img width="408" height="197" alt="image" src="https://github.com/user-attachments/assets/eb365f07-5cdf-49a3-a215-c11fe2c50b0b" /><br/>

A Layer 3 Etherchannel is also configured for load balancing between the distribution switches, as well as OSPFv3 enabled on the routers and distribution switches. An NTP is also supposed to be enabled on the network, but due to packet tracer's limitations, IPv6 NTP is not supported. <br/>
HSRP would have also been configured on each SVI to allow for redundancy between the two distribution switches in case one fails. <br/>
This network in particular has a lot of issues, which are further discussed in Known Issues & Misconfigurations. <br/>


