# Home Lab Networking
This project showcases my ability to configure networks and network devices. It also showcases my knowledge on topics such as: Dynamic Routing, Inter-VLAN Routing, IPv4 & IPv6, Spanning Tree, DHCP, First-Hop Redundancy, EtherChannels, Port Security, Logging Messages, DNS, and More.

## Table Of Contents

- [ROAS Configuration](#ROAS)
- [Office Configuration](#Office)
- [Collapsed Core & IPv6 Configuration](#Collapsed)
- [OSPF Configurations](#OPSF)
- [PAT Configuration](#PAT)

# ROAS
<img width="592" height="383" alt="image" src="https://github.com/user-attachments/assets/991c1a0d-980d-4561-877a-472a8a0c64f2" /><br/>
3 subnets and 3 VLANs, the routing takes care of the inter-VLAN routing 

Current configuration : 1632 bytes<br/>
!<br/>
version 15.4<br/>
no service timestamps log datetime msec<br/>
no service timestamps debug datetime msec<br/>
no service password-encryption<br/>
!<br/>
hostname R1<br/>
!<br/>
!<br/>
no ip cef<br/>
no ipv6 cef<br/>
!<br/>
!<br/>
ip name-server 10.0.0.2<br/>
!<br/>
!<br/>
spanning-tree mode pvst<br/>
!<br/>
!<br/>
interface Loopback0<br/>
 ip address 1.1.1.1 255.255.255.255<br/>
!<br/>
interface GigabitEthernet0/0/0<br/>
 no ip address<br/>
 ip ospf 1 area 0<br/>
 duplex auto<br/>
 speed auto<br/>
!<br/>
interface GigabitEthernet0/0/0.10<br/>
 encapsulation dot1Q 10<br/>
 ip address 172.16.0.1 255.255.0.0<br/>
 ip ospf 1 area 0<br/>
!<br/>
interface GigabitEthernet0/0/0.20<br/>
 encapsulation dot1Q 20<br/>
 ip address 192.168.0.1 255.255.255.0<br/>
 ip ospf 1 area 0<br/>
!<br/>
interface GigabitEthernet0/0/0.30<br/>
 encapsulation dot1Q 30<br/>
 ip address 10.0.0.1 255.0.0.0<br/>
 ip ospf 1 area 0<br/>
!<br/>
interface GigabitEthernet0/0/1<br/>
 no ip address<br/>
 duplex auto<br/>
 speed auto<br/>
 shutdown<br/>
!<br/>
interface Serial0/1/0<br/>
 no ip address<br/>
 clock rate 2000000<br/>
 shutdown<br/>
!<br/>
interface Serial0/1/1<br/>
 no ip address<br/>
 clock rate 2000000<br/>
 shutdown<br/>
!<br/>
interface Serial0/2/0<br/>
 ip address 162.10.9.1 255.255.255.252<br/>
 ip ospf network point-to-point<br/>
 clock rate 2000000<br/>
!<br/>
interface Serial0/2/1<br/>
 ip address 162.10.8.1 255.255.255.252<br/>
 ip ospf network point-to-point<br/>
 clock rate 2000000<br/>
!<br/>
interface Vlan1<br/>
 no ip address<br/>
 shutdown<br/>
!<br/>
router ospf 1<br/>
 log-adjacency-changes<br/>
 passive-interface GigabitEthernet0/0/0<br/>
 passive-interface Loopback0<br/>
 passive-interface GigabitEthernet0/0/0.10<br/>
 passive-interface GigabitEthernet0/0/0.20<br/>
 passive-interface GigabitEthernet0/0/0.30<br/>
 network 162.10.0.0 0.0.255.255 area 0<br/>
!<br/>
ip classless<br/>
!<br/>
ip flow-export version 9<br/>
!<br/>
!<br/>
line con 0<br/>
!<br/>
line aux 0<br/>
!<br/>
line vty 0 4<br/>
 login<br/>
!<br/>
!<br/>
end<br/>

This is the current configuration for R1; it uses subinterfaces for each VLAN to allow for Inter-VLAN Routing. Each subinterface uses the first available IP Address in that subnet. Each PC has connectivity and can also contact the DNS server.<br/>
<img width="514" height="275" alt="image" src="https://github.com/user-attachments/assets/560dc73b-7d6f-41e7-8b1f-12983f1841a3" /><br/>
The Router forwards all DNS Requests to the DNS Server, and this allows the PCs to ping each other using names.<br/>
<img width="408" height="222" alt="image" src="https://github.com/user-attachments/assets/2fc63978-60c4-425f-abf2-a30c8d5937e5" /><br/>
<img width="400" height="219" alt="image" src="https://github.com/user-attachments/assets/e42eca55-2346-452d-ba6a-309a795d1e5b" /><br/>

