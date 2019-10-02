# ICA0013 Fundamentals Of Networking

Cheat sheet for Cisco Networking Labs.
Can be used on: Cisco IOS and Microsoft Windows Vista, 7, 8, 8.1, 10.

- [ICA0013 Fundamentals Of Networking](#ica0013-fundamentals-of-networking)
  - [SWITCH/ROUTER](#switchrouter)
    - [Connecting to a switch/router using console port](#connecting-to-a-switchrouter-using-console-port)
      - [Setting up physical connection](#setting-up-physical-connection)
      - [Using PuTTY/TeraTerm to connect to a switch/router](#using-puttyteraterm-to-connect-to-a-switchrouter)
    - [Viewing switch/router info](#viewing-switchrouter-info)
    - [Enabling and disabling "EXEC Mode"](#enabling-and-disabling-%22exec-mode%22)
    - [Viewing and setting time](#viewing-and-setting-time)
      - [Viewing time](#viewing-time)
      - [Setting time](#setting-time)
    - [Configuring terminal](#configuring-terminal)
      - [Setting hostname](#setting-hostname)
      - [Setting password](#setting-password)
        - [EXEC Mode](#exec-mode)
        - [TELNET/SSH](#telnetssh)
        - [Console connection](#console-connection)
      - [Disabling DNS Lookup](#disabling-dns-lookup)
      - [Setting a MOTD banner](#setting-a-motd-banner)
      - [Configuring an interface](#configuring-an-interface)
    - [Viewing running configuration](#viewing-running-configuration)
    - [Saving configuration](#saving-configuration)
    - [Resetting configuration](#resetting-configuration)
    - [Viewing status of connected interfaces](#viewing-status-of-connected-interfaces)
    - [Viewing MAC address of switch](#viewing-mac-address-of-switch)
    - [Viewing ARP table of the switch/router](#viewing-arp-table-of-the-switchrouter)
    - [Viewing MAC address table](#viewing-mac-address-table)
    - [View interface status](#view-interface-status)
    - [Clear MAC address table](#clear-mac-address-table)
    - [View routing table](#view-routing-table)
  - [COMPUTER](#computer)
    - [Configuring IPv4 address](#configuring-ipv4-address)
    - [Opening Command Prompt](#opening-command-prompt)
    - [Viewing interfaces, IP, MAC address, gateway, subnet mask](#viewing-interfaces-ip-mac-address-gateway-subnet-mask)
    - [Pinging](#pinging)
    - [Viewing ARP table of the computer](#viewing-arp-table-of-the-computer)
  - [About](#about)
  
## SWITCH/ROUTER

### Connecting to a switch/router using console port

#### Setting up physical connection

1. Connect a RJ-45 Ethernet cable to the port labelled **"Console"** on the (back of the) switch / (front of the) router.
2. Connect the other end to the correct port on the **"Patch Panel"**.
3. Connect the ethernet end of the **"Console Cable"** to the port on the wall, serial end to the computer's COM (serial) port.
4. [Optional] Connect **"USB to DB9"** adapter to the serial end of the **"Console Cable"**.
5. [Optional] Connect the USB end of the **"USB to DB9"** adapter to the computer.

#### Using PuTTY/TeraTerm to connect to a switch/router

1. Open PuTTY/TeraTerm.
2. Select **"Serial"** connection.
3. Choose the correct **"COM Port"**.
4. Click on "Connect".
5. If nothing shows up, hit *ENTER* a couple of times.
6. Say *no* to the prompt.

``` bash
Would you like to enter the initial configuration dialog? [yes/no]: n
```

### Viewing switch/router info

``` bash
Switch> show version
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2012 by Cisco Systems, Inc.
Compiled Sat 28-Jul-12 00:29 by prod_rel_team

ROM: Bootstrap program is C2960 boot loader
BOOTLDR: C2960 Boot Loader (C2960-HBOOT-M) Version 12.2(53r)SEY3, RELEASE SOFTWARE (fc1)

Switch uptime is 2 minutesSystem returned to ROM by power-onSystem image file is "flash://c2960-lanbasek9-mz.150-2.SE.bin"
<output omitted>
```

### Enabling and disabling "EXEC Mode"

> **"Switch>"** --> No EXEC Mode
> **"Switch#"** --> EXEC Mode

``` bash
Switch> enable
Switch# |
```

``` bash
Switch# disable
Switch> |
```

``` bash
Switch# exit
Switch> |
```

### Viewing and setting time

#### Viewing time

``` bash
Switch> show clock
*00:30:05.261 UTC Mon Mar 1 1993
```

#### Setting time

``` bash
Switch# clock set 14:56:24 Oct 02 2019
*Oct 02 14:56:24.000: %SYS-6-CLOCKUPDATE: System clock has been updated from 00:31:43 UTC Mon Mar 1 1993 to 14:56:24 UTC Wed Oct 02 2019, configured from console by console.
```

### Configuring terminal

> **"Switch#"** --> Not in configure mode
> **"Switch(config)#"** --> In configure mode

``` bash
Switch# conf t
Switch(config)# |
```

``` bash
Switch(config)# exit
Switch# |
```

#### Setting hostname

``` bash
Switch(config)# hostname NAME
NAME(config)#
```

``` bash
Switch(config)# hostname S1
S1(config)#
```

#### Setting password

##### EXEC Mode

``` bash
Switch(config)# enable secret PASSWORD
```

``` bash
Switch(config)# enable secret thisismypassword
```

##### TELNET/SSH

``` bash
Switch(config)# line vty 0 4
Switch(config-line)# password PASSWORD
Switch(config-line)# login
Switch(config-line)# exit
Switch(config)# |
```

``` bash
Switch(config)# line vty 0 4
Switch(config-line)# password thisismypassword
Switch(config-line)# login
Switch(config-line)# exit
Switch(config)# |
```

##### Console connection

``` bash
Switch(config)# line con 0
Switch(config-line)# password PASSWORD
Switch(config-line)# login
Switch(config-line)# exit
Switch(config)# |
```

``` bash
Switch(config)# line con 0
Switch(config-line)# password thisismypassword
Switch(config-line)# login
Switch(config-line)# exit
Switch(config)# |
```

#### Disabling DNS Lookup

``` bash
Switch(config)# no ip domain-lookup
```

#### Setting a MOTD banner

``` bash
Switch(config)# banner motd #
Enter TEXT message. End with the character '#'.
Unauthorized access is strictly prohibited and prosecuted to the full extent of the law. #
Switch(config)# |
```

#### Configuring an interface

> *"no shut"* command enables the interface.

``` bash
Switch(config)# interface INTERFACE_NAME INTERFACE_NO
Switch(config-if)# ip address IP_ADDRESS SUBNET_MASK
Switch(config-if)# no shut
Switch(config-if)# exit
Switch(config)# |
```

``` bash
Switch(config)# interface gigabitethernet 0/0
Switch(config-if)# ip address 192.168.1.0 255.255.255.0
Switch(config-if)# no shut
Switch(config-if)# exit
Switch(config)# |
```

### Viewing running configuration

``` bash
S1# show run
Building configuration...
Current configuration : 1508 bytes
!
! Last configuration change at 00:06:11 UTC Mon Mar 1 1993
!
version 15.0
no service pad
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname S1
!
<output omitted>
```

### Saving configuration

``` bash
Switch# copy running-config startup-config
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
Switch# |
```

### Resetting configuration

1. Delete VLAN configuration.

    ``` bash
    Switch# delete vlan.dat
    Delete filename [vlan.dat]? y
    Delete flash:/vlan.dat? [confirm] y
    Switch# |
    ```

2. Erase startup-config.

    ``` bash
    Switch# erase startup-config
    Erasing the nvram filesystem will remove all configuration files! Continue? [confirm] y
    [OK]
    Erase of nvram: complete
    Switch# |
    ```

3. Reload the switch.

    ``` bash
    Switch# reload
    Proceed with reload? [confirm] y
    System configuration has been modified. Save? [yes/no]: n
    ```

### Viewing status of connected interfaces

``` bash
Switch# show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
Vlan1                  unassigned      YES unset  up                    up
FastEthernet0/1        unassigned      YES unset  up                    up
FastEthernet0/2        unassigned      YES unset  down                  down
FastEthernet0/3        unassigned      YES unset  down                  down
FastEthernet0/4        unassigned      YES unset  down                  down
FastEthernet0/5        unassigned      YES unset  down                  down
<output omitted>
```

### Viewing MAC address of switch

``` bash
Switch# show interfaces vlan 1
Vlan1 is up, line protocol is up
    Hardware is EtherSVI, address is 001b.0c6d.8f40 (bia 001b.0c6d.8f40)
    Internet address is 192.168.1.1/24
<output omitted>
```

### Viewing ARP table of the switch/router

``` bash
Switch# show arp
Protocol  Address          Age (min)  Hardware Addr   Type   Interface
Internet  192.168.1.1             -   001b.0c6d.8f40  ARPA   Vlan1
Internet  192.168.1.3             0   5c26.0a24.2a60  ARPA   Vlan1
```

### Viewing MAC address table

Use [MAC Vendor Lookup](https://www.macvendorlookup.com/) to lookup the vendor of the device using the MAC address.

``` bash
Switch# show mac address-table
          Mac Address Table
-------------------------------------------
Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
 All    0100.0ccc.cccc    STATIC      CPU
 All    0100.0ccc.cccd    STATIC      CPU
 All    0180.c200.0000    STATIC      CPU
 All    0180.c200.0001    STATIC      CPU
 All    0180.c200.0002    STATIC      CPU
 All    0180.c200.0003    STATIC      CPU
 All    0180.c200.0004    STATIC      CPU
 All    0180.c200.0005    STATIC      CPU
 All    0180.c200.0006    STATIC      CPU
 All    0180.c200.0007    STATIC      CPU
 All    0180.c200.0008    STATIC      CPU
 All    0180.c200.0009    STATIC      CPU
 All    0180.c200.000a    STATIC      CPU
 All    0180.c200.000b    STATIC      CPU
 All    0180.c200.000c    STATIC      CPU
 All    0180.c200.000d    STATIC      CPU
 All    0180.c200.000e    STATIC      CPU
 All    0180.c200.000f    STATIC      CPU
 All    0180.c200.0010    STATIC      CPU
 All    ffff.ffff.ffff    STATIC      CPU
   1    5c26.0a24.2a60    DYNAMIC     Fa0/6
Total Mac Addresses for this criterion: 21
```

### View interface status

``` bash
Switch# show interface F0/1
```

### Clear MAC address table

``` bash
Switch# clear mac address-table dynamic
```

**Wait 10 seconds.**

### View routing table

> **C**: Direct Connection
> **L**: Local Connection
> **R**: Remote Connection

``` bash
Router# show ip route
```

## COMPUTER

### Configuring IPv4 address

1. Open **"Control Panel"**.
2. Go to **"Network and Internet" > "Network and Sharing Center" > ADAPTER_NAME > "Properties" > "Internet Protocol Version 4 (TCP/IPv4)" > "Properties"**.
3. Select **"Use the following IP address:"**.
4. Type the IP, subnet mask, [gateway].
5. Press *"OK"*.

### Opening Command Prompt

1. Press *WIN* + *R*.
2. Type *"cmd"*.
3. Hit *ENTER*, or click *"Run"*.

### Viewing interfaces, IP, MAC address, gateway, subnet mask

``` bash
C:\Users\USERNAME\> ipconfig /all

Windows IP Configuration

   Host Name . . . . . . . . . . . . : COMPUTERNAME
   Primary Dns Suffix  . . . . . . . :
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No

Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Intel(R) Ethernet Connection (2) I219-V
   Physical Address. . . . . . . . . : 4C-CD-6A-AE-0D-2E
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe81::ac43:6f38:d9e2:189c%15(Preferred)
   IPv4 Address. . . . . . . . . . . : 192.168.1.13(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Lease Obtained. . . . . . . . . . : Wednesday, 2 October 2019 11:51:27
   Lease Expires . . . . . . . . . . : Thursday, 3 October 2019 11:53:30
   Default Gateway . . . . . . . . . : 192.168.1.1
   DHCP Server . . . . . . . . . . . : 192.168.1.1
   DHCPv6 IAID . . . . . . . . . . . : 374131818
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-24-C6-10-C5-00-E0-4A-68-A4-D6
   DNS Servers . . . . . . . . . . . : 1.1.1.1
   NetBIOS over Tcpip. . . . . . . . : Enabled

C:\Users\USERNAME\> |
```

### Pinging

``` bash
C:\Users\USERNAME\> ping IP_ADDRESS_OR_SITE

Pinging IP_ADDRESS_OR_SITE [IP_OF_DESTINATION] with 32 bytes of data:
Reply from IP_OF_DESTINATION: bytes=32 time=15ms TTL=54
Reply from IP_OF_DESTINATION: bytes=32 time=14ms TTL=54
Reply from IP_OF_DESTINATION: bytes=32 time=11ms TTL=54
Reply from IP_OF_DESTINATION: bytes=32 time=12ms TTL=54

Ping statistics for IP_OF_DESTINATION:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 11ms, Maximum = 15ms, Average = 13ms

C:\Users\USERNAME\> |
```

### Viewing ARP table of the computer

> **ff-ff-ff-ff-ff-ff**: Multicast or broadcast.

``` bash
C:\Users\USERNAME\> arp -a

Interface: 25.63.150.45 --- 0xa
  Internet Address      Physical Address      Type
  25.255.255.255        ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static

C:\Users\USERNAME\> |
```

---

## About

By Adil Atalay Hamamcıoğlu, a Cybersecurity Engineering student at Tallinn University of Technology, 2019 - 2023.
Made this cheat-sheet to not to suffer in Cisco Networking Labs.
