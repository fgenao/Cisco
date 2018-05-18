# Cisco
## Configuring Layer 2 EtherChannels on a Cisco Catalyst 3750 IOS Ver 12.2(44)SE2
To configure Layer 2 EtherChannels, create the port-channel logical interface and then put the Ethernet
interfaces into the port-channel.
### Creating Port-Channel Logical Interfaces
This example shows how to create port-channel interface 1:
```cisco
Switch# configure terminal
Switch(config)# interface port-channel 1
Switch(config-if)# end
```
This example shows how to verify the configuration of port-channel interface 1:
```
Switch# show running-config interface port-channel 1
Building configuration...
Current configuration: 92 bytes
!
interface Port-channel1
 switchport trunk encapsulation dot1q
 switchport mode trunk
end
Switch#
```
### Configuring Physical Interfaces as Layer 2 EtherChannels
This example shows how to configure Fast Ethernet interfaces 5/4 and 5/5 into port-channel 1 with PAgP
mode desirable:
```
Switch# configure terminal
Switch(config)# interface range fastethernet 5/4 - 5 !(Note: Space is mandatory.)
Switch(config-if)# no switchport
Switch(config-if)# no ip address
Switch(config-if)# channel-group 1 mode desirable
Switch(config-if)# end
```

The following two examples shows how to verify the configuration of Gigabit Ethernet interface 1/0/25:
```
Switch# show running-config interface GigabitEthernet1/0/25
Building configuration...
Current configuration: 129 bytes
!
interface GigabitEthernet1/0/25
switchport trunk encapsulation dot1q
switchport mode trunk
no ip directed-broadcast
 channel-group 1 mode active
end

Switch# show interfaces GigabitEthernet1/0/25 etherchannel
Port state    = Up Mstr Assoc In-Bndl 
Channel group = 1           Mode = Active          Gcchange = -
Port-channel  = Po1         GC   =   -             Pseudo port-channel = Po1
Port index    = 0           Load = 0x00            Protocol =   LACP

Flags:  S - Device is sending Slow LACPDUs   F - Device is sending fast LACPDUs.
        A - Device is in active mode.        P - Device is in passive mode.

Local information:
                            LACP port     Admin     Oper    Port        Port
Port      Flags   State     Priority      Key       Key     Number      State
Gi1/0/25  SA      bndl      32768         0x1       0x1     0x19        0x3D  

Partner's information:

                  LACP port                        Admin  Oper   Port    Port
Port      Flags   Priority  Dev ID          Age    key    Key    Number  State
Gi1/0/25  SA      32768     b862.1f81.e100   4s    0x0    0x1    0x135   0x3D  

Age of the port in the current state: 76d:19h:56m:30s
```
This example shows how to verify the configuration of port-channel interface 1 after the interfaces have
been configured:
```
Switch# show etherchannel 1 port-channel
		Port-channels in the group: 
		---------------------------

Port-channel: Po1    (Primary Aggregator)

------------

Age of the Port-channel   = 76d:20h:05m:03s
Logical slot/port   = 10/1          Number of ports = 3
HotStandBy port = null 
Port state          = Port-channel Ag-Inuse 
Protocol            =   LACP
Port security       = Disabled

Ports in the Port-channel: 

Index   Load   Port     EC state        No of bits
------+------+------+------------------+-----------
  0     00     Gi1/0/25 Active             0
  0     00     Gi1/0/27 Active             0
  0     00     Gi1/0/28 Active             0

Time since last port bundled:    76d:20h:03m:55s    Gi1/0/27
```
