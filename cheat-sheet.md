# penetration-testing-useful-commands

This page is a toolbox cheatsheet to help you for penetration testing.

## Contributions are welcome!

Feel free to submit a pull request, with anything from small fixes to tools you'd like to add. If adding a new tool, **please add a brief description** that you think new penetration tester would understand.

## Table of Contents

### Infrastructure
- [HTTP Web Server](#HTTPWebServer)
- [Wi-Fi](#Wi-fi)
- [Linux](#Linux)

### Tools
- [Wireshark](#Wireshark)


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

List all the available network Interfaces:
```bash
airmon-ng
```
Monitor the desired network interface:
```bash
airmon-ng start wlan0 
```
Capture the network interface traffic:
```bash
airodump-ng wlan0mon
```
Capture required data from the specific network:
```bash
airodump-ng --bssid 09:98:98:98:98:98 -c 1 --write psk wlan0mon
```
De-authenticate the client:
```bash
aireplay-ng --deauth 100 -a 09:98:98:98:98:98 wlan0mon
```
Verify the captured handshake file:
```bash
ls
```
Stop Wi-Fi interface monitoring:
```bash
airmon-ng stop wlan0mon
```
Cracking password from the captured handshake file:
```bash
aircrack-ng -w wordlist psk*.cap
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
Useful command reference and description:
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
Shortcuts:
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

### Wireshark

#### Marking Packets:

To mark a packet, either right-click it in the Packet List pane and choose Mark Packet from the pop-up or click a packet in the Packet List pane and press cTRl-M. To unmark a packet, toggle this setting off by pressing cTRl-M again. You can mark as many packets as you wish in a capture. To jump forward and backward between marked packets, press shifT-cTRl-N and shifT-cTRl-B, respectively.

#### Using Filters:

• Capture filters are specified when packets are being captured and will capture only those packets that are specified for inclusion/exclusion in the given expression.
• Display filters are applied to an existing set of captured packets in order to hide unwanted packets or show desired packets based on the speci- fied expression.

#### Protocol Field Filters:

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
