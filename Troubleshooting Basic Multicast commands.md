### Troubleshooting: Basic Multicast commands

**PIM:**

```
show ip mroute x.x.x.x detail --> Great to see RP, IIF, OIL, FLAGs set, OILs that are not programmed (Typically reason si also mentioed i.e say we are the Assert Loser or not the reciever DR)

show ip pim interface ---> To check who is the DR on the segment, if we have any PIM neighbors, if there are any drops at the CPU (such as for RPF failures etc)

show ip pim protocol counters --> To check if we recived/sent register stops (FHR/RP), sent/received registers(FHR/RP), received any errors (Debugging failed neighborships or registrations etc)

show ip pim rp-hash <Group> --> To check the current used RP IP for a specifc group

show ip mfib <group> --> Great to check the Activity timer, check for fast drops if any

show ip mfib software <group> --> Especially helpful to detremine if multicast traffic is hitting the CPU. If traffic is hitting the CPU either the counter will increment or the state will be "Unresolved" both a good indicative that something is amiss and traffic is hitting the CPU instead of gretting programmed in HW

show ip pim config-sanity ---> For basic misconfigurations
```

**IGMP:**

```
show ip igmp snooping groups x.x.x.x detail ---> For a particular group to check if there are any valid receivers

show ip igmp snooping mrouter --> Check if the switch has any mrouters. Even if the above command yeilds no results (is empty), the switch will forward any received traffic on a valn to its mrouter ports on that vlan. A switch may have one or more mrouter ports.

show ip igmp snooping querier --> Especiallyhelpful in L2 setups. While IGMP snooping by default is enabled, it is not effective unless there is a querier of some sort on that vlan

show ip igmp snooping counters -> Good to get a quick snapsjot of joins/leaves/queries received/transmitted on an interface
```



**tcpdump**

```
tcpdump -i vlanxxx igmp src xxxx dst xxxx  --->to check the IGMP join messages 


```

