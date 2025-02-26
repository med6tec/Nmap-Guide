# Mastering Network Scanning: A Practical Guide to Nmap
Network scanning is the process of discovering devices and services on a computer network. It plays a crucial role in network security and management, enabling administrators to identify vulnerabilities and ensure proper configurations. This process involves sending packets to a range of IP addresses and analyzing the responses, which can help determine the status of hosts, ports, and services on a network.

## Types of Network Scanning

* Port Scanning: Identifies open ports and the services running on devices. For example, scanning ports 80 and 443 may reveal if a web server is active.
* Vulnerability Scanning: Detects security weaknesses, such as outdated software or misconfigured services.
* Network Mapping: Creates a visual representation of devices connected to a network, showing relationships and connectivity.

## Nmap
Nmap (Network Mapper) is an open-source tool used for network discovery and security auditing. It is versatile and supports a wide range of features, including host discovery, service enumeration, and OS fingerprinting.

## Why Use Nmap?
1. Flexibility: Nmap supports multiple scanning techniques tailored to different use cases.
2. Customizability: Includes a scripting engine (NSE) to automate tasks and identify vulnerabilities.

3. Cross-Platform: Available for Linux, Windows, and macOS, with both command-line and GUI options (Zenmap).

## Common Nmap Flags and Their Roles:
1. TCP SYN Scan: A stealthy scan by sending SYN packets without completing the TCP handshake.
 _(If the port is open, the target responds with a SYN-ACK. If closed, it responds with an RST.)_

``` ruby 
nmap -sS <target>
```
_Use Case: Detect open ports without being easily logged by the target._

2. TCP Connect Scan: Completes a full TCP handshake for every port it scans.

More detectable than SYN scan since it completes the connection.

``` ruby 
nmap -sT <target>
```
_Use Case: Use when you don’t have administrative privileges (since SYN scans require raw socket access)._

3. UDP Scan: Sends UDP packets to detect open ports.

An open port responds (if the service uses UDP). Closed ports often return ICMP “Port Unreachable.”

``` ruby 
nmap -sU <target>
```

_Use Case: Useful for finding UDP-based services like DNS (port 53) or SNMP (port 161)._

4. TCP ACK Scan: Sends TCP ACK packets to probe firewall rules.

Helps determine if ports are filtered (stateful firewalls block ACK packets for unopened connections).

``` ruby 
nmap -sA <target>
```

_Use Case: Determine if a firewall is in place or which ports are being filtered._

5. SCTP INIT Scan: Probes SCTP (Stream Control Transmission Protocol) ports by sending INIT packets.

``` ruby 
nmap -sY <target>
```
_Use Case: Useful for scanning telecommunication networks or SCTP-enabled servers._

6. FIN Scan: Sends TCP FIN packets to scan ports.

If a port is closed, it replies with an RST. Open ports generally remain silent.

``` ruby 
nmap -sF <target>
```
_Use Case: Evade basic firewall rules since many firewalls don’t log FIN packets._

7. Ping Scan: Checks if a host is alive without scanning ports.

Methods include:

ICMP Echo Requests.

ARP requests (local network).

TCP SYN to port 443 or 80 (if ICMP is blocked).

``` ruby 
nmap -sn <target>
```

_Use Case: Quickly identify live hosts in a subnet._

8. Service Version Detection: Identifies the version of services running on open ports by probing them.

``` ruby 
nmap -sV <target>
```

_Use Case: Gain detailed insights into running services, which can help identify vulnerabilities._


