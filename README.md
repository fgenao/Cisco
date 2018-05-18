# Cisco
## Configuring Layer 3 EtherChannels on a Cisco Catalyst 3750 IOS Ver 12.2(44)SE2
To configure Layer 3 EtherChannels, create the port-channel logical interface and then put the Ethernet
interfaces into the port-channel.
### Creating Port-Channel Logical Interfaces
This example shows how to create port-channel interface 1:
```
Switch# configure terminal
Switch(config)# interface port-channel 1
Switch(config-if)# ip address 172.32.52.10 255.255.255.0
Switch(config-if)# end
This example shows how to verify the configuration of port-channel interface 1:
Switch# show running-config interface port-channel 1
Building configuration...
Current configuration:
!
interface Port-channel1
 ip address 172.32.52.10 255.255.255.0
 no ip directed-broadcast
end
Switch#
```
### Configuring Physical Interfaces as Layer 3 EtherChannels
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
