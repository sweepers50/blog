---
title:       "DHCP"
subtitle:    ""
description: ""
date:        2018-06-04
author:      ""
image:       ""
tags:        ["tag1", "tag2"]
categories:  ["Tech" ]
---





# DHCP

- DHCP : automates the assignment of IPv4 addresses, subnet masks, gateways, and other IPv4 networking parameters.
- DHCP can allocate IP addresses for a configurable period of time, called a **lease period**.
- **lease period** : is an important DHCP setting, When the lease period expires or the DHCP server gets a DHCPRELEASE message the address is returned to the DHCP pool for reuse.
- DHCP for IPv6 (DHCPv6) provides similar services for IPv6 clients. **One important difference** is that DHCPv6 does not provide a default gateway address.



## DHCP Operation

<img src="D:\github\SOC-analysis\Network_services\Mics\DHCP_operation.PNG" style="zoom:50%;" />



1.  the client broadcasts a DHCP discover (DHCPDISCOVER) message to identify any available DHCP servers on the network.
2. A DHCP server replies with a DHCP offer (DHCPOFFER) message. The offer message contains:
   1. the IPv4 address and subnet mask to be assigned
   2. the IPv4 address of the DNS server
   3. the IPv4 address of the default gateway. 
   4. The lease offer also includes the duration of the lease.
3. The client may receive multiple DHCPOFFER messages if there is more than one DHCP server on the local network. Therefore, it must choose between them, and sends a DHCP request (DHCPREQUEST) message that identifies the explicit server and lease offer that the client is accepting.
4. If the IPv4 address requested by the client, or offered by the server, is still available, the server returns a DHCP acknowledgment (DHCPACK)
5. If the offer is no longer valid, then the selected server responds with a DHCP negative acknowledgment (DHCPNAK) message.
6.  If a DHCPNAK message is returned, then the selection process must begin again with a new DHCPDISCOVER message being transmitted.



- The DHCP server ensures that all IP addresses are unique

- DHCPv6 has a set of messages that is similar to those for DHCPv4. The DHCPv6 messages are SOLICIT, ADVERTISE, INFORMATION REQUEST, and REPLY.



## DHCP Message Format

- DHCPv4 messages are encapsulated within the UDP transport protocol.
-  DHCPv4 messages that are sent from the client use UDP source port 68 and destination port 67.

<img src="D:\github\SOC-analysis\Network_services\Mics\DHCP_format.PNG" style="zoom:80%;" />



# DNS

- The DNS consists of a hierarchy:
  1.  top-level domains (gTLD) which consist of .com, .net, .org, .gov, .edu, and numerous country-level domains, such as .br (Brazil), .es (Spain), .uk (United Kingdom), etc.
     - .com - a business or industry
     - .org - a non-profit organization
     - .au - Australia
     - .co - Colombia
  2. Domains
  3. Subdomains
  4. A host in a subdomain.
- Each element of a domain specification is sometimes called a label. The labels move from the top of the hierarchy downward from right to left. A dot (“.“) at the end of a domain name represents the root server at the top of the hierarchy.

<img src="D:\github\SOC-analysis\Network_services\Mics\DNS_Hierarchy.PNG" style="zoom:60%;" />



## DNS Lookup Process

- **Resolver** - A DNS client that sends DNS messages to obtain information about the requested domain name space.
- **Recursion** - The action taken when a DNS server is asked to query on behalf of a DNS resolver.
- **Authoritative Server** - A DNS server that responds to query messages with information stored in Resource Records (RRs) for a domain name space stored on the server.
- **Recursive Resolver** - A DNS server that recursively queries for the information asked in the DNS query.
- **FQDN** - A Fully Qualified Domain Name is the absolute name of a device within the distributed DNS database.
- **RR** - A Resource Record is a format used in DNS messages that is composed of the following fields: NAME, TYPE, CLASS, TTL, RDLENGTH, and RDATA. 
  - Types of record
    - **A** - An end device IPv4 address
    - **NS** - An authoritative name server
    - **AAAA** - An end device IPv6 address (pronounced quad-A)
    - **MX** - A mail exchange record
- **Zone** - A database that contains information about the domain name space stored on an authoritative server.



## DNS Message Format

- DNS uses UDP port 53 for DNS queries and responses.
-  **ipconfig /displaydns** command displays all of the cached DNS entries.
- DNS uses the same message format for
  - All types of client queries and server response
  - Error messages
  - The transfer of resource records between servers

![](D:\github\SOC-analysis\Network_services\Mics\dns_format.PNG)

![](D:\github\SOC-analysis\Network_services\Mics\dns_format_tb.PNG)



## The WHOIS Protocol

- WHOIS is a TCP-based protocol that is used to identify the owners of internet domains through the DNS system.
  - An internet-based WHOIS service is called **ICANN Lookup** can be used to obtain the registration record a URL.