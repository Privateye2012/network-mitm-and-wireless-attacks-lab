# Network MITM and Wireless Attacks Lab

## Overview
This repository documents a hands-on offensive cybersecurity laboratory focused on
Man-in-the-Middle (MITM) attacks, credential interception, network spoofing, and
wireless attack techniques.

The activity was developed as part of the Offensive Cybersecurity microcredential
(Week 7).

The original report was written in Portuguese, as the course was taught in Portuguese.
This repository aims to demonstrate practical attack techniques, methodology,
and technical understanding in a controlled and ethical laboratory environment.

---

## Objectives
- Perform Man-in-the-Middle attacks in a local network
- Capture credentials from insecure network services
- Analyze network traffic using packet inspection tools
- Execute ARP spoofing attacks
- Intercept HTTP, FTP, and HTTPS communications
- Perform wireless reconnaissance and attacks
- Capture and crack wireless authentication credentials
- Understand the risks of insecure network configurations

---

## Lab Environment
- Attacker: Kali Linux
- Targets: Windows and Linux systems
- Network: Isolated laboratory environment (LAN and Wireless)

### Tools Used
- arpspoof
- Wireshark
- Ettercap
- mitmproxy
- Cain & Abel
- airmon-ng
- airodump-ng
- aireplay-ng
- aircrack-ng
- reaver
- macchanger

---

## Man-in-the-Middle Attacks (LAN)

### HTTP Credential Capture (ARP Spoofing + Wireshark)
- Identified victim and gateway IP addresses
- Enabled IP forwarding on Kali Linux
- Performed ARP spoofing between victim and gateway
- Captured HTTP traffic using Wireshark
- Extracted cleartext credentials from HTTP POST requests

Example command:
sudo arpspoof -i eth0 -t <victim-ip> <gateway-ip>


---

### FTP Credential Capture (Ettercap)
- Configured an FTP server on the target system
- Performed network host discovery
- Executed ARP poisoning attack using Ettercap
- Captured FTP credentials transmitted in cleartext

Credentials were successfully intercepted during login attempts.

---

### HTTPS Credential Interception (mitmproxy)
- Installed and executed mitmproxy on Kali Linux
- Configured the victim system to use a manual proxy
- Installed the mitmproxy CA certificate on the victim
- Intercepted HTTPS POST requests
- Extracted credentials from encrypted traffic

This demonstrates how HTTPS can be compromised when trust is misconfigured.

---

### Credential Capture with Cain & Abel
- Installed and configured Cain & Abel on Windows
- Enabled sniffer and ARP poisoning
- Performed network scanning
- Captured FTP credentials during authentication attempts

---

## Wireless Attacks

### Wireless Reconnaissance
- Enabled monitor mode using airmon-ng
- Identified nearby wireless networks and clients
- Detected encryption types and channels

Example command:
airmon-ng start wlan0
airodump-ng wlan0mon


---

### MAC Address Spoofing
- Identified authorized MAC addresses on the target network
- Changed attacker MAC address to bypass MAC filtering

Example command:
macchanger --mac=<authorized-mac> wlan0


---

### Denial of Service (Deauthentication)
- Performed deauthentication attacks to disconnect clients
- Forced reconnections to capture authentication handshakes

Example command:
aireplay-ng -0 2 -e <ssid> wlan0mon


---

### WEP Cracking
- Captured IV packets using airodump-ng
- Injected traffic using replay attacks
- Recovered WEP key using aircrack-ng

This demonstrates the insecurity of legacy wireless encryption.

---

### WPA/WPA2 Handshake Capture and Cracking
- Captured WPA/WPA2 handshakes
- Performed dictionary attacks using wordlists
- Successfully recovered pre-shared keys

Example command:
aircrack-ng -w /usr/share/wordlists/rockyou.txt capture.cap


---

### WPS Attacks
- Identified networks with WPS enabled
- Attempted Pixie Dust attack
- Performed traditional WPS PIN brute-force with delays to avoid lockout

Example command:
reaver -i wlan0mon -b <bssid> -vv


---

## Impact Analysis
- Cleartext protocols expose credentials to interception
- ARP spoofing enables full traffic manipulation
- Improper certificate trust compromises HTTPS security
- Weak wireless encryption allows unauthorized access
- WPS significantly weakens wireless network security

---

## Ethical Considerations
- All activities were performed in a controlled laboratory environment
- No real users, credentials, or production systems were targeted
- The work was conducted strictly for academic and educational purposes


- No sensitive information is included in this repository
- The PDF reflects the original academic submission
- This repository demonstrates attack techniques to improve defensive awareness
