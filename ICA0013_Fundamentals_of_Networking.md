# ICA0013 Fundamentals Of Networking

     [Login MOTD Banner](#)
     [Configuring an interface](#)
       [Configuring SVI IP for remote access](#)
   [Viewing running configuration](#)
   [Saving configuration](#)
   [Resetting configuration](#)
 [COMPUTER](#computer)

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
  
## SWITCH/ROUTER

### Connecting to a switch/router using console port

#### Setting up physical connection

1. Connect a RJ-45 Ethernet cable to the port labelled **"Console"** on the (back of the) switch / (front of the) router.
2. Connect the other end to the correct port on the **"Patch Panel"**.
   1. Connect the ethernet end of the **"Console Cable"** to the port on the wall, serial end to the computer's COM (serial) port.
   2. [Optional] Connect **"USB to DB9"** adapter to the serial end of the **"Console Cable"**.
   3. [Optional] Connect the USB end of the **"USB to DB9"** adapter to the computer.

#### Using PuTTY/TeraTerm to connect to a switch/router

1. Open PuTTY/TeraTerm.
2. Select **"Serial"** connection.
3. Choose the correct **"COM Port"**.
4. Click on "Connect".
5. If nothing shows up, press *Enter* a couple of times.
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

**"Switch> |"** --> No EXEC Mode
**"Switch# |"** --> EXEC Mode

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

**"Switch# |"** --> Not in configure mode
**"Switch(config)# |"** --> In configure mode

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
Switch(config)# hostname <NAME>
<NAME>(config)#
```

``` bash
Switch(config)# hostname S1
S1(config)#
```

### Setting password

#### EXEC Mode

``` bash
Switch(config)# enable secret <PASSWORD>
```

``` bash
Switch(config)# enable secret thisismypassword
```

#### TELNET/SSH

``` bash
Switch(config)# line vty 0 4
Switch(config-line)# password <PASSWORD>
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

#### Console connection

``` bash
Switch(config)# line con 0
Switch(config-line)# password <PASSWORD>
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

### Disabling DNS Lookup

``` bash
Switch(config)# no ip domain-lookup
```

### Setting a MOTD banner

``` bash
Switch(config)# 
```
