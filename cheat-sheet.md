# penetration-testing-useful-commands

This page is a toolbox cheatsheet to help you for penetration testing.

## Contributions are welcome!

Feel free to submit a pull request, with anything from small fixes to tools you'd like to add. If adding a new tool, **please add a brief description** that you think new penetration tester would understand.

## Table of Contents

### Infrastructure
- [HTTP Web Server](#HTTPWebServer)
- [Wi-Fi](#Wi-fi)
- [Linux](#Linux)
  - [Useful commands](#Wireshark)
  - [Shortcuts](#Wireshark)
  - [Hidden “Dot” Files](#Wireshark)
  - [Important System Files](#Important-System-Files)
  - [Important Directories](#Important-Directories)

### Tools
- [Wireshark](#Wireshark)
  - [ICMP (Internet Control Message Protocol)](#Wireshark)
  - [TCP (Transmission Control Protocol)](#Wireshark)


### HTTP Web Server

Start a HTTP Web Server:
```bash
php -S 0.0.0.0:8080 # PHP
-
python -m http.server 8080 # Python
-
npm install http-server -g # NodeJS
http-server -p 8080  # NodeJS
```
### Wi-Fi

```bash
airmon-ng # List all the available network Interfaces
airmon-ng start wlan0  # Monitor the desired network interface
airodump-ng wlan0mon # Capture the network interface traffic
airodump-ng --bssid 09:98:98:98:98:98 -c 1 --write psk wlan0mon # Capture required data from the specific network
aireplay-ng --deauth 100 -a 09:98:98:98:98:98 wlan0mon # De-authenticate the client
ls # Verify the captured handshake file
airmon-ng stop wlan0mon # Stop Wi-Fi interface monitoring
aircrack-ng -w wordlist psk*.cap # Cracking password from the captured handshake file
```

### Linux

Index number, or inode, is a number that is unique to a file in the Unix filesystem:
```bash
0x4a756a75@nixfund:/etc$ ls -i | grep sudoers
147627 sudoers
```
We can look at the whole structure after creating the parent directories with the tool tree . :
```bash
0x4a756a75@htb[/htb]$ tree .
```
#### Useful command reference and description:

```bash
man <tool> # Opens man pages for the specified tool.
<tool> -h # Prints the help page of the tool.
apropos <keyword> # Searches through man pages' descriptions for instances of a given keyword.
cat # Concatenate and print files.
whoami # Displays current username.
id # Returns users identity.
hostname # Sets or prints the name of the current host system.
uname # Prints operating system name.
pwd # Returns working directory name.
ifconfig # The ifconfig utility is used to assign or view an address to a network interface and/or configure network interface parameters.
ip # Ip is a utility to show or manipulate routing, network devices, interfaces, and tunnels.
netstat # Shows network status.
ss # Another utility to investigate sockets.
ps # Shows process status.
who # Displays who is logged in.
env # Prints environment or sets and executes a command.
lsblk # Lists block devices.
lsusb # Lists USB devices.
lsof # Lists opened files.
lspci # Lists PCI devices.
sudo # Execute command as a different user.
su # The su utility requests appropriate user credentials via PAM and switches to that user ID (the default user is the superuser). A shell is then executed.
useradd # Creates a new user or update default new user information.
userdel # Deletes a user account and related files.
usermod # Modifies a user account.
addgroup # Adds a group to the system.
delgroup # Removes a group from the system.
passwd # Changes user password.
dpkg # Install, remove and configure Debian-based packages.
apt # High-level package management command-line utility.
aptitude # Alternative to apt.
snap # Install, remove and configure snap packages.
gem # Standard package manager for Ruby.
pip # Standard package manager for Python.
git # Revision control system command-line utility.
systemctl # Command-line based service and systemd control manager.
ps # Prints a snapshot of the current processes.
journalctl # Query the systemd journal.
kill # Sends a signal to a process.
bg # Puts a process into background.
jobs # Lists all processes that are running in the background.
fg # Puts a process into the foreground.
curl # Command-line utility to transfer data from or to a server.
wget # An alternative to curl that downloads files from FTP or HTTP(s) server.
python3 -m http.server # Starts a Python3 web server on TCP port 8000.
ls # Lists directory contents.
cd # Changes the directory.
clear # Clears the terminal.
touch # Creates an empty file.
mkdir # Creates a directory.
tree # Lists the contents of a directory recursively.
mv # Move or rename files or directories.
cp # Copy files or directories.
nano # Terminal based text editor.
which # Returns the path to a file or link.
find # Searches for files in a directory hierarchy.
updatedb # Updates the locale database for existing contents on the system.
locate # Uses the locale database to find contents on the system.
more # Pager that is used to read STDOUT or files.
less # An alternative to more with more features.
head # Prints the first ten lines of STDOUT or a file.
tail # Prints the last ten lines of STDOUT or a file.
sort # Sorts the contents of STDOUT or a file.
grep # Searches for specific results that contain given patterns.
cut # Removes sections from each line of files.
tr # Replaces certain characters.
column # Command-line based utility that formats its input into multiple columns.
awk # Pattern scanning and processing language.
sed # A stream editor for filtering and transforming text.
wc # Prints newline, word, and byte counts for a given input.
chmod # Changes permission of a file or directory.
chown # Changes the owner and group of a file or directory.
```
#### Shortcuts:
```bash
[CTRL] + A # Move the cursor to the beginning of the current line.
[CTRL] + E # Move the cursor to the end of the current line.
[CTRL] + [←] / [→] # Jump at the beginning of the current/previous word.
[ALT] + B / F # Jump backward/forward one word.
[CTRL] + U # Erase everything from the current position of the cursor to the beginning of the line.
[Ctrl] + K # Erase everything from the current position of the cursor to the end of the line.
[Ctrl] + W # Erase the word preceding the cursor position.
[Ctrl] + Y # Pastes the erased text or word.
[CTRL] + C # Ends the current task/process by sending the SIGINT signal. For example, this can be a scan that is running by a tool. If we are watching the scan, we can stop it / kill this process by using this shortcut. While not configured and developed by the tool we are using. The process will be killed without asking us for confirmation.
[CTRL] + D # Close STDIN pipe that is also known as End-of-File (EOF) or End-of-Transmission.
[CTRL] + L # Clears the terminal. An alternative to this shortcut is the clear command you can type to clear our terminal.
[CTRL] + Z # Suspend the current process by sending the SIGTSTP signal.
[CTRL] + R # Search through command history for commands we typed previously that match our search patterns.
[↑] / [↓] # Go to the previous/next command in the command history.
[ALT] + [TAB] # Switch between opened applications.
[CTRL] + [+] # Zoom in.
[CTRL] + [-] # Zoom out.
```
#### Hidden “Dot” Files

```bash
[ ] .bash_history # For users of the bash shell, a file containing up to 500 of the most recent commands available for recall using the up and down arrow keys.
[ ] .bash_logout # Script that is run by the bash shell when the user logs out of the system
[ ] .bash_profile # Initialization script that is run by the bash shell upon login in order to setup variables and aliases.  When bash is started as the default login shell, it looks for the .bash_profile file in the user’s home directory; if not found, it looks for .bash_login.  If there is no .bash_login file, it then looks for a .profile file.
[ ] .bashrc # Initialization script executed whenever the bash shell is started in some way other than a login shell. It is better to put system-wide functions and aliases in /etc/bashrc, which will be presented later in the book.
[ ] .gtkrc # GTK initialization file.  GTK+ is a multi-platform toolkit for creating graphical user interfaces, used by a large number of applications.  It is the toolkit used by the GNU project's GNOME desktop.
[ ] .login # The initialization script that is run whenever a user login occurs.
[ ] .logout # The script that is automatically run whenever a user logout occurs.
[ ] .profile # Put default system-wide environment variables in /etc/profile.
[ ] .viminfo # Initialization file for the Vim text editor that is compatible with vi.
[ ] .wm_style # Specifys the default window manager if one is not specified in startx
[ ] .Xdefaults & .Xresources # Initialization files for Xterm resources for the user. Application program behavior can be changed by modifying these files.
[ ] .xinitrc # The initialization file used when running startx, which can be used to activate applications and run a particular window manager.
[ ] .xsession # This file is executed when a user logs in to an X-terminal and is used to automatically load the window manager and applications.
```

#### Important System Files

```bash
[ ] /boot/vmlinuz # The Linux kernel file.  File naming conventions may include release information
[ ] /dev/fd0 # Device file for the first floppy disk drive on the system
[ ] /dev/fd0H1440 # Device driver for the first floppy drive in high density mode, commonly invoked when formatting a floppy diskette for that density
[ ] /dev/hda # Device file for the first IDE hard drive on the system
[ ] /dev/hdc # Commonly, the IDE CDROM drive device file which often is a symbolic link called to /dev/cdrom, the real CDROM driver file.
[ ] /dev/null  # A dummy device which contains nothing.  It is sometimes useful to send output to this device to make it go away forever.
[ ] /etc/aliases # Contains aliases used by sendmail and other mail transport agents. Whenever this file is changed, the newaliases utility must be run to notify sendmail of the changes
[ ] /etc/bashrc # Contains global defaults and aliases used by the bash shell
[ ] /etc/crontab # A parent shell script to run commands periodically.  It invokes hourly, daily, weekly, and monthly scripts.
[ ] /etc/exports # Contains a list of filesystems which may be made available to other systems on the network via NFS.
[ ] /etc/fstab # The file system table contains the description of what disk devices are available at what mount points.
[ ] /etc/group # Holds information regarding security group definitions.
[ ] /etc/grub.conf # The grub boot loader configuration file
[X] /etc/hosts # Contains host names and their corresponding IP addresses used for name resolution whenever a DNS server is unavailable
[ ] /etc/hosts.allow # Contains a list of hosts allowed to access services on this computer.
[ ] /etc/hosts.deny # Contains a list of hosts forbidden to access services on this computer.
[ ] /etc/inittab # Describes how the INIT process should set up the system in various runlevels
[ ] /etc/issue # Contains the pre-login message, often overwritten by the /etc/rc.d/rc.local script in Red Hat and some other rpm-based Linux distributions
[ ] /etc/lilo.conf # The lilo boot loader configuration file
[ ] /etc/modules.conf # Holds options for configurable system modules
[ ] /etc/motd # This is the ”message of the day” file which is printed upon login. It can be overwritten by /etc/rc.d/rc.local Red Hat on startup.
[ ] /etc/mtab # Status information for currently mounted devices and partitions
[X] /etc/passwd # Contains information regarding registered system users. Passwords are typically kept in a shadow file for better security.
[ ] /etc/printcap # Holds printer setup information
[ ] /etc/profile # Contains global defaults for the bash shell
[X] /etc/resolv.conf # A list of domain name servers (DNS) used by the local machine
[ ] /etc/securetty # This file contains a list of terminals where root can login
[ ] /etc/termcap # An extensive ASCII text file defining the properties of consoles, terminals, and printers
[ ] /proc/cpuinfo # Contains CPU related information
[ ] /proc/filesystems # Holds information regarding filesystems that are currently in use
[ ] /proc/interrupts # Stores the interrupts that are currently being used
[ ] /proc/ioports # A list of the I/O addresses used by devices connected to the server
[ ] /proc/meminfo # Contains memory usage information for both physical memory and swap
[ ] /proc/modules # Lists currently loaded kernel modules
[ ] /proc/mounts  # Displays currently mounted file systems
[ ] /proc/stat # Contains various statistics about the system, such as the number of page faults since the system was last booted
[ ] /proc/swaps # Holds swap file utilization information
[ ] /proc/version # Contains Linux version information
[ ] /var/log/lastlog # Stores information about the last boot process
[ ] /var/log/messages # Contains messages produced by the syslog daemon during the boot process
[ ] /var/log/wtmp # A binary data file holding login time and duration for each user currently on the system
```

#### Important Directories

```bash
[ ] /bin # All binaries needed for the boot process and to run the system in single-user mode, including essential commands such as cd, ls, etc.
[ ] /boot # Holds files used during the boot process along with the Linux kernel itself
[ ] /dev # Contains device files for all hardware devices on the system
[X] /etc # Files used by application subsystems such as mail, the Oracle database, etc.
[ ] /etc/init.d # Contains various service startup scripts
[ ] /etc/profile.d # Holds application setup scripts run by /etc/profile upon login
[ ] /etc/rc.d # Contains subdirectories which contain run level specific scripts
[ ] /etc/rc.d/init.d # run level initialization scripts
[ ] /etc/rc.d/rc?.d # Where ‘?’ is a number corresponding to the default run level. Contains symbolic links to scripts which are in /etc/rc.d/init.d. for services to be started and stopped at the indicated run level.
[ ] /etc/skel # Holds example dot files used to populate a new user's home directory.
[ ] /etc/X11 # Contains subdirectories and configuration files for the X Window system
[X] /home # User home directories
[ ] /lib # Some shared library directories, files, and links
[X] /mnt # The typical mount point for the user-mountable devices such as floppy drives and CDROM
[ ] /proc # Virtual file system that provides system statistics.  It doesn't contain real files but provides an interface to runtime system information.
[X] /root # Home directory for the root user
[ ] /sbin # Commands used by the super user for system administrative functions
[X] /tmp # A standard repository for temporary files created by applications and users.
[ ] /usr # Directory contains subdirectories with source code, programs, libraries, documentation, etc.
[X] /usr/bin # Contains commands available to normal users
[ ] /usr/bin/X11 # X Window system  binaries
[ ] /usr/include # Holds include files used in C programs
[ ] /usr/share # Contains shared directories for man files, info files, etc.
[ ] /usr/lib # Library files searched by the linker when programs are compiled
[ ] /usr/local/bin # Common executable application files local to this system
[ ] /usr/sbin # Commands used by the super user for system administrative functions
[ ] /var # Administrative files such as log files, locks, spool files, and temporary files used by various utilities
```

### Wireshark

#### Interface

- Packet List
- Packet Details
- Packet Bytes

#### Marking Packets:

To mark a packet, either right-click it in the Packet List pane and choose Mark Packet from the pop-up or click a packet in the Packet List pane and press cTRl-M. To unmark a packet, toggle this setting off by pressing cTRl-M again. You can mark as many packets as you wish in a capture. To jump forward and backward between marked packets, press shifT-cTRl-N and shifT-cTRl-B, respectively.

#### Using Filters:

- Capture filters are specified when packets are being captured and will capture only those packets that are specified for inclusion/exclusion in the given expression.
- Display filters are applied to an existing set of captured packets in order to hide unwanted packets or show desired packets based on the speci- fied expression.

#### ARP (Address Resolution Protocol) 

- Logical addresses allow for communication among multiple networks and indirectly connected devices. 
- Physical addresses facilitate communica- tion on a single network segment for devices that are directly connected to each other with a switch.

CAM = Content Addressable Memory (CAM) table : which lists the MAC addresses of all devices plugged into each of its ports. 

The ARP resolution process uses only two packets: an ARP request and an ARP response 

![Screenshot 2022-03-03 at 1 06 07 PM](https://user-images.githubusercontent.com/96379191/156499943-d4b1ed17-1cfc-4198-b70e-50584bfe6887.png)

Operation The function of the ARP packet: either 1 (=0x0001) for a request or 2 (=0x0002) for a reply

- Broadcast: ff:ff:ff:ff:ff:ff
- Unknow Addr. : 00:00:00:00:00:00

Gratuitous ARP = where the source and destination IP are both set to the IP of the machine issuing the packet and the MAC is the broadcast address ff:ff:ff:ff:ff:ff.
- To help detect IP conflicts. When a device receives an ARP request containing a source IP that matches its own, then it knows there is an IP address conflict.
- In many cases, a device’s IP address can change. When this happens, the IP-to-MAC address mappings that hosts on the network have in their caches will be invalid.


#### IP (Internet Protocol)

##### Classes

![image](https://user-images.githubusercontent.com/96379191/156510403-26fccf83-3cf8-4afd-aff4-b866aaf2cc7d.png)
![Screenshot 2022-03-03 at 2 39 53 PM](https://user-images.githubusercontent.com/96379191/156510471-e2d92d8c-753a-43a6-9a25-f87aaafb396a.png)


##### IPv4

Ipv4 for 4.3 billion addresses.

![Screenshot 2022-03-03 at 1 52 51 PM](https://user-images.githubusercontent.com/96379191/156504788-8f489022-fc33-4cc7-bf46-175a82827e68.png)

- The Time to Live (TTL) value defines a period of time that can elapse or a maximum number of routers a packet can traverse before the packet is discarded for IPv4.
- Packet fragmentation is a feature of IP that permits reliable delivery of data across varying types of networks by splitting a data stream into smaller fragments. 
  - The fragmentation of a packet is based on the maximum transmission unit (MTU) size of the layer 2 data link protocol in use and the configuration of the devices using this layer 2 protocol. 
  - Ethernet has a default MTU of 1,500, which means that the maximum packet size that can be transmitted over an Ethernet network is 1,500 bytes (not including the 14-byte Ethernet header itself).
  - When a device prepares to transmit an IP packet, it determines whether it must fragment the packet by comparing the packet’s data size to the MTU of the network interface from which the packet will be transmitted. If the data size is greater than the MTU, the packet will be fragmented.
  - The Fragment offset value is 1480. This is indicative of the 1,500-byte MTU, minus 20 bytes for the IP header.
  - More Fragment: Flag = 0001 = Set
  - Last Fragment: FLag = 0000 = No Set

##### IPv6

- 1111:0000:2222:0000:3333:4444:5555:6666
  - OK: 1111::2222:0000:3333:4444:5555:6666 
  - NOK: 1111::2222::3333:4444:5555:6666

- 1111:0000:2222:0333:0044:0005:ffff:ffff
  - OK: 1111::2222:333:44:5:ffff:ffff

![casting_IPv6-min](https://user-images.githubusercontent.com/96379191/156509787-e9d77e9c-a2e3-47c9-9e18-7f4324dd191b.jpg)


#### ICMP (Internet Control Message Protocol)

![Screenshot 2022-03-01 at 10 21 58 PM](https://user-images.githubusercontent.com/96379191/156186345-ac9c9825-5341-47b9-93de-f5974422f45c.png)

The type field is located at the very beginning of a packet, which puts it at offset 0:
```bash
icmp[0] == 3 # Represent destination unreachable (type 3) messages
icmp[0] == 8 || icmp[0] == 0 # Represent an echo request (type 8)
icmp[0:2] == 0x0301 # Captures all ICMP destination-unreachable, host-unreachable packets, identified by type 3, code 1.
```

#### TCP (Transmission Control Protocol)

![Screenshot 2022-03-01 at 10 22 45 PM](https://user-images.githubusercontent.com/96379191/156186431-c1520d64-4c2c-4255-a461-27e9239fac11.png)

TCP packet are located at offset 13
```bash
tcp[13] & 32 == 32 # TCP packets with the URG flag set
tcp[13] & 16 == 16 # TCP packets with the ACK flag set
tcp[13] & 8 == 8 # TCP packets with the PSH flag set
tcp[13] & 4 == 4 # TCP packets with the RST flag set
tcp[13] & 2 == 2 # TCP packets with the SYN flag set
tcp[13] & 1 == 1 # TCP packets with the FIN flag set 
tcp[13] == 18 # TCP SYN-ACK packets
```

#### Viewing Endpoint Statistics

Open the Wireshark’s Endpoints window (Statistics > Endpoints)

#### Viewing Network Conversations

Open the Wireshark Conversations window (Statistics > Conversations)

#### Protocol hierarchy statistics

Open the Protocol Hierarchy Statistics window, by choosing Statistics > Protocol Hierarchy. The Protocol Hierarchy Statistics window gives you a snapshot of
the type of activity occurring on a network such as 100 percent is Ethernet traffic, 99.7 percent is IPv4, 98 percent is TCP, and 13.5 percent is HTTP from web browsing.

#### WHOIS

- https://whois.arin.net/ui/
- https://www.robtex.com/

#### Using a Custom hosts File

Choose Edit > Preferences > Name Resolution and select Only use the profile “hosts” file. The file’s name should simply be hosts. No extension

- Windows: <USERPROFILE>\Application Data\Wireshark\hosts
- OS X: /Users/<username>/.wireshark/hosts
- Linux: /home/<username>/.wireshark/hosts

![Screenshot 2022-03-02 at 4 41 04 PM](https://user-images.githubusercontent.com/96379191/156326015-097be447-4437-447c-b730-a262afb2dcb5.png)
![Screenshot 2022-03-02 at 4 41 07 PM](https://user-images.githubusercontent.com/96379191/156326049-9958d432-6980-4a5a-b007-003d3a31ffb8.png)

