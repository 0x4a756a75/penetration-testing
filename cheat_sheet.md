# penetration-testing-useful-commands

This page is a toolbox cheatsheet to help you for penetration testing.

## Contributions are welcome! 

Feel free to submit a pull request, with anything from small fixes to tools you'd like to add. If adding a new tool, **please add a brief description** that you think new penetration tester would understand.

## Table of Contents

### Setup

- [Organization](#Organization)
- [Notes](#Notes)

### Infrastructure
- [VM Vs Containers](#HTTPWebServer)
- [HTTP Web Server](#HTTPWebServer)
- [Wi-Fi](#Wi-fi)
- [Service Provider and Key Generation](#Wi-fi)
- [Windows](#Windows)
- [Linux](#Linux)
  - [Useful commands](#Wireshark)
  - [Shortcuts](#Wireshark)
  - [Hidden “Dot” Files](#Wireshark)
  - [Important System Files](#Important-System-Files)
  - [Important Directories](#Important-Directories)
- [SMB](#smb)


### Organization

#### Structure #1
.
└── Penetration-Testing
	│
	├── Pre-Engagement
	│       └── ...
    ├── Network-Pentesting
	│       ├── Linux
	│       │   ├── Information-Gathering
	│		│   │   └── ...
	│       │   ├── Vulnerability-Assessment
    │       │   │	└── ...
    │       │	└── ...
    │       │    	└── ...
    │		├── Windows
    │ 		│   ├── Information-Gathering
    │		│   │   └── ...
    │		│   └── ...
    │       └── ...
    ├── WebApp-Pentesting
	│       └── ...
    ├── Social-Engineering
	│       └── ...
    ├── .......
	│       └── ...
    ├── Reporting
    │   └── ...
	└── Results
	    └── ...

#### Structure #2

.
└── Penetration-Testing
	│
	├── Pre-Engagement
	│       └── ...
    ├── Network-Pentesting
	│       ├── Linux
	│       │   ├── Information-Gathering
	│		│   │   └── ...
	│       │   ├── Vulnerability-Assessment
    │       │   │	└── ...
    │       │	└── ...
    │       │    	└── ...
    │		├── Windows
    │ 		│   ├── Information-Gathering
    │		│   │   └── ...
    │		│   └── ...
    │       └── ...
    ├── WebApp-Pentesting
	│       └── ...
    ├── Social-Engineering
	│       └── ...
    ├── .......
	│       └── ...
    ├── Reporting
    │   └── ...
	└── Results
	    └── ...
      
### Notes 

#### Note-taking

- CherryTree
- https://www.notion.so/
- https://obsidian.md/

#### Results

- GhostWriter
- Pwndoc

#### Logging

Logging is essential for both documentation and our protection. If third parties attack the company during our penetration test and damage occurs, we can prove that the damage did not result from our activities. For this, we can use the tools script and date. Date can be used to display the exact date and time of each command in our command line. With the help of script, every command and the subsequent result is saved in a background file. To display the date and time, we can replace the PS1 variable in our .bashrc file with the following content.
```
PS1="\[\033[1;32m\]\342\224\200\$([[ \$(/opt/vpnbash.sh) == *\"10.\"* ]] && echo \"[\[\033[1;34m\]\$(/opt/vpnserver.sh)\[\033[1;32m\]]\342\224\200[\[\033[1;37m\]\$(/opt/vpnbash.sh)\[\033[1;32m\]]\342\224\200\")[\[\033[1;37m\]\u\[\033[01;32m\]@\[\033[01;34m\]\h\[\033[1;32m\]]\342\224\200[\[\033[1;37m\]\w\[\033[1;32m\]]\n\[\033[1;32m\]\342\224\224\342\224\200\342\224\200\342\225\274 [\[\e[01;33m\]$(date +%D-%r)\[\e[01;32m\]]\\$ \[\e[0m\]"
-----
script 03-21-2021-0200pm-exploitation.log # Start the tool script and log in the .log file
```

#### Screenshots + Recording

- Flameshot
- Peek - Create GIFs that record all the required actions for us.


### VM Vs Containers

![Screenshot 2022-03-04 at 11 00 37 AM](https://user-images.githubusercontent.com/96379191/156691222-865791ba-c4d2-43a7-9e69-2c902c7fd52f.png)

- Virtual Machine	
   - Contain applications and the complete operating system	
   - A hypervisor such as VMware ESXi provides virtualization
   - Multiple VMs run in isolation from each other on a physical server
   	
- Containers
   - Contain applications and only the necessary operating system components such as libraries and binaries
   - The operating system with the container engine provides its own virtualization
   - Several containers run isolated from each other on one operating system


Orchestration systems = These systems distribute the containers over the existing hardware based on predefined rules and monitor them.
   - Apache Mesos
   - Google Kubernetes

- Docker Engine = Docker Engine is the main component of container virtualization. The software provides the interface between host resources and running containers. Any system that has Docker Engine installed can use Docker containers.
- Vagrant 
   - Vagrant is a tool that can create, configure and manage virtual machines or virtual machine environments. 
   - The VMs are not created and configured manually but are described in code in a Vagrantfile.
   - It tries to simplify the software configuration management of virtualization in order to increase development productivity.

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

### Service Provider and Key Generation

- https://www.vultr.com/products/cloud-compute/
- https://www.linode.com/pricing/
- https://www.digitalocean.com/pricing
- https://onehostcloud.hosting/

File to SSH => /home/user/.ssh/id_rsa or /root/.ssh/id_rsa
```
vim id_rsa
chmod 600 id_rsa
ssh user@10.10.10.10 -i id_rsa # If we can read the /root/.ssh/ directory and can read the id_rsa file, we can copy it to our machine and use the -i flag to log in with it
```

Generation Private and Public keys for SSH:
```
ssh-keygen -t rsa -b 4096 -f vps-ssh
------
ssh-keygen -f key # New key with ssh-keygen and the -f flag to specify the output file:
```

Adding a New Sudo User:
```
adduser test
usermod -aG sudo test
su - test
```

Adding Public SSH Key to VPS:
```
[test@VPS ~]$ mkdir ~/.ssh
[test@VPS ~]$ echo '<vps-ssh.pub>' > ~/.ssh/authorized_keys
[test@VPS ~]$ chmod 600 ~/.ssh/authorized_keys
```

Using SSH Keys:
```
0x4a756a75@htb[/htb]$ ssh root@<vps-ip-address> -i vps-ssh-test
[test@VPS ~]$ 
```

#### VPS Hardening

- Install Fail2ban
- Working only with SSH keys
- Reduce Idle timeout interval
- Disable passwords
- Disable x11 forwarding
- Use a different port
- Limit users' SSH access
- Disable root logins
- Use SSH proto 2
- Enable 2FA Authentication for SSH

Update the System:
```
sudo apt update -y && sudo apt full-upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y
```

#### SSH Hardening: 

/etc/ssh/sshd_config File for SSH Hardening
```
sudo apt install fail2ban -y # Once we have installed it, we can find the configuration file at /etc/fail2ban/jail.conf
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.conf.bak # Make a backup
```
/etc/fail2ban/jail.conf File
```
# [sshd]
enabled = true
bantime = 4w # set the ban time to four weeks
maxretry = 3 # allow a maximum of 3 attempts.
```
Editing OpenSSH Config
```
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
sudo vim /etc/ssh/sshd_config
---------
LogLevel VERBOSE # Gives the verbosity level that is used when logging messages from SSH daemon.
PermitRootLogin no # Specifies whether root can log in using SSH.
MaxAuthTries 3 # Specifies the maximum number of authentication attempts permitted per connection.
MaxSessions 5 # Specifies the maximum number of open shell, login, or subsystem (e.g., SFTP) sessions allowed per network connection.
HostbasedAuthentication no # Specifies whether rhosts or /etc/hosts.equiv authentication together with successful public key client host authentication is allowed (host-based authentication).
PermitEmptyPasswords no	When password authentication is allowed, it specifies whether the server allows login to accounts with empty password strings.
ChallengeResponseAuthentication yes # Specifies whether challenge-response authentication is allowed.
UsePAM yes # Specifies if PAM modules should be used for authentification.
X11Forwarding no # Specifies whether X11 forwarding is permitted.
PrintMotd no # Specifies whether SSH daemon should print /etc/motd when a user logs in interactively.
ClientAliveInterval 600 # Sets a timeout interval in seconds, after which if no data has been received from the client, the SSH daemon will send a message through the encrypted channel to request a response from the client.
ClientAliveCountMax 0 # Sets the number of client alive messages which may be sent without SSH daemon receiving any messages back from the client.
AllowUsers <username> # This keyword can be followed by a list of user name patterns, separated by spaces. If specified, login is allowed only for user names that match one of the patterns.
Protocol 2 # Specifies the usage of the newer protocol with is more secure.
AuthenticationMethods publickey,keyboard-interactive # Specifies the authentication methods that must be successfully completed for a user to be granted access.
PasswordAuthentication no # Specifies whether password authentication is allowed.
```
#### 2FA Authentication

Installing Google-Authenticator PAM Module
```
sudo apt install libpam-google-authenticator -y
google-authenticator
```
2FA PAM Configuration:
```
sudo cp /etc/pam.d/sshd /etc/pam.d/sshd.bak
sudo vim /etc/pam.d/sshd
```
/etc/pam.d/sshd => We comment out the "@include common-auth" line by putting a "#" in front of it. Besides, we add two new lines at the end of the file, as follows:
```
#@include common-auth 
auth required pam_google_authenticator.so
auth required pam_permit.so
```
/etc/ssh/sshd_config => Next, we need to adjust our settings in our SSH daemon to allow this authentication method. In this configuration file (/etc/ssh/sshd_config), we need to add two new lines at the end of the file as follows:
```
AuthenticationMethods publickey,keyboard-interactive
PasswordAuthentication no
# Finally, we have to restart the SSH server to apply the new configurations and settings.
```
Restart SSH Server
```
sudo service ssh restart # 
```
2FA SSH Login => Now we can test this and try to login to the SSH server with our SSH key and check if everything works as intended.
```
ssh cry0l1t3@VPS -i cry0l1t3
```
SCP Syntax => Finally, we can transfer all our resources, scripts, notes, and other components to the VPS using SCP.
```
scp -i <ssh-private-key> -r <directory to transfer> <username>@<IP/FQDN>:<path>
```
Resources Transfer
```
scp -i ~/.ssh/cry0l1t3 -r ~/Pentesting cry0l1t3@VPS:~/
```

### Windows

- Windows Subsystem for Linux (WSL) is an excellent example of this. It allows for Linux operating systems to run alongside our Windows install. This can help us by giving us a space to run tools developed for Linux right inside our Windows host without the need for a hypervisor program or installation of a third-party application such as VirtualBox or Docker.
- Chocolatey Package Manager is a free and open software package management solution that can manage the installation and dependencies for our software packages and scripts. 

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

- Logical Volume Manager (LVM) = LVM is a partitioning scheme mainly used in Unix and Linux environments, which provides a level of abstraction between disks, partitions, and file systems. Using LVM, it is possible to form dynamically changeable partitions, which can also extend over several disks. In this case, we will install all files in one partition.

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
----
grep # Searches for specific results that contain given patterns.
cut # Removes sections from each line of files.
tr # Replaces certain characters.
column # Command-line based utility that formats its input into multiple columns.
awk # Pattern scanning and processing language.
sed # A stream editor for filtering and transforming text.
wc # Prints newline, word, and byte counts for a given input.
----
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
#### File Descriptors

A file descriptor (FD) in Unix/Linux operating systems is an indicator of connection maintained by the kernel to perform Input/Output (I/O) operations
  - Data Stream for Input = STDIN – 0 => Input from Keyboard
  - Data Stream for Output = STDOUT – 1 => Display after input from keyboard
  - Data Stream for Output that relates to an error occurring = STDERR – 2 => Such as "Permission Denied"

```
find /etc/ -name shadow 2>/dev/null # This way, we redirect the resulting errors to the "null device," which discards all data
find /etc/ -name shadow 2>/dev/null > results.txt # Redirect to a file with the name results.txt that will only contain standard output without the standard errors. When we use the greater-than sign (>) to redirect our STDOUT, a new file is automatically created if it does not already exist.
find /etc/ -name shadow 2> stderr.txt 1> stdout.txt # Redirect STDOUT and STDERR to Separate Files
cat < stdout.txt # Redirect STDIN
find /etc/ -name passwd >> stdout.txt 2>/dev/null # Redirect STDOUT and Append to a File
find /etc/ -name *.conf 2>/dev/null | grep systemd # Any errors are redirected to the "null device" (/dev/null). Using grep, we filter out the results and specify that only the lines containing the pattern "systemd" should be displayed.
find /etc/ -name *.conf 2>/dev/null | grep systemd | wc -l # we will use the tool called wc, which should count the total number of obtained results.

```


#### SMB
```	
smbclient -N -L \\\\10.129.42.253 # The -L flag specifies that we want to retrieve a list of available shares on the remote host, while -N suppresses the password prompt.
smbclient \\\\10.129.42.253\\users # This reveals the non-default share users. Let us attempt to connect as the guest user.
smb: \bob\> get passwords.txt # Download text

```
Robots.txt = It is common for websites to contain a robots.txt file, whose purpose is to instruct search engine web crawlers such as Googlebot which resources can and cannot be accessed for indexing. The robots.txt file can provide valuable information such as the location of private files and admin pages. In this case, we see that the robots.txt file contains two disallowed entries.
	
#### Metasploit

```
msfconsole # Stating Metasploit
search exploit eternalblue # Search vulnerabilities
use exploit/windows/smb/ms17_010_psexec # use exploit
msf6 exploit(windows/smb/ms17_010_psexec) > set RHOSTS 10.10.10.40 # Set configuration
msf6 exploit(windows/smb/ms17_010_psexec) > check # Check if the target is vulnerable
msf6 exploit(windows/smb/ms17_010_psexec) > exploit # Exploit the vulnerability
```
