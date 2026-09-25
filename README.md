# Week 2 – Penetration Testing & Network Reconnaissance

**Author:** Tiffany Lucia  
**Week:** 02  
**Focus:** Footprinting, Reconnaissance, Network Configuration & Network Discovery  
**Environment:** Kali Linux, VirtualBox and Zenmap  
**Date:** 25 September 2026

## Overview

Week 2 focused on applying the cybersecurity lab environment configured during Week 1 to practical reconnaissance and network discovery activities.

The work covered:
1. Footprinting and reconnaissance using Kali Linux.
2. Private lab network configuration and connectivity verification.
3. Network discovery using Zenmap/Nmap on an authorized local network.

> **Authorization:** All activities documented here were performed for educational purposes and within an authorized scope.

## Objectives

- Perform basic domain footprinting.
- Identify publicly observable domain information.
- Identify web technologies used by a website.
- Resolve a domain through DNS.
- Inspect HTTP response headers.
- Identify a detected Web Application Firewall.
- Enumerate DNS records.
- Configure and verify the cybersecurity lab network.
- Discover live hosts on an authorized local subnet.
- Document commands, observations and evidence.

# 1. Footprinting & Reconnaissance

## 1.1 WHOIS

### Command
```bash
whois networkwalks.com
```

### Purpose
WHOIS was used to obtain publicly available domain registration information.

### Observation
The output included the domain name, registrar information, registration dates, domain status information and HostGator name servers.

### Evidence
![WHOIS](evidence/01-whois-domain-registration.png)

---

## 1.2 WhatWeb

### Command
```bash
whatweb networkwalks.com
```

### Purpose
WhatWeb was used to fingerprint technologies exposed by the website.

### Observation
The result identified technologies including Apache, Bootstrap, WordPress 7.1.2, WP Download Manager 3.3.58 and HTML5. It also displayed the IP address `192.232.216.135`.

### Evidence
![WhatWeb](evidence/02-whatweb-technology-fingerprinting.png)

---

## 1.3 Nslookup

### Command
```bash
nslookup networkwalks.com
```

### Purpose
Nslookup was used to perform DNS resolution.

### Result
```text
Name: networkwalks.com
Address: 192.232.216.135
```

The screenshot shows `8.8.8.8` as the DNS server.

### Evidence
![Nslookup](evidence/03-nslookup-dns-resolution.png)

---

## 1.4 Curl

### Command
```bash
curl -I https://networkwalks.com
```

### Purpose
Curl was used to inspect HTTP response headers.

### Observation
The response returned `HTTP/2 200` and exposed HTTP response headers and WordPress-related links.

### Evidence
![Curl](evidence/04-curl-http-headers.png)

---

## 1.5 Wafw00f

### Command
```bash
wafw00f networkwalks.com
```

### Purpose
Wafw00f was used to identify whether a Web Application Firewall was detected.

### Result
The tool identified:

```text
ModSecurity (SpiderLabs)
```

### Evidence
![Wafw00f](evidence/05-wafw00f-waf-detection.png)

---

## 1.6 DNSRecon

### Command
```bash
dnsrecon -d networkwalks.com
```

### Purpose
DNSRecon was used to enumerate DNS information.

### Observation
The output included NS, MX, TXT and SRV information and reported:

```text
8 Records Found
```

### Evidence
![DNSRecon](evidence/06-dnsrecon-dns-enumeration.png)

---

# 2. Network Configuration

The private cybersecurity lab network created during Week 1 was used as the foundation for network discovery.

| Setting | Value |
|---|---|
| Network Type | NAT Network |
| Subnet | `10.0.0.0/24` |
| Kali IPv4 | `10.0.0.10/24` |
| Gateway | `10.0.0.1` |
| DNS | `8.8.8.8` |

## Connectivity Test

After configuring Kali, connectivity was tested using `ping`.

The recorded result was:

- 38 packets transmitted
- 34 packets received
- Approximately 10% packet loss

This confirmed working connectivity through the configured lab network while also documenting the observed packet loss.

# 3. Network Discovery with Zenmap

Zenmap/Nmap was used for a Ping Scan on the authorized local network.

The objectives were to:
- Identify the relevant subnet.
- Discover live hosts.
- Record IP addresses.
- Identify MAC addresses where available.
- Review the network topology.

**Important:** Final live-host IP addresses and MAC addresses should be copied directly from the final Zenmap scan evidence rather than guessed or invented.

# 4. Findings & Risk Considerations

| Finding | Evidence | Security relevance |
|---|---|---|
| Domain information exposed | WHOIS | Can contribute to an infrastructure profile |
| Web technologies identifiable | WhatWeb | May assist authorized technology review |
| IP address resolved | Nslookup/WhatWeb | Provides network-location information |
| HTTP headers visible | Curl | Can assist fingerprinting |
| WAF identifiable | Wafw00f | Reveals part of defensive architecture |
| DNS records available | DNSRecon | Can contribute to infrastructure mapping |
| Live hosts visible locally | Zenmap | Unexpected devices should be verified |

These observations do not by themselves establish confirmed vulnerabilities.

# 5. Recommendations

1. Review publicly exposed technical information regularly.
2. Keep web technologies and plugins updated.
3. Review HTTP response headers for unnecessary information exposure.
4. Review DNS records periodically.
5. Maintain and monitor WAF configurations.
6. Maintain an inventory of authorized network devices.
7. Investigate unexpected hosts discovered during authorized scans.
8. Preserve screenshots and command output as evidence.
9. Perform reconnaissance and scanning only with appropriate authorization.

# 6. Key Learning Outcomes

During Week 2 I gained practical experience with:

- Linux reconnaissance tools
- Domain footprinting
- DNS enumeration
- Web technology fingerprinting
- HTTP header analysis
- WAF identification
- Private network configuration
- Network discovery
- Zenmap/Nmap
- Cybersecurity documentation

A major lesson was that reconnaissance provides useful information before deeper security testing begins. Different tools reveal different parts of an environment, so combining their results provides a more complete picture.

# 7. Tools Used

| Tool | Main Use |
|---|---|
| Kali Linux | Cybersecurity testing environment |
| VirtualBox | Virtual lab environment |
| WHOIS | Domain registration information |
| WhatWeb | Web technology fingerprinting |
| Nslookup | DNS resolution |
| Curl | HTTP header inspection |
| Wafw00f | WAF detection |
| DNSRecon | DNS enumeration |
| Zenmap | Network discovery |

# 8. Evidence

All supplied evidence screenshots are stored in the `evidence/` folder.

- `01-whois-domain-registration.png`
- `02-whatweb-technology-fingerprinting.png`
- `03-nslookup-dns-resolution.png`
- `04-curl-http-headers.png`
- `05-wafw00f-waf-detection.png`
- `06-dnsrecon-dns-enumeration.png`

# 9. Conclusion

Week 2 allowed me to move from having a cybersecurity lab environment to actively using it for practical reconnaissance and network discovery.

I gained hands-on experience with several Kali Linux tools and learned how different tools provide different categories of information. I also continued working with network configuration and learned how Zenmap can be used for live-host discovery.

Most importantly, I learned the importance of combining technical results with proper documentation, evidence and an authorized testing scope.

## Author

**Tiffany Lucia**  
Cybersecurity & Ethical Hacking Training  
Week 2 — Penetration Testing & Network Reconnaissance


