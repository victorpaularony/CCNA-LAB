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

