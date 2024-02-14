## ERSPAN configure 

### 1. topo

![image-20230717090443118](C:\Users\simon\AppData\Roaming\Typora\typora-user-images\image-20230717090443118.png)



### 2. configuration 

**a. Add the ACL for ERSPAN** 

`!`
`ip access-list ERSPAN-ACL`
   `10 permit ip 10.1.1.0/24 20.1.1.0/24`

**b. create the ERSPAN**

```
monitor session ERSPAN ip access-group ERSPAN-ACL
monitor session ERSPAN source Ethernet1 rx
monitor session ERSPAN destination tunnel mode gre source 10.1.1.1 destination 10.2.2.2
```

**c. interface configuration**  

```
!
interface Ethernet1
   description TC1
   no switchport
   ip address 10.1.1.1/24
!
interface Ethernet2
   description TC2
   no switchport
   ip address 20.1.1.1/24
!
interface Ethernet3
   description TC3
   no switchport
   ip address 30.1.1.2/24
!
```

**d. add the static route to the ERSPAN tunnel destination address**

```
ip route 10.2.2.2/32 30.1.1.1
```



### 3. verification on TC3 

```
`root@Server-3:/home/vyos# tcpdump -i eth1`
`tcpdump: verbose output suppressed, use -v or -vv for full protocol decode`
`listening on eth1, link-type EN10MB (Ethernet), capture size 65535 bytes`
`01:00:10.451899 IP 10.1.1.1 > 10.2.2.2: GREv0, length 102: gre-proto-0x88be`  //Get the ERPAN traffic 
`01:00:10.451931 IP 10.2.2.2 > 10.1.1.1: ICMP 10.2.2.2 protocol 47 unreachable, length 130`
`01:00:11.451879 IP 10.1.1.1 > 10.2.2.2: GREv0, length 102: gre-proto-0x88be`
`01:00:11.451907 IP 10.2.2.2 > 10.1.1.1: ICMP 10.2.2.2 protocol 47 unreachable, length 130`
`01:00:12.451907 IP 10.1.1.1 > 10.2.2.2: GREv0, length 102: gre-proto-0x88be`
`01:00:12.451941 IP 10.2.2.2 > 10.1.1.1: ICMP 10.2.2.2 protocol 47 unreachable, length 130`
`01:00:13.451894 IP 10.1.1.1 > 10.2.2.2: GREv0, length 102: gre-proto-0x88be`
```

