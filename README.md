# Home Lab Networking
This project showcases my ability to configure networks and network devices. It also showcases my knowledge on topics such as: Dynamic Routing, Inter-VLAN Routing, IPv4 & IPv6, Spanning Tree, DHCP, First-Hop Redundancy, EtherChannels, Port Security, Logging Messages, DNS, and More.

## Table Of Contents

- [ROAS Configuration](#ROAS)
- [Office Configuration](#Office)
- [Collapsed Core & IPv6 Configuration](#Collapsed)
- [OSPF Configurations](#OPSF)
- [PAT Configuration](#PAT)

# ROAS
<img width="592" height="383" alt="image" src="https://github.com/user-attachments/assets/991c1a0d-980d-4561-877a-472a8a0c64f2" />
3 subnets and 3 VLANs, the routing takes care of the inter-VLAN routing 

Current configuration : 1632 bytes
!
version 15.4
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1
!
!
no ip cef
no ipv6 cef
!
!
ip name-server 10.0.0.2
!
!
spanning-tree mode pvst
!
!
interface Loopback0
 ip address 1.1.1.1 255.255.255.255
!
interface GigabitEthernet0/0/0
 no ip address
 ip ospf 1 area 0
 duplex auto
 speed auto
!
interface GigabitEthernet0/0/0.10
 encapsulation dot1Q 10
 ip address 172.16.0.1 255.255.0.0
 ip ospf 1 area 0
!
interface GigabitEthernet0/0/0.20
 encapsulation dot1Q 20
 ip address 192.168.0.1 255.255.255.0
 ip ospf 1 area 0
!
interface GigabitEthernet0/0/0.30
 encapsulation dot1Q 30
 ip address 10.0.0.1 255.0.0.0
 ip ospf 1 area 0
!
interface GigabitEthernet0/0/1
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/1/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/1/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/2/0
 ip address 162.10.9.1 255.255.255.252
 ip ospf network point-to-point
 clock rate 2000000
!
interface Serial0/2/1
 ip address 162.10.8.1 255.255.255.252
 ip ospf network point-to-point
 clock rate 2000000
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 1
 log-adjacency-changes
 passive-interface GigabitEthernet0/0/0
 passive-interface Loopback0
 passive-interface GigabitEthernet0/0/0.10
 passive-interface GigabitEthernet0/0/0.20
 passive-interface GigabitEthernet0/0/0.30
 network 162.10.0.0 0.0.255.255 area 0
!
ip classless
!
ip flow-export version 9
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
end

This is the current configuration for R1; it uses subinterfaces for each VLAN to allow for Inter-VLAN Routing. Each subinterface uses the first available IP Address in that subnet. Each PC has connectivity and can also contact the DNS server.
<img width="514" height="275" alt="image" src="https://github.com/user-attachments/assets/560dc73b-7d6f-41e7-8b1f-12983f1841a3" />
The Router forwards all DNS Requests to the DNS Server, and this allows the PCs to ping each other using names.
<img width="408" height="222" alt="image" src="https://github.com/user-attachments/assets/2fc63978-60c4-425f-abf2-a30c8d5937e5" />
<img width="400" height="219" alt="image" src="https://github.com/user-attachments/assets/e42eca55-2346-452d-ba6a-309a795d1e5b" />

