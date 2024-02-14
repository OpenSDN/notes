CLI Access Modes:

# Operational Mode:

o    Use operational mode to view information about firewall & the traffic running through.

o    Use to perform operations such as restarting, loading configuration, or shutting down.

o    When log in to Firewall , the Command Line Interface (CLI) opens in operational mode.

o    Palo Alto Firewall Operational Mode, command prompt sign is a greater then sing ( >).

# Configuration Mode:

o    Use configuration mode to view and modify the Palo Alto Firewall configuration.

o    You can switch between operational mode and configuration mode at any time.

o    Command prompt changes from a > to a #, indicating that successfully changed modes.

o    Switch from configuration mode to operational mode, use either quit or exit command.

o    To enter operational mode command while in configuration mode, use the run command.

 

![img](file:///C:/Users/simon/AppData/Local/Temp/msohtmlclip1/01/clip_image003.gif)**Operational**—Use operational mode to view information about the Firewall.

**Configuration**—Use configuration mode to view and modify the configuration.

 

 

| **Symbol  or Key** | **Description**                                              |
| ------------------ | ------------------------------------------------------------ |
| *                  | Indicates that the option is required.                       |
| >                  | Indicates that there are additional nested commands.         |
| +                  | Indicates that the option has an associated value that you must  enter. |
| \|                 | Allows you to  filter command output.                        |
| Tab Key            | Automatically complete the command.                          |
| Exit               | Switch from configuration mode to operational mode.          |
| Quit               | Switch from configuration mode to operational mode.          |
| Run                | To run operational mode command while in configuration mode. |
| ?                  | Show list of the available commands appears.                 |
| Commit             | Save candidate config to the running config                  |

 

|      |                                                              |
| ---- | ------------------------------------------------------------ |
|      | ![img](file:///C:/Users/simon/AppData/Local/Temp/msohtmlclip1/01/clip_image005.jpg) |





 

 

|      |                                                              |
| ---- | ------------------------------------------------------------ |
|      | ![img](file:///C:/Users/simon/AppData/Local/Temp/msohtmlclip1/01/clip_image007.jpg) |







# CLI Management Commands:

| **Commands**                                                 | **Description**                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| > show  interface management                                 | Show management  Interface details                           |
| > show  system info                                          | Display  system’s management IP, Serial  number, and  code version |
| > show system disk-space                                     | Show percent usage of disk partitions.                       |
| > show system software status                                | Show running processes.                                      |
| > show system resources                                      | Show processes running in management plane.                  |
| > show running resource-monitor                              | Show resource utilization in the data plane.                 |
| > request license info                                       | Show the licenses installed on the device.                   |
| > show jobs processed                                        | Show when commits are completed.                             |
| > show  session info                                         | Display session  usage, rate etc information.                |
| > show session id <session-id>                               | Display information about a specific session.                |
| > show running security-policy                               | Show the running security policy.                            |
| > request restart system                                     | Restart the device.                                          |
| > request shutdown system                                    | Shutdown the device.                                         |
| >request system private-data-reset                           | Default Factory reset command                                |
| > show admins                                                | Show administrators who are currently logged.                |
| > show  admins all                                           | Show administrators  who can access the web  interface or  command line interface CLI. |
| > ping host <destination-ip-address>                         | Ping from management interface                               |
| > ping  source <ip-address-on-dataplane> host <destination-ip-address> | Ping from a  dataplane interface to a destination IP address |
| > show running nat-policy                                    | Shows current NAT policy table.                              |
| > show running ippool                                        | Shows NAT pool utilization.                                  |
| > show  running global-ippool                                | Shows NAT pool  utilization.                                 |
| > show routing route                                         | Shows routing table.                                         |
| > show running security-policy                               | Shows current policy set.                                    |
| > show vpn flow                                              | Shows encap/decap counters                                   |
| > show vpn gateway                                           | Shows list of IKE gateway configurations.                    |
| > show vpn ike-sa                                            | Shows IKE Phase 1 SA                                         |
| > show vpn ipsec-sa                                          | Shows IPSEC Phase 2 SA.                                      |
| > show vpn tunnel                                            | List of auto-key IPSec tunnel configurations.                |
| > show  high-availability state                              | Shows the HA  state of the device.                           |
| > show high-availability all                                 | Shows settings configured on device & peer.                  |
| > show  high-availability state-  synchronization            | Shows if the  devices are synchronized                       |
| > request  high-availability state suspend                   | Suspends active  device and makes passive  device active     |
| > request high-availability state functional                 | Changes the state from suspend to passive.                   |
| > request license info                                       | Shows the license installed on the device.                   |



| **Commands**                                                 | **Description**                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| # set zone Outside                                           | Create zone with name Outside.                               |
| # set network virtual-router VR-1                            | Create Virtual Router named VR-1                             |
| # set network  interface ethernet ethernet1/1  layer3 ip  192.168.100.100/24 | Assign IP  address and subnet mask to  interface  ethernet 1/1 and set as Layer 3 |
| # set deviceconfig system type static                        | Set the interface type to static                             |
| # set deviceconfig system type dhcp-client                   | Set the interface type to DHCP                               |
| # set deviceconfig system dns-setting servers                | Set Primary and Secondary DNS                                |
| # set mgt-config users admin password                        | Set Administrator password                                   |
| # set deviceconfig system ip-address                         | Assign IP address to Management interface.                   |
| > find command                                               | Display entire command in current mode.                      |
| > find command keyword show                                  | Locate all commands have specified  keyword.                 |

 

|      |                                                              |
| ---- | ------------------------------------------------------------ |
|      | ![img](file:///C:/Users/simon/AppData/Local/Temp/msohtmlclip1/01/clip_image009.jpg) |





 

GUI Error Prompts.

o    The GUI provides guidance when configure the Palo Alto Network firewall.

o    Red underline indicates tabs, which must be completed for a given interface.

o    The Yellow highlights specify that fields is required and must to enter or type.

|      |                                                              |
| ---- | ------------------------------------------------------------ |
|      | ![img](file:///C:/Users/simon/AppData/Local/Temp/msohtmlclip1/01/clip_image012.gif) |

The OK button will be unavailable if the interface is missing required infor