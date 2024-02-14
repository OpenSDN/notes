### 1. configure the BOGON-V4 file on the Http server as following format.

```
(base) root@AGX:/var/www/html# cat BOGON-V4.txt 
   seq 10 permit 0.0.0.0/8 ge 8
   seq 20 permit 10.0.0.0/8 ge 8
   seq 30 permit 172.16.0.0/12 ge 12
   seq 40 permit 192.168.0.0/16 ge 16
   seq 50 permit 100.64.0.0/10 ge 10
   seq 60 permit 127.0.0.0/8 ge 8
   seq 70 permit 169.254.0.0/16 ge 16
   seq 80 permit 192.0.0.0/24 ge 24
   seq 90 permit 192.0.2.0/24 ge 24
   seq 100 permit 198.18.0.0/15 ge 15
   seq 110 permit 198.51.100.0/24 ge 24
   seq 120 permit 203.0.113.0/24 ge 24
   seq 130 permit 224.0.0.0/4 ge 4
   seq 140 permit 240.0.0.0/4 ge 4
   seq 150 permit 255.255.255.255/32 
#Then apply the deny cause in the route-map for the prefix
```

### 2. configure the ip-prefix BOGON-V4 on EOS

```
#Need to make sure the http server can be reached and can get the prefix correcly.
#Failure conditon 
EOS-1(config)#ip prefix-list BOGON-V4 source http://17.1.1.101/BOGON-V4.txt 
% Download prefix list test from http://17.1.1.101/BOGON-V4.txt failed: [Errno 0] 
---- Connecting to 17.1.1.101 (17.1.1.101) port 80
**** Socket error (No route to host) - reconnecting
---- Connecting to 17.1.1.101 (17.1.1.101) port 80
**** Socket error (No route to host) - reconnecting
get: /BOGON-V4.txt: Fatal error: max-retries exceeded (No route to host)

#Successful condition should like below, the command can be configure without any error

ip prefix-list test source http://17.1.1.100/BOGON-V4.txt 

#check the prefix list BOGON-V4 
refresh ip prefix-list BOGON-V4
refreshed ip prefix-list BOGON-V4 source http://17.1.1.100/BOGON-V4.txt
Num entries: 15
```

### 3. Configure the schedule and refresh the prefix each 5min

```
#Create the schedule each 5min to refresh the ip-prefix from http server

schedule updateprefix interval 5 timeout 2 max-log-files 20 command "refresh ip prefix-list BOGON-V4"

#Check the schedule status below 
EOS-1(config)#show schedule updateprefix
The last CLI command failed with exit status 1
CLI command ""refresh ip prefix-list BOGON-V4"" is scheduled next at "02:22:43 05/26/2023", interval is 5 minutes
Timeout is 2 minutes
Maximum of 20 log files will be stored
Verbose logging is off
4 log files currently stored in flash:schedule/updateprefix/

Start time                 Size          Filename                                      
----------------------- ---------------- ----------------------------------------------
May 26 2023 02:17       77.0 bytes       CloudEOS-1_updateprefix_2023-05-26.0217.log.gz
May 26 2023 02:12       77.0 bytes       CloudEOS-1_updateprefix_2023-05-26.0212.log.gz
May 26 2023 02:07       77.0 bytes       CloudEOS-1_updateprefix_2023-05-26.0207.log.gz
May 26 2023 01:49       77.0 bytes       CloudEOS-1_updateprefix_2023-05-26.0149.log.gz
```

