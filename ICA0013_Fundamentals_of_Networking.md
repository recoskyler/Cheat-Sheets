# ICA0013 Fundamentals Of Networking

## Index

 [SWITCH/ROUTER](#switchrouter)
   [Connecting to a switch/router using console port](#connecting-to-a-switchrouter-using-console-port)
     [Setting up physical connection](#setting-up-physical-connection)
     [Using PuTTY/TeraTerm to connect to a switch/router](#)
   [Viewing switch/router info](#)
   [Enabling and disabling "Privilaged Mode"](#)
   [Viewing and setting time](#)
   [Changing configuration](#)
     [Setting hostname](#)
     [Setting password](#)
       [Console](#)
       [Privilaged Mode](#)
       [TELNET/SSH](#)
     [Disabling DNS Lookup](#)
    * [Login MOTD Banner](#)
     [Configuring an interface](#)
       [Configuring SVI IP for remote access](#)
   [Viewing running configuration](#)
   [Saving configuration](#)
   [Resetting configuration](#)
 [COMPUTER](#computer)

- [ICA0013 Fundamentals Of Networking](#ica0013-fundamentals-of-networking)
  - [Index](#index)
  - [SWITCH/ROUTER](#switchrouter)
    - [Connecting to a switch/router using console port](#connecting-to-a-switchrouter-using-console-port)
      - [Setting up physical connection](#setting-up-physical-connection)
      - [Using PuTTY/TeraTerm to connect to a switch/router](#using-puttyteraterm-to-connect-to-a-switchrouter)
    - [Viewing switch/router info](#viewing-switchrouter-info)
  - [COMPUTER](#computer)
  
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
```

## COMPUTER
