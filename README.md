# Useful Everyday Linux Commands I oft forget.

## wget
wget is a useful utility for downloading files from any website.

```
wget https://someurl.com/somefile.zip
```

## netstat

Lists the various in-use ports and the process using it
```
netstat -anp | grep tcp | grep LISTEN
```
## Find

Find a file or directory by name
```
find . -name [file]
```
Finds users.txt file under /home and deep
```
find /home -name users.txt
```
Finds users.txt file ignoring case under /home and deep
```
find /home -iname users.txt
```
Finds all Java files from current dir and deep
```
find . -type f -name "*.java"
```
Finds all files
```
find / -type f -perm 0777
```
Finds all executable files
```
find / -perm /a=x
```
Finds all files that belong to bob
```
find /home -user bob
```
Finds all files that belong to the dev group
```
find /home -group dev
```
Finds all files modified in the last 10 days
```
find / -mtime 10
```
Finds all files accessed in the last 10 minutes
```
find / -amin -10
```
## grep

Find the string “stuff” in all the .txt files
```
grep -i stuff `find . -name \*.txt -print`
```
## sed

sed is used among other things to apply substitution, find or replace files content.

Changes the first occurrence in each line containing the blue word to red
```
sed 's/blue/red/' colors.txt
```
Changes the second occurrence in each line containing the blue word to red
```
sed 's/blue/red/2' colors.txt
```
Changes all the occurrences containing the blue word to red
```
sed 's/blue/red/g' colors.txt
```
Changes all the occurrences from line number 1 to 3 containing the blue word to red
```
sed '1,3 s/blue/red/g' colors.txt
```
Deletes line number 5
```
sed '5d' colors.txt
```
Deletes from line 12 to last line The sed command also supports regular expression.
```
sed '12,$d' colors.txt
```
## awk

awk is a text manipulation tool implementing a powerful scripting language.

Prints lines matching the given pattern
```
awk '/red/ {print}' colors.txt
```
Split each line in columns (whitespace as separator) and prints column 1
```
awk '{print $1,$4}' colors.txt
```
Prints from line 3 to 6 prefixed with the line number (NR)
```
and 4 awk 'NR==3, NR==6 {print NR,$0}' colors.txt
```
Prints from line 2 to end of file
```
awk 'NR > 1 {print}' colors.txt
```
## top

Order process by CPU usage
```
top -u
```
Order process by memory
```
top -o mem
```
Only shows 5 processes
```
top -n 5
```
## history

history command shows all of the last commands that have been recently used.
```
history
```
You can run any of the commands by appending exclamation (!) to the number of the command
```
! #
```
## journalctl

Show and keep open (-f) the system log, allowing you to see new messages scrolling by. The -l flag prevents truncating of long lines.
```
journalctl -f -l
```
Same as above, but only for log messages from the httpd and mariadb services.
```
journalctl -f -l -u httpd -u mariadb
```
Same as above, only for log messages that are less than 300 seconds (5 minutes) old
```
journalctl -f -l -u httpd -u mariadb --since -300
```
## scp

SCP is an acronym for Secure Copy Protocol. It is a command line utility that allows the user to securely copy files and directories between two locations usually between unix or linux systems.
```
scp [OPTIONS] [[user@]src_host:]file1 [[user@]dest_host:]file2
```

## lspci & lsusb & lsblk

lspci (in the pciutils package) lists PCI devices.

-v for loads of info
```
lspci
```
lsusb (in the usbutils package) lists USB devices
-v for loads of info
```
lsusb
```
lsblk lists Block (Storage) Devices
```
lsblk
```
## nmap

Nmap is a network scanner created by Gordon Lyon. Nmap is used to discover hosts and services on a computer network by sending packets and analyzing the responses.

-A Agressive Scan -O Detect OS
```
nmap -A -traceroute -O 0.0.0.1/24
```

## vi

vi is a screen-oriented text editor originally created for the Unix operating system.

Find ad Replace

```
:%s/^foo*/bar/gc
```

: Function
% Global
s find / replace
/^foo* find string
/bar/ replace string
gc 

## SSH

Create and setup an Public and Private RSA key.
```
ssh-keygen -t rsa

ssh-agent bash

ssh-add ~/.ssh/id_rsa
```

To use the ssh-copy-id utility, to connect to, and copy a public yer to the remote device user account that you require SSH access to.
```
ssh-copy-id username@remote_host
```

## nmcli

nmcli is a command-line tool for controlling NetworkManager and reporting network status. It can be utilized as a replacement for nm-applet or other graphical clients. nmcli is used to create, display, edit, delete, activate, and deactivate network connections, as well as control and display network device status.

The -a flag will ask you to enter the WiFi password.

```
nmcli -a device wifi connect [wifiname]
```

Get the connection name, run below nmcli command to assign static ipv4 address.

```
nmcli connection
nmcli con mod 'eth0' ipv4.address 0.0.0.0/24
nmcli con mod 'eth0' ipv4.gateway 0.0.0.0
nmcli con mod 'eth0' ipv4.method manual
nmcli con mod 'eth0' ipv4.dns '0.0.0.0'
nmcli connection down eth0
nmcli connection up eth0
ip add show eth0
nmcli -p con show 'eth0'
```


## Podman, Buildah & Quay

Download an image
```
buildah from 'name'  
```
View a download image
```
buildah images
```
View a container
```
buildah containers
```
Copy stuff into a conainer image
``` 
buildah copy name-working-container /home/1.rpm /home/1.rpm
```    
Updates and install package
```
buildah run name-working-container -- dnf update -y
buildah run name-working-container -- dnf install -y package
```
Commit conainer image
```
buildah commit name-working-container new-name
```
Login to a Container Registry (i.e. Quay.io)
```
buildah login quay.io
``` 
Push the container to a Container Regisrey (i.e Quay.io)
```
buildah push localhost/name:latest quay.io/account/name:latest
``` 
Import the container image from a custom registry (i.e. Quay.io)
```
buildah from --name=local-name quay.io/account/name:latest
```
Run a container image and connect to the shell
``` 
podman run -it quay.io/repo/imagename /bin/bash
```
Run a container image with Network Privs
``` 
podman run -it --cap-add=NET_ADMIN quay.io/repo/imagename
```
The Podman ps command is used to list creating and running containers.
```
podman ps
```
You can "inspect" a running container for metadata and details about itself.
```
podman inspect -l | grep IPAddress\":
"SecondaryIPAddresses": null,
"IPAddress": "",
```
View the container's logs:
```
podman logs --latest
```
Stop the last started container:
```
podman stop --latest
```
