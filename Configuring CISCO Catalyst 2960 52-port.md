**Configuring CISCO Catalyst 2960 52-port switch**

configuring the switch with three vlans step by step

step by step checklist

1. Set hostname and administrative passwords(sw1,enable secret, console login)
2. Create departmental VLANs(VLAN 2 ICT, VLAN 3 HR, VLAN 4 SALES)
3. Assign 14 ports to each department (fa0/1-14, fa0/15-28, fa0/29-42)
4. Secure unused ports (fa043-48 assigned to VLAN 999 and shut down
5. handle uplinks correctly (keep unused uplinks shut down; configure trunk when required)
6. verify VLAN membership and connectivity (show vlan brief,show interface status, PC ping tedts)
7. save the configuration (copy running-config startup-config)





Network Design

Cisco Catalyst 2960- sw1

&#x09;vlan 10-ICT (14 ports fa0/1-14 192.168.10.0/24)

&#x09;vlan 20-HR (14 ports fa0/15-28 198.168.20.0/24)

&#x09;vlan 30-Sales (14 ports fa0/29-42 198.168.30.0/24)

&#x09;unused 999 (6 ports)

&#x09;uplink  \_\_  (2 ports Gi0/1 - gi0/2)



Step to Configure the switch

1. Connect to the switch

   1. use console cable and a terminal application(putty or in packet tracer)
   2. Inspect the switch if it has configurations(backup then erase)
switch>
   3. Enter privileged mode

&#x09;switch> enable

&#x09;switch#

&#x20;   4. Enter global configuration mode

&#x09;switch# configure terminal

&#x09;switch(config)#

2\. Configure the switch identity and basic security

&#x09;switch(config)# hostname sw1

&#x09;sw1(config)# enable secret Password

&#x09;sw1(config)# service password-encryption

&#x09;sw1(config)# no ip domain-lookup	(prevent the switch from trying DNS lookups)

&#x09;sw1(config)# banner motd $Authorized users only$



&#x09;Configure the console password

&#x09;sw1(config)# line console 0

&#x09;sw1(config-line)# password ConsolePassword

&#x09;sw1(config-line)# login

&#x09;sw1(config-line)# logging synchronous		(reduce command-line SMS interruptions)

&#x09;sw1(config-line)# exec-timeout 10 0		(logout idle console after 10min)

&#x09;sw1(config-line)# exit



3\. Create the three VLANs

&#x09;sw1(config)# vlan 10

&#x09;sw1(config-vlan)# name ICT

&#x09;sw1(config-vlan)# exit



&#x09;sw1(config)# vlan 20

&#x09;sw1(config-vlan)# name HR

&#x09;sw1(config-vlan)# exit



&#x09;sw1(config)# vlan 30

&#x09;sw1(config-vlan)# name SALES

&#x09;sw1(config-vlan)# exit



&#x20;  Now check the vlan (this will enable to see VLANs 10,20,30 but the ports will appear after assigning)

&#x09;sw1(config)# end

&#x09;sw1# show vlan brief



&#x09;

4\. Assign 14 portd to ICT

&#x09;sw1#configure terminal

&#x09;sw1(config)# interface range fastEthernet 0/1 - 14

&#x09;sw1(config-if-range)# description ICT\_DEPERTMENT

&#x09;sw1(config-if-range)# switchport mode access

&#x09;sw1(config-if-range)# switchport access vlan 10

&#x09;sw1(config-if-range)# spanning-tree portfast		(enable endpoint port ports to transition to forwarding quickly on ports connected to end devices not switch-to-switch link)

&#x09;sw1(config-if-range)# end



5\. Assign 14 ports to HR

&#x09;sw1#configure terminal

&#x09;sw1(config)# interface range fastEthernet 0/15 - 28

&#x09;sw1(config-if-range)# description HR\_DEPARTMRNT

&#x09;sw1(config-if-range)# switchport access vlan 20

&#x09;sw1(config-if-range)# spanning-tree portfast

&#x09;sw1(config-if-range)# end



6\. Assign 14 ports to SALEs

&#x09;sw1#configure terminal

&#x09;sw1(config)# interface range fastEthernet 0/15 - 28

&#x09;sw1(config-if-range)# description SALES\_DEPARTMRNT

&#x09;sw1(config-if-range)# switchport access vlan 30

&#x09;sw1(config-if-range)# spanning-tree portfast

&#x09;sw1(config-if-range)# end



7\. Disable unused ports

&#x20;   to reduce risk of someone plugging an unauthorized device into an active network port.

&#x09;sw1#configure terminal

&#x09;sw1(config) vlan 999

&#x09;sw1(config-vlan)# name UNUSED\_PORTS

&#x09;sw1(config-vlan)# exit

&#x20;   Assign the unused ports to VLAN 999 and disable them

&#x09;sw1(config)# interface range fastEthernet 0/43 - 48

&#x09;sw1(config-if-range)# description UNUSED\_PORTS

&#x09;sw1(config-if-range)# switchport mode access

&#x09;sw1(config-if-range)# switchport access vlan 999

&#x09;sw1(config-if-range)# shutdown

&#x09;sw1(config-if-range)# exit



8\. Configure the Gigabit uplink port

&#x20;   In this they are reserved for router or switch connection. If not in use then should be disabled

&#x09;sw1# configure terminal

&#x09;sw1(config)# interface range gigabitEthernet 0/1 - 2

&#x09;sw1(config-if-range)# description RESERVED\_UPLINK

&#x09;sw1(config-if-range)# shutdown

&#x09;sw1(config-if-range)# end



&#x09;Connection of a trunk incase there was two or more switches of IEEE802.1Q

&#x09;sw1#configure terminal

&#x09;sw1(config)# interface gigabitEthernet 0/1

&#x09;sw1(config-if)# description TRUNK\_TO\_ROUTER

&#x09;sw1(config-if)# switchport mode trunk

&#x09;sw1(config-if)# switchport trunk allowed vlan 10,20,30

&#x09;sw1(config-if)# no shutdown

&#x09;sw1(config-if)# end



9\. Configure a management IP address

&#x20;   Giving the switch management IP address for remote access(for this use an address within the ICT subnet)

&#x09;sw1# configure terminal

&#x09;sw1(config)# interface vlan 10

&#x09;sw1(config-if)# ip address 192.168.10.2 255.255.255.0

&#x09;sw1(config-if)# no shutdown

&#x09;sw1(config-if)# end

