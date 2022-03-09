# Useful Everyday Linux Commands - I oft forget.

Good (free) book : https://debian-handbook.info/

## wget

wget is a useful utility for downloading files from any website. If installation is required, simply
sudo dnf -y install wget
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

sed is used among other things to apply substitution,  find or replace  files content.

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

## lspci & lsusb

lspci (in the pciutils package) lists PCI devices.
```
lspci -v
```
lsusb (in the usbutils package) lists USB devices
```
lsusb -v
```

## nmap

Nmap is a network scanner created by Gordon Lyon. Nmap is used to discover hosts and services on a computer network by sending packets and analyzing the responses.

-A Agressive Scan -O Detect OS
```
nmap -A -traceroute -O 0.0.0.1/24
```
