![Screenshot 2022-03-05 at 8 49 04 PM](https://user-images.githubusercontent.com/96379191/156889170-8c74f4a0-03de-4338-94c1-94f6ff173e43.png)


- Ethernet (IEEE 802.3)
- Bluetooth (IEEE 802.15)
- WLAN (IEEE 802.11)

https://www.subnet-calculator.com/cidr.php

![netmask](https://user-images.githubusercontent.com/96379191/156889213-b7cd441b-34ec-4ff5-a0b9-09d84f98ddc3.jpg)

48-bit (6 octets) Media Access Control (MAC) 
- The first half (3 bytes / 24 bit) is the so-called Organization Unique Identifier (OUI)
- The last half of the MAC address is called the Individual Address Part or Network Interface Controller (NIC)

The last two bits in the first octet can play another essential role = Unicast (0) or Multicast (1) or Broadcast (all bits at 1)
The second last bit in the first octet identifies whether it is a global OUI, defined by the IEEE, or a locally administrated MAC address.

| Features | IPv4 | IPv4 |
| --- | --- | --- |
|Bit length |32-bit |128 bit |
|OSI layer | Network Layer | Network Layer |
|Adressing range | ~ 4.3 billion | ~ 340 undecillion |
|Representation | Binary | Hexadecimal |
|Prefix notation | 10.10.10.0/24 | fe80::dd80:b1a9:6687:2d3b/64 |
|Dynamic addressing | DHCP | SLAAC / DHCPv6 |
|IPsec | Optional | Mandatory |

An IPv6 address consists of two parts:

Network Prefix (network part)
Interface Identifier also called Suffix (host part)

![external-content duckduckgo](https://user-images.githubusercontent.com/96379191/156889562-079c9c92-cc53-4331-b204-4986b3934c6f.png)

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

#### Shell

- Reverse shell	= Initiates a connection back to a "listener" on our attack box.
```
nc -lvnp 1234 # The first step is to start a netcat listener on a port of our choosing
------
-l # Listen mode, to wait for a connection to connect to us.
-v # Verbose mode, so that we know when we receive a connection.
-n # Disable DNS resolution and only connect from/to IPs, to speed up the connection.
-p # 1234	Port number netcat is listening on, and the reverse connection should be sent to.
------
# Now that we have a netcat listener waiting for a connection, we can execute the reverse shell command that connects to us.


```
- Bind shell = "Binds" to a specific port on the target host and waits for a connection from our attack box.
- Web shell = Runs operating system commands via the web browser, typically not interactive or semi-interactive. It can also be used to run single commands (i.e., leveraging a file upload vulnerability and uploading a PHP script to run a single command.
```
default webroots for common web servers:
------
Apache # /var/www/html/
Nginx # /usr/local/nginx/html/
IIS # c:\inetpub\wwwroot\
XAMPP # C:\xampp\htdocs\
```
#### Ports

- https://web.mit.edu/rhel-doc/4/RH-DOCS/rhel-sg-en-4/ch-ports.html
- https://packetlife.net/media/library/23/common-ports.pdf

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

![Screenshot 2022-03-03 at 2 44 42 PM](https://user-images.githubusercontent.com/96379191/156511292-18809627-c640-46df-9d14-55a925355820.png)
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

![Screenshot 2022-03-02 at 4 41 04 PM](https://user-images.githubusercontent.com/96379191/156326015-097be447-4437-447c-b730-a262afb2dcb5.png)
![Screenshot 2022-03-02 at 4 41 07 PM](https://user-images.githubusercontent.com/96379191/156326049-9958d432-6980-4a5a-b007-003d3a31ffb8.png)

- Windows: <USERPROFILE>\Application Data\Wireshark\hosts
- OS X: /Users/<username>/.wireshark/hosts
- Linux: /home/<username>/.wireshark/hosts
