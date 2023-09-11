# Cisco IAD2400

How to setup a Cisco IAD2432 as a VoIP gateway.

We have a Cisco IAD2432-24FXS, which is an old router that happens to have an RJ-21 port on the back that supports 24 analog phone lines. These routers can be found for $30 used which makes them incredibly inexpensive compared to ATAs with a high capacity of lines.

As the model name implies, we will get 24 different lines off of this device.

## Factory Reset
Before we configure our lines we should completely wipe the existing config and start from a blank slate.

To factory reset we must open a console session with the IAD. While booting, keep sending `BREAK` in the console until you see a `rommon 1 >` prompt.

Now we need to change the register we boot from to load defaults and then reboot,

```
rommon 1 >confreg 0x2142
rommon 2 >reset
```

After router restarts, you should be prompted to run initial setup. Do so, or if you accidentally exit out of it you can invoke it with `setup`, 

```
Router#setup


         --- System Configuration Dialog ---

Continue with configuration dialog? [yes/no]: yes

At any point you may enter a question mark '?' for help.
Use ctrl-c to abort configuration dialog at any prompt.
Default settings are in square brackets '[]'.


Basic management setup configures only enough connectivity
for management of the system, extended setup will ask you
to configure each interface on the system

Would you like to enter basic management setup? [yes/no]: no

First, would you like to see the current interface summary? [yes]: no

Configuring global parameters:

  Enter host name [Router]: iad2432-24fxs

  The enable secret is a password used to protect access to
  privileged EXEC and configuration modes. This password, after
  entered, becomes encrypted in the configuration.
  Enter enable secret: cisco123

  The enable password is used when you do not specify an
  enable secret password, with some older software versions, and
  some boot images.
  Enter enable password: cisco123
% Please choose a password that is different from the enable secret
  Enter enable password: cisco321

  The virtual terminal password is used to protect
  access to the router over a network interface.
  Enter virtual terminal password: cisco123
  Configure SNMP Network Management? [no]: yes
    Community string [public]:
  Configure LAT? [yes]:
Configure IP? [yes]:
    Configure RIP routing? [no]:
  Configure bridging? [no]:
Configure CLNS? [no]:

Configuring interface parameters:

Do you want to configure FastEthernet0/0  interface? [no]: yes
  Operate in full-duplex mode? [no]: yes
  Configure IP on this interface? [no]: yes
    IP address for this interface: 192.168.3.200
    Subnet mask for this interface [255.255.255.0] :
    Class C network is 192.168.3.0, 24 subnet bits; mask is /24
  Configure LAT on this interface? [no]:

Do you want to configure FastEthernet0/1  interface? [no]: yes
  Operate in full-duplex mode? [no]: yes
  Configure IP on this interface? [no]: yes
    IP address for this interface: 192.168.3.201
    Subnet mask for this interface [255.255.255.0] :
    Class C network is 192.168.3.0, 24 subnet bits; mask is /24
  Configure LAT on this interface? [no]:

Would you like to go through AutoSecure configuration? [yes]: no
AutoSecure dialog can be started later using "auto secure" CLI

The following configuration command script was created:

hostname iad2432-24fxs
enable secret 5 $1$T4HJ$VdHWbnYjfc6jE02Q14gEm0
enable password cisco321
line vty 0 4
password cisco123
snmp-server community public
!
ip routing
no bridge 1
no clns routing
!
interface FastEthernet0/0
no shutdown
full-duplex
ip address 192.168.3.200 255.255.255.0
no lat enabled
!
interface FastEthernet0/1
no shutdown
full-duplex
ip address 192.168.3.201 255.255.255.0
no lat enabled
dialer-list 1 protocol ip permit
!
end


[0] Go to the IOS command prompt without saving this config.
[1] Return back to the setup without saving this config.
[2] Save this configuration to nvram and exit.

Enter your selection [2]:
 Warning: MD5 encryption will be deprecated soon. Please move to SHA256 encryption.
% 192.168.3.0 overlaps with FastEthernet0/0
Building configuration...
```

Afterwards, we can set the register back, save our changes, and then restart,

```
conf t
config-register 0x2102
exit
wr
reload
```

## SIP Configuration
This thread was helpful in getting the SIP configuration working, https://www.voip-info.org/forum/threads/using-a-cisco-iad2400-with-freepbx.22980/

Let's bring down the networking interfaces as apparantly the config breaks if these are up when configuring,
```
en
conf t
interface fa 0/0
shut
interface fa 0/1
shut
```

Next, we can set the default gateway,

```
ip route 0.0.0.0 0.0.0.0 192.168.3.1
```

Now, we will shutoff VoIP services and then add our 24 SIP peers,

```
dial-peer voice 2401 pots
destination-pattern 8927221
port 2/0
authentication u 8927221 p lamepassword
dial-peer voice 2402 pots
destination-pattern 8927222
port 2/1
authentication u 8927222 p lamepassword
dial-peer voice 2403 pots
destination-pattern 8927223
port 2/2
authentication u 8927223 p lamepassword
dial-peer voice 2404 pots
destination-pattern 8927224
port 2/3
authentication u 8927224 p lamepassword
dial-peer voice 2405 pots
destination-pattern 8927225
port 2/4
authentication u 8927225 p lamepassword
dial-peer voice 2406 pots
destination-pattern 8927226
port 2/5
authentication u 8927226 p lamepassword
dial-peer voice 2407 pots
destination-pattern 8927227
port 2/6
authentication u 8927227 p lamepassword
dial-peer voice 2408 pots
destination-pattern 8927228
port 2/7
authentication u 8927228 p lamepassword
dial-peer voice 2409 pots
destination-pattern 8927229
port 2/8
authentication u 8927229 p lamepassword
dial-peer voice 2410 pots
destination-pattern 8927230
port 2/9
authentication u 8927230 p lamepassword
dial-peer voice 2411 pots
destination-pattern 8927231
port 2/10
authentication u 8927231 p lamepassword
dial-peer voice 2412 pots
destination-pattern 8927232
port 2/11
authentication u 8927232 p lamepassword

dial-peer voice 2413 pots
destination-pattern 8927233
port 2/12
authentication u 8927233 p lamepassword
dial-peer voice 2414 pots
destination-pattern 8927234
port 2/13
authentication u 8927234 p lamepassword
dial-peer voice 2415 pots
destination-pattern 8927235
port 2/14
authentication u 8927235 p lamepassword
dial-peer voice 2416 pots
destination-pattern 8927236
port 2/15
authentication u 8927236 p lamepassword
dial-peer voice 2417 pots
destination-pattern 8927237
port 2/16
authentication u 8927237 p lamepassword
dial-peer voice 2418 pots
destination-pattern 8927238
port 2/17
authentication u 8927238 p lamepassword
dial-peer voice 2419 pots
destination-pattern 8927239
port 2/18
authentication u 8927239 p lamepassword
dial-peer voice 2420 pots
destination-pattern 8927240
port 2/19
authentication u 8927240 p lamepassword
dial-peer voice 2421 pots
destination-pattern 8927241
port 2/20
authentication u 8927241 p lamepassword
dial-peer voice 2422 pots
destination-pattern 8927242
port 2/21
authentication u 8927242 p lamepassword
dial-peer voice 2423 pots
destination-pattern 8927243
port 2/22
authentication u 8927243 p lamepassword
dial-peer voice 2424 pots
destination-pattern 8927244
port 2/23
authentication u 8927244 p lamepassword
```

Next, some default dialing rules (even though we don't really need these as we won't be making outgoing calls),

```
dial-peer voice 10 voip
description Extension Dial
destination-pattern ...T
session protocol sipv2
session target sip-server
codec g711ulaw

dial-peer voice 20 voip
description 10 Digit Dial
destination-pattern ..........T
session protocol sipv2
session target sip-server
codec g711ulaw

dial-peer voice 30 voip
description 11 Digit Dial
destination-pattern ...........
session protocol sipv2
session target sip-server
codec g711ulaw

dial-peer voice 100 voip
description Catch All Dial
destination-pattern .T
session protocol sipv2
session target sip-server
codec g711ulaw
```

Then we can specify our SIP server/port and restart SIP,

```
sip-ua
registrar ipv4:192.168.5.228:16555 expires 3600
sip-server ipv4:192.168.5.228:16555
protocol mode ipv4

voice service voip
sip
no call service stop
```

Finally, bring the ethernet interfaces back up, save, and restart the system,

```
inter fa 0/0
no shut
inter fa 0/1
no shut

exit
exit
write
reload
```

## Asterisk Config
We just need to make sure we have the SIP peers defined in `sip.conf` provided you are using `chan_sip`,

```
[8927221](lines)
defaultuser = 8927221
secret = lamepassword
authid = 8927221
callerid = "Dialup.World" <8927221> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927222](lines)
defaultuser = 8927222
secret = lamepassword
authid = 8927222
callerid = "Dialup.World" <8927222> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927223](lines)
defaultuser = 8927223
secret = lamepassword
authid = 8927223
callerid = "Dialup.World" <8927223> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927224](lines)
defaultuser = 8927224
secret = lamepassword
authid = 8927224
callerid = "Dialup.World" <8927224> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927225](lines)
defaultuser = 8927225
secret = lamepassword
authid = 8927225
callerid = "Dialup.World" <8927225> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927226](lines)
defaultuser = 8927226
secret = lamepassword
authid = 8927226
callerid = "Dialup.World" <8927226> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927227](lines)
defaultuser = 8927227
secret = lamepassword
authid = 8927227
callerid = "Dialup.World" <8927227> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927228](lines)
defaultuser = 8927228
secret = lamepassword
authid = 8927228
callerid = "Dialup.World" <8927228> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927229](lines)
defaultuser = 8927229
secret = lamepassword
authid = 8927229
callerid = "Dialup.World" <8927229> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927230](lines)
defaultuser = 8927230
secret = lamepassword
authid = 8927230
callerid = "Dialup.World" <8927230> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927231](lines)
defaultuser = 8927231
secret = lamepassword
authid = 8927231
callerid = "Dialup.World" <8927231> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927232](lines)
defaultuser = 8927232
secret = lamepassword
authid = 8927232
callerid = "Dialup.World" <8927232> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927233](lines)
defaultuser = 8927233
secret = lamepassword
authid = 8927233
callerid = "Dialup.World" <8927233> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927234](lines)
defaultuser = 8927234
secret = lamepassword
authid = 8927234
callerid = "Dialup.World" <8927234> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927235](lines)
defaultuser = 8927235
secret = lamepassword
authid = 8927235
callerid = "Dialup.World" <8927235> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927236](lines)
defaultuser = 8927236
secret = lamepassword
authid = 8927236
callerid = "Dialup.World" <8927236> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927237](lines)
defaultuser = 8927237
secret = lamepassword
authid = 8927237
callerid = "Dialup.World" <8927237> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927238](lines)
defaultuser = 8927238
secret = lamepassword
authid = 8927238
callerid = "Dialup.World" <8927238> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927239](lines)
defaultuser = 8927239
secret = lamepassword
authid = 8927239
callerid = "Dialup.World" <8927239> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927240](lines)
defaultuser = 8927240
secret = lamepassword
authid = 8927240
callerid = "Dialup.World" <8927240> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927241](lines)
defaultuser = 8927241
secret = lamepassword
authid = 8927241
callerid = "Dialup.World" <8927241> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927242](lines)
defaultuser = 8927242
secret = lamepassword
authid = 8927242
callerid = "Dialup.World" <8927242> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927243](lines)
defaultuser = 8927243
secret = lamepassword
authid = 8927243
callerid = "Dialup.World" <8927243> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw

[8927244](lines)
defaultuser = 8927244
secret = lamepassword
authid = 8927244
callerid = "Dialup.World" <8927244> ; change the CNAM and caller ID of your line here
context = from-internal ; context in the dialplan in which this user originates a call
directmedia = yes
call-limit = 1
disallow = all
allow = ulaw
```

## RJ21 Cable

To make an easy RJ21 hydra cable, I ordered a cable with bare ends on one side and a male RJ21 connector on the other.

The pairs can be split off to their own RJ11 cables as follows:

| Color | Pin (Tip) | Pin (Ring) | Color |
|-------|-----------|------------|-------|
| White/Blue | 26 | 1 | Blue/White |
| White/Orange | 27 | 2 | Orange/White |
| White/Green | 28 | 3 | Green/White |
| White/Brown | 29 | 4 | Brown/White |
| White/Slate | 30 | 5 | Slate/White |
| Red/Blue | 31 | 6 | Blue/Red |
| Red/Orange | 32 | 7 | Orange/Red |
| Red/Green | 33 | 8 | Green/Red |
| Red/Brown | 34 | 9 | Brown/Red |
| Red/Slate | 35 | 10 | Slate/Red |
| Black/Blue | 36 | 11 | Blue/Black |
| Black/Orange | 37 | 12 | Orange/Black |
| Black/Green | 38 | 13 | Green/Black |
| Black/Brown | 39 | 14 | Brown/Black |
| Black/Slate | 40 | 15 | Slate/Black |
| Yellow/Blue | 41 | 16 | Blue/Yellow |
| Yellow/Orange | 42 | 17 | Orange/Yellow |
| Yellow/Green | 43 | 18 | Green/Yellow |
| Yellow/Brown | 44 | 19 | Brown/Yellow |
| Yellow/Slate | 45 | 20 | Slate/Yellow |
| Violet/Blue | 46 | 21 | Blue/Violet |
| Violet/Orange | 47 | 22 | Orange/Violet |
| Violet/Green | 48 | 23 | Green/Violet |
| Violet/Brown | 49 | 24 | Brown/Violet |
| Violet/Slate | 50 | 25 | Slate/Violet |
