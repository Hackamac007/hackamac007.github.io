---
layout: post
title: Automotive Hacking
subtitle: Overview and Notes
cover-img: /assets/img/path.jpg
tags: [Automotive, Hacking, Security]
---

#### Background on SNMP

The Simple Network Management Protocol (SNMP) is part of the Internet Protocol Suite that is designed to manage computers and network devices. Cisco describes it as "an application layer protocol that facilitates the exchange of information between network devices".
SNMP is a stateless, datagram oriented protocol. It involves one or more administrative computers called managers. These managers monitor and manage a group of computers. Each of the managed computers has an agent installed that communicates with the manager.

The SNMP protocol communicates on UDP port 161. The communication takes place with protocol data units or PDU's. These PDU's are of seven (7) types. 

```
GetRequest  
SetRequest  
GetNextRequest  
GetBulkRequest  
Response  
Trap  
InformRequest 
```

Steps-
* Get SNMP IP from Wireshark 
* Use snmpcheck -t IP

**Cracking SNMP community strings( if not set to "public")**

	kali > onesixtyone 192.168.1.102 -c /usr/share/doc/onesixtyone/dict.txt  

#### Zero Day :[NSA Exploit in CISCO ASA]( https://www.hackers-arise.com/post/2016/08/22/the-extrabacon-zero-day-exploit-on-cisco-asa-firewalls)

According to Cisco, this EXTRABACON exploit enables  attackers within the network and with the SNMP community string to execute code remotely on their firewalls. In essence, the appliance designed to protect our network is compromised making the entire network unsafe. Like so many other pieces of remote code execution malware, EXTRABACON takes advantage of a buffer overflow in the code of the affected device

This exploit requires;
1. SNMP be enabled on the device
2. Knowledge of the community string in any version of SNMP (v1,v2,v3)
3. an attack with IPv4 packets only
4. Access to a system residing on the interface to the firewall

Note : The EXTRABACON exploit is a python script that you can [download here](https://github.com/blahdidbert/extrabacon).

**Using Extrabacon:**
		
	kali > ./extrabacon info -t 192.168.1.101 -c hackers-arise
		This will return a file that we need in exec mode of EXTRABACON. Here, I have named that file OTW
	kali > ./extrabacon_1.1.0.1.py exec -k OTW -t 192.168.1.101 -c hackers-arise --mode pass-enable
		When the exploit is successful, it will execute the shellcode on the Cisco ASA firewall, giving the attacker complete control!  

#### Defenses
Until Cisco releases a patch for this exploit, there are two best defenses you can apply for the time being-
1. Make your SNMP community string long and complex
2. Disable SNMP on the vulnerable device (no snmp-server enable)


For more info - [Reference](https://www.hackers-arise.com/post/2019/03/23/network-basics-for-hackers-simple-network-management-protocol-snmp-theory-reconnaissance)   
Car Hacking with Python - [Medium link](https://medium.com/bugbountywriteup/car-hacking-with-python-part-1-data-exfiltration-gps-and-obdii-can-bus-69bc6b101fd1)
