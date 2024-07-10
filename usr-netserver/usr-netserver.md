# USR NETServer

We want to reset the unit. On the bottom row of DIP switches on the back of the unit, set switch #4 ON (down) and reboot.

Speed: 57600
netserver> list users

USERS
                                 Login      Network
User Name                       Service     Service    Status   Type
admin                           TELNET  (D) PPP    (D) INACTIVE LOGIN
                                                                MANAGE
default                         TELNET      PPP        INACTIVE NETWORK
netserver>

netserver> show user default

INFORMATION FOR USER: default
Status:                                    INACTIVE
Type:                                      NETWORK
Expiration:                                00-   -0000
Message:
Phone Number:
Alternate Phone Number:
Input Filter:
Output Filter:
Modem Group:                               all
Session Timeout                            0
Idle Timeout:                              0

PARAMETERS FOR NETWORK USERS:
Network Service                            PPP
Header Compression:                        TCPIP
MTU:                                       1514
Send Password:
Appletalk:                                 ENABLED
Appletalk Address Range:                   0 - 0
Filter Zones                               ENABLED
IP Usage:                                  ENABLED
Address Selection:                         ASSIGN
   <enter> for more... Q to quit...
Remote IP Address:                         0.0.0.0/H
IP Routing:                                NONE
Default Route Option:                      DISABLED
IP RIP Routing Protocol:                   RIPV1
IP RIP Routing Policies:
IP RIP Authentication Key:
IPX Usage:                                 ENABLED
IPX Address:                               0
IPX Routing:                               RESPOND
IPX WAN Usage:                             DISABLED
Spoofing:                                  DISABLED

PARAMETERS for NETWORK PPP USERS
Max Channels                               1
Channel Decrement Percent:                 20
Channel Expansion Percent:                 60
Expansion Algorithm:                       LINEAR
Receive ACC Map:                           ffffffff
Transmit ACC Map:                          ffffffff
Compression Algorithm:                     AUTO
Compression Reset Mode:                    AUTO
Min Compression Size:                      256

INFORMATION FOR USER: admin
Status:                                    INACTIVE
Type:                                      LOGIN
                                           MANAGE
Expiration:                                00-   -0000
Message:
Phone Number:
Alternate Phone Number:
Input Filter:
Output Filter:
Modem Group:                               all    (D)
Session Timeout                            0
Idle Timeout:                              0

PARAMETERS FOR LOGIN USERS:
Login Service:                             TELNET  (D)
TCP Port:                                  23    (D)
Terminal:                                  vt100    (D)
Login Host:                                000.000.000.000
Host Type:                                 SELECT
netserver> list network

CONFIGURED NETWORKS
Name                            Prot Int      State Type Network Address
ip                              IP   eth:1    ENA   STAT 192.168.3.2/C
IP-loopback                     IP   loopback ENA   AUTO 127.0.0.1/A

SHOW IP  NETWORK ip SETTINGS:
Interface:                                 eth:1
Network Address:                           192.168.3.2/C
Frame Type:                                ETHERNET_II
Status:                                    ENABLED
Reconfigure Needed:                        FALSE
Mask:                                      255.255.255.0
Station:                                   192.168.3.2
Broadcast Algorithm:                       1
Max Reassembly Size:                       3468
IP Routing Protocol:                       NONE
IP RIP Routing Policies:
IP RIP Authentication Key:

---------------------------------------------------------------------------------------------------

NetServer 8/16 Application Loader Is Running...

Initializing the FLASH file system.

Erasing FLASH configuration.

Uncompressing file: ns816.bin.z
Initializing decompression module.

In : 2047539 bytes
--10--20--30--40--50--60--70--80--90--100
▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒
Completed uncompressing the imag▒▒NetServer 8/16 kernel is running...
IPX/IP Dial-out networking software is Copyright (c)1985-1996,
       Network Products Corporation (Pasadena, CA) All rights reserved.
AppleTalk-compatible networking software is Copyright 1993-1995,
       Quiotix Corporation (Menlo Park, CA) All rights reserved.
TCP/IP networking software is Copyright 1988-1995,
       Epilogue Corporation, Albuquerque NM, All rights reserved.
IP routing software is Copyright 1993-1995,
       RainbowBridge Communication. Inc. Rockville MD, All rights reserved.
IPX networking software is Copyright 1994-1995,
       RouterWare Inc. Newport Beach CA, Unpublished - rights reserved
       under the Copyright Laws of the United States.
VJ TCP Header Compression software is Copyright (c) 1989, 1991, 1992, 1993,
       Regents of the University of California. All rights reserved.


Netserver, V4.0.12
    U. S. Robotics Access Corporation, Skokie Illinois
    The Intelligent Choice in Information Access

The software contained in this product is
    Copyright 1996, US Robotics Access Corporation, Skokie Illinois
    All rights reserved.


Allocated 1678336 bytes of memory for RoboExec
Starting up the Netserver system Executive...
Starting up Netserver Configuration process...

Netserver Configuration Process starting......

Netserver starting required processes......

Netserver configuring interfaces......

Netserver configuring networks......

Netserver Adding networks to LAN interfaces....

Netserver enabling networks on LAN interfaces....

Configuring Network Services.....

Starting the CLI......
Command Line Interpreter Started - Please Wait...

Configuring default Network Services (telnet and tftp.....
At 12:50:59, Facility "Configurator", Level "INFORMATION":: Netserver system configuration complete at 12/4/2018 12:50:59
netserver>_QuickNetServer
netserver>Welcome to the Netserver Quick Setup


The Netserver Quick Setup will let you set up simple configuration
for your whole system or different portions of the system.

Do you want to continue with Netserver Quick Setup? yes

 There are two ways to proceed: You can set up only the basic
configuration, which will allow you to continue with the Windows-based
Netserver Manager Plus. Or you can configure a simple configuration
for IP, IPX, and AppleTalk.

Do you want to configure only enough to use the GUI based system [yes]? no

Please answer the following questions with "yes" or "no" to
indicate which portions of the system you want to configure.
When Quick Setup displays a question it will display a default
answer in square brackets, like "[yes]". If you simply press
enter, this is the answer that will be used for you.
     Network management [yes]?
     IP [yes]?
     IPX [no]?
     AppleTalk [no]?

Quick Setup Identification information
--------------------------------------
>>> Enter the name of your system []: dialupworld-usr-netserver8
>>> Who is the system contact person []? mike@dialup.world
>>> Where is this system located []? philly

Quick Setup Management information
----------------------------------

You can set up your system to require a user to log in via the console
or leave it so that the console is always in command line mode.
>>> Do you want a log in required at the console [no]? no
>>> Do you want to be able to manage the system via SNMP [yes]? no
>>> Do you want to allow command line management via TELNET [yes]? yes

For TELNET management of the system you need to create a user name
and password to control access.
>>> What user name will be allowed to manage this system [administrator]?
>>> What password will be used for this user []? admin

>>> Do you want to set up the syslog daemon [yes]? no

>>> Would you like to set up radius accounting [yes]? no

>>> Would you like to set up radius authentication [yes]? no

Quick Setup IP information
--------------------------

The Netserver uses a network name to identify the network for
future management commands.
>>> Enter the network name of your IP network [ip]:

>>> Enter the IP address for the Netserver []: 192.168.3.20

The IP mask can be specified as a class ("A", "B", or "C"),
the number of one bits in the mask, or as an address in the format
255.x.x.x
>>> What should the mask be set to [C]?

You need to specify the framing for the IP network.
It should be either "ethernet_ii" or "snap".
>>> What is the framing for the IP network [ethernet_ii]? snap

>>>Do you want to set up a default gateway [yes]? yes

The default gateway gives the address of a router that the Netserver
will forward packets to when it has no other route to their destination.
It cannot be the same address as the IP address for the Netserver
>>> Enter the IP address of the default gateway []? 192.168.3.1

The metric or "hop count" tells the Netserver how far the default
router is from the Netserver.
>>> What metric should be applied to the default gateway [1]? 1

>>> Do you want to configure DNS for this Netserver [yes]?
>>> What is the address of the main DNS server for this Netserver []? 8.8.8.8
>>> What is the default DNS domain name for this Netserver []?
You must specify a network name, blanks are not sufficient.
>>> What is the default DNS domain name for this Netserver []? dialup.local

You can either assign each user his or her own address or you can
set aside a pool of addresses for dynamic allocation.
>>>Do you want to set up an address pool [yes]?

The address pool is a continuous range of addresses.
>>>What is the initial address in the pool []? 10.88.88.80
>>>How many addresses should be in the pool [16]?

It is possible to restrict access to the TFTP server to a specific
system or a list of systems. Quick Setup will allow you to enter
one system that is allowed or allow all systems access
>>>Do you want to allow all systems to access the TFTP server [no]?
>>>From what IP address will you allow access to your TFTP network server []? 192.168.3.49
IP setup is completed.

Would you like to review your current settings before executing [yes]? yes
Identification Information:
   System Name:                  dialupworld-usr-netserver8
   System Contact:               mike@dialup.world
   System Location:              philly
Management Information:
   Console Login:                disabled
   TELNET Management:
      User name:                 administrator
      Password:                  admin
IP Information:
   IP Network Name:              ip
   IP Network Address:           192.168.3.20
   IP Mask:                      C
   IP Frame Type:                snap
   IP Def Gateway Addr:          192.168.3.1
   IP Def Gateway Metric:        1
   DNS Server Information:
      DNS Server Address:        8.8.8.8
      DNS Server Domain Name:    dialup.local
   IP address pool:              enabled
      IP pool address:           10.88.88.80
      IP pool size:              16
   IP WAN Information:
....<enter> for more....Q to quit.....   TFTP Client Information:
      TFTP Access:               Only: 192.168.3.49

Do you want to change any answers [no]?


Do you want to actually execute these commands [yes]?
DO /./QuickSetup.cfg
netserver>
netserver>netserver>set system name "dialupworld-usr-netserver8"
netserver>set system location "philly"
netserver>set system contact "mike@dialup.world"
netserver>enable security_option remote_user_administration telnet
netserver>add user "administrator" password "admin" type login,manage
netserver>add ip network "ip" interface eth:1 address 192.168.3.20/C frame snap enable no
netserver>enable ip network "ip"
netserver>add ip defaultroute gateway 192.168.3.1 metric 1
netserver>enable ip forwarding
netserver>add dns server 8.8.8.8 preference 1
netserver>set dns domain_name "dialup.local"
netserver>set ip system initial_pool_address 10.88.88.80 pool_members 16
netserver>add tftp client 192.168.3.49
netserver>save all
Saving..... SAVE ALL
SAVE ALL  Complete
netserver>Spawned Process CFP 2b2002   /./QuickSetup.cfg Completed Successfully

set switched interface mod:1 access DIAL_IN
set switched interface mod:2 access DIAL_IN
set switched interface mod:3 access DIAL_IN
set switched interface mod:4 access DIAL_IN
set switched interface mod:5 access DIAL_IN
set switched interface mod:6 access DIAL_IN
set switched interface mod:7 access DIAL_IN
set switched interface mod:8 access DIAL_IN
enable interface mod:1
enable interface mod:2
enable interface mod:3
enable interface mod:4
enable interface mod:5
enable interface mod:6
enable interface mod:7
enable interface mod:8
add user world password dialup type network network_service ppp
set network user world address_selection assign
?enable MODEM_GROUP all
netserver>reconfigure ip network ip frame ETHERNET_II
netserver>disable interface eth:1
netserver>enable interface eth:1

save all