



## Setup 

![image-20230519163848550](C:\Users\simon\AppData\Roaming\Typora\typora-user-images\image-20230519163848550.png)

**From server ping SVI IP - 10.88.0.1 (You should be able to ping)** 

![image-20230519164015948](C:\Users\simon\AppData\Roaming\Typora\typora-user-images\image-20230519164015948.png)

**Do a show ARP - you should see virtual mac address - 00:1c:73:00:00:12 attached to 10.88.0.1**

![image-20230519162409797](C:\Users\simon\AppData\Roaming\Typora\typora-user-images\image-20230519162409797.png)

**Now shut down border leaf 1 SVI Vlan 88 - and now do a ping again from server see if it works? if it does then enable the SVI on border leaf 1**

**after shutdown the border leaf1 SVL vlan88 the host can ping the 10.88.0.1**

![image-20230519162538649](C:\Users\simon\AppData\Roaming\Typora\typora-user-images\image-20230519162538649.png)

**Now shutdown  border leaf 2 SVI Vlan 88 - do a ping from server - It would fail.**

![image-20230519162824588](C:\Users\simon\AppData\Roaming\Typora\typora-user-images\image-20230519162824588.png)

**shutdown border-1 leaf and border-2 leaf SVI, from the host s1-Core ping the 10.88.0.1 will be failure.**

Also, even both SVIs are up, we can't ping from borderleaf to the server IP but we can ping from server to the SVIs 

![image-20230519163148300](C:\Users\simon\AppData\Roaming\Typora\typora-user-images\image-20230519163148300.png)



The problem that we are facing with the config you sent: when we shutdown one SVI on the borderleaf the server can't reach the SVI anymore, even after we clear arp etc. I did some tcp dump and tests if you need to refer. 

**shutdown one SVI of border-leaf2**

![image-20230519163501979](C:\Users\simon\AppData\Roaming\Typora\typora-user-images\image-20230519163501979.png)



Some observations:
Noticed  I can't ping from border leaf to server IP (on both) but can ping from server to SVI (it's strange)

**From the Border-leaf2 can ping the server**

![image-20230519165939965](C:\Users\simon\AppData\Roaming\Typora\typora-user-images\image-20230519165939965.png)

Enabled tcpdump on the both brd routers - it's always brd2 responding to icmp so if SVI is shutdown on brd 2, brd 1 never gets a request.

Always border2-leaf response to the ICMP.

Another test:
Removed ip virtual-router mac-address 00:1c:73:00:00:12 from brd leaf
Removed from vxlan interface "vxlan virtual-router encapsulation mac-address 00:1c:73:00:00:12"
From server now can see brd2 mac for SVI (in arp table, not the virtual), when shut down and clear arp still can't ping - means anycast never getting picked by brd1)

Got the device border-leaf2 SVI mac 

![image-20230519170714071](C:\Users\simon\AppData\Roaming\Typora\typora-user-images\image-20230519170714071.png)

![image-20230519170440857](C:\Users\simon\AppData\Roaming\Typora\typora-user-images\image-20230519170440857.png)

















































































