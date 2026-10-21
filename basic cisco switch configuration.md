**Basic Switch Configuration CISCO ISO Commands**



**switch> en**

**switch# conf t**

**switch(config)# hostname sw1**         (setting up hostname)

**sw1(config)# enable secret Password**		(configure enable password protection to the privileged EXEC mode (encrypted))

&#x20;To set password for the console access through the console cable

**sw1(config)#line console 0**

**sw1(config-line)# password Cisco123**

**sw1(config-line)#login**		(without this the line password does not enable the usual console password prompt.)

**sw1(config-line)#exit**		 (moves back exactly one level into global config mode)

**sw1(config)#**



(or use end i.e)

**sw1(Config-line)# end**		(exit config mode completely to privileged root prompt)

**sw1#**



**configuring the management IP Address**

&#x09;Layer2 switches need ip address assigned (VLAN1) for remote access

**sw1(config)# interface vlan 1**		(interface config mode for VLAN1)

**sw1(config-if)# ip address 192.168.1.10 255.255.255.0**		(ipv4 address and subnet mask of class C/24)

**sw1(config-if)# no shutdown**		(turn on the virtual interface)

**sw1(config-if)# exit**



&#x20;**Setup default gateway**

&#x09;to enable the switch to be access from different network from the local network for remote access
**sw1(config)# ip default-gateway 192.168.1.1**



Enable remote Access(VYT Line)

virtual terminal(VYT) to allow access using protocols like SSH or Telnet

**sw1(config)# line vty 0 4**

**sw1(config-line)# password YourRemotePassword**

**sw1(config-line) login**

**sw1(config-line)#exit**



**Enable SSH and Telnet access**

**sw1(config)# line vty 0 4**

**sw1(config-line)# transport input ssh telnet** 		(in packet tracer use **transport input all**)

**sw1(config-line)#exit**



**Encrypt all clear text password**

**sw1(config)# service password-encryption**



**Adding a legal Banner(MOTD)**

&#x09;Message of the day(MOTD)- display legal warning to anyone attempting to login for unauthorized access:

**sw1(config)# banner motd $ WARNING: Unauthorized access is prohibited! $**



**Save the Configuration**

&#x09;All configs are written to the RAM and if switch reboots the configs disappear unless saved to NVRAM(startup configuration ):

**sw1(config)# exit**

**sw1# copy running-config startup-config**







**Popular Show commands**

**#show ip interface brief** 	(display all interface, their IP addresses and their current status and protocols)

**#show ipv6 interface brief**

**#show ip route**		(display content of the IP routing table stored in RAM)

**#show ipv6 route**

**#show ip interface** 		(display statistic for all interfaces on the device)

**#show ip interface** 	 	display IPV4 statistics for all interface on the router

**#show ipv6 interface** 		Display the IPV6 stats for all interface on router)





Basic CISCO switch configuration workflow

1. Power on
2. connect via console
3. enter enable mode 
4. configure terminal
5. set hostname
6. configure password 
7. set management IP address
8. save configuration





**Other Switch commands** 

**(config-line)# logging synchronous** 		(prevent system log(syslog) and status sms from interrupting the command line while you are typing)

**(config-line)# exec-timeout 10 15**		(after 10min and 15sec inactivity session is timeout.)

**(config-line)# history size 10**		(show command history of console connection set to 10 commands)

(config-if)# no shutdown		(enable the interface by changing its administrative state from "administratively down" to "up"... turn on the ports so as to send and receive data)

\#write 		(to save all the configuration)

\# logout 	(logout of the session or end session)

