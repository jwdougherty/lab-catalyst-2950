# lab-catalyst-2950
Notes on configuring a catalyst 2950 for the home lab.

# [SOLVED] Trouble booting up
This particular switch gets stuck booting up. The status light flashes orange, but never turns green. The console never shows any output.
If I interupt the boot process by holding down the mode button, then the prompt loads. From the rescue prompt I am able to load the ios by:

```
flash_init
load_helper
boot
```
From the IOS
```
sw#show boot
BOOT path-lists:
Config file:          flash:/config.text
Private Config file:  flash:/private-config.text
Enable Break:         no
Manual Boot:          no
HELPER path-lists:
NVRAM/Cofig file 
      buffer size:    32768
      
```
I notice that the BOOT path-list is empty.
```
sw#dir
```
shows me the bin file Now I set the BOOT path variable with,
```
sw# boot system flash:<name-of-image>.bin
sw# reload
```
Oops, that didn't work. I needed to direct the path to flash:/
```
sw# boot system flash:/<name-of-image>.bin
sw# reload
```
Now, `show boot` lists the image in the boot path.
Power cycle confirms [SOLVED]

# Overwrite passwords
https://www.cisco.com/c/en/us/support/docs/switches/catalyst-2950-series-switches/12040-pswdrec-2900xl.html

Overwrite the current passwords that you do not know. Choose a strong password with at least one capital letter, one number, and one special character.
Note: Overwrite the passwords which are necessary. You need not overwrite all of the mentioned passwords.

```
Sw1#configure terminal

!--- To overwrite existing secret password
Sw1(config)#enable secret <new_secret_password>

!--- To overwrite existing enable password
Sw1(config)#enable password <new_enable_password>

!--- To overwrite existing vty password
Sw1(config)#line vty 0 15
Sw1(config-line)#password <new_vty_password>
Sw1(config-line)#login

!--- To overwrite existing console password
Sw1(config-line)#line con 0
Sw1(config-line)#password <new_console_password>
```
Write the running configuration to the configuration file with the write memory command.

```
Sw1#write memory
    Building configuration...
    [OK]
    Sw1#
```


# Configuring Switch
? hostname
?password-encryption
? secret
? password
?local users
?domain name
? spanning tree
?vlan
?http server
?line console password (login)
?line vty password (local login)
?ssh (there is no ssh on this switch)
? dhcp
