# FOOTPRINTING-RECONNAISSANCE-ATTACKS-WITH-MULTIPLE-KALI-TOOLS
Footprinting &amp; Network Scanning Phases 
W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS

| Field | Details |
|---|---|
| **Pentester Name** | Julius De Jesus |
| **Program/Batch** | B084-Networkwalks |
| **Date** | 13 November 2026 |
| **Modules Completed** | W2-PM1 (Multiple Kali Tools); W2-PM5 (Zenmap Scanning) |
| **Client/Target** | 1. Networkwalks (written permission secured)<br>2. My own local LAN |
| **Permission secured from client?** | Yes |
| **Phases covered** | Phase 1: Reconnaissance & Footprinting<br>Phase 2: Scanning & Network Discovery<br>Phases 3–5: In Progress |



## 1. Liability Disclaimer

I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.

## 2. Introduction

This report covers footprinting the networkwalks.com domain using multiple Kali Linux tools (W2-PM1) and scanning my own local network with Zenmap (W2-PM5). One module covers the footprinting phase and the other covers the scanning phase, so together they show how an attacker moves from gathering public information to mapping live hosts on a network. It is the Week 2 part of my ongoing internship program at Networkwalks.
All commands were run in Kali Linux (footprinting). Every step below includes the exact command used, the result I observed, a screenshot as evidence, and a short note on why the finding matters from an attacker's point of view.

## 3. Tools Used
The table below lists each tool used in this report and its purpose.
| Tools | Purpose |
|---|---|
| **Kali Linux** | Operating Systems used for reconnaissance activities |
| **WHOIS** | Find domain registration details (owner, dates, name servers). |
| **whatweb** | Fingerprint web technologies (server, CMS, plugins, IP). |
| **nslookup** | Resolve the domain name to its IP address using DNS. |
| **curl -l** | Read the HTTP response headers of the website. | 
| **wafw00f** | Detect whether a Web Application Firewall protects the site. |
| **dnsrecon** | Enumerate all DNS records (NS, MX, SPF, TXT, SRV). | 

## 4. Activities Performed

### 4.1 Footprinting & Reconnaissance

I performed reconnaissance against the networkwalks.com domain using six Kali Linux tools: WHOIS, WhatWeb, Nslookup, Curl, Wafw00f and DNSRecon. Each tool was used to collect a different type of information about the target.

First, I used WHOIS to obtain publicly available domain registration information and identify the domain’s name servers. The results provided information about the domain registration and hosting infrastructure.

I then used WhatWeb to identify technologies used by the website. The results identified WordPress 7.1.4 and WP Download Manager 3.3.76, along with other information exposed by the website.

Using Nslookup, I resolved the domain name to its IP address. The provided result identified 192.232.216.135.

I used Curl with the -I option to inspect the HTTP response headers. This provided additional information about the web application and exposed the WordPress REST API endpoint /wp-json/.

Next, I used Wafw00f to determine whether a Web Application Firewall was protecting the website. The result identified ModSecurity (SpiderLabs).

Finally, I used DNSRecon to enumerate DNS records. The results provided information relating to name servers, mail servers, SPF/TXT records, service records and DNS software information.

## 4.2 Network Scanning with Zenmap

For the second activity, I used Zenmap to perform network discovery on my local network. The practical required me to identify my local IP address and subnet, discover live hosts, identify their IP and MAC addresses, and generate a network topology.
I first used the Windows ipconfig command to identify my local IP address and LAN subnet. I then entered the subnet into Zenmap and selected Ping Scan to identify active hosts.
The example results provided in the practical identified 14 live hosts:
•	192.168.100.1<img width="889" height="716" alt="zenmap topology" src="https://github.com/user-attachments/assets/3d9f2a9f-5b28-4ef5-b8f0-5983370f439a" />


The example results also included four MAC addresses.
After completing the scan, I opened the Topology section in Zenmap, enabled the legend and saved the network topology in PDF format as required by the practical task.
Note: The actual subnet, number of hosts and addresses should be replaced with the results from my own network when submitting the report.

## Risk Analysis / Impact

Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.
| # | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
|---|---|---|---|---|
| 1 | Web technology information is visible | WhatWeb identified WordPress and WP Download Manager | Technology and version details may help someone decide what further security checks to conduct | Medium |
| 2 | The server IP address is identifiable | Nslookup resolved the domain to `192.232.216.135` | The address gives additional information about where the web service is hosted | Low |
| 3 | HTTP technical information is available | Curl returned response headers and showed the `/wp-json/` endpoint | This information may assist with technology fingerprinting and further enumeration | Low |
| 4 | WAF technology is identifiable | Wafw00f identified ModSecurity (SpiderLabs) | Identifying the WAF provides information about the site’s security setup | Low |
| 5 | DNS infrastructure information is available | DNSRecon returned DNS, mail and service-related records | These records can help build a broader picture of the organization’s infrastructure | Medium |
| 6 | Live devices were visible on the local network | The practical’s example results listed a live host at `192.168.100.1` | Network discovery can help identify devices that should be checked and accounted for | Medium |

Risk level key:  ● Critical  ● Medium  ● Low

The risks above are observations from the footprinting and scanning exercises, not confirmed vulnerabilities.

The practical exercises primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed as part of these two modules.

Therefore, the presence of information such as a software version, IP address or DNS record does not by itself mean that the system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.

## Recommendations
Based on the observations from these activities, I recommend the following security improvements:
1.	Review publicly exposed technology information
Organizations should regularly review what information about their web technologies, CMS and plugins is publicly visible.
2.	Keep software updated
CMS platforms, plugins and other web technologies should be regularly updated and reviewed against current security advisories.
3.	Review HTTP headers
HTTP response headers should be reviewed to determine whether unnecessary technical information is being exposed.
4.	Review DNS records regularly
DNS records should be checked periodically to ensure that only required information and services are publicly exposed.
5.	Properly configure and monitor the WAF
Keep the WAF (ModSecurity) enabled and tuned, since it already blocks naive attacks.
6.	Perform regular internal network discovery
Organizations should periodically scan their own networks to identify active devices.
7.	Investigate unknown devices
Any unexpected device discovered during network scanning should be investigated and verified.
8.	Maintain network documentation
Network topology and device information should be documented and updated regularly.
9.	Perform security testing with authorization
Reconnaissance and scanning should only be performed against systems and networks where appropriate authorization has been provided.

## Conclusion
During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical activities covering footprinting, reconnaissance and network scanning.

In the footprinting activity, I used six Kali Linux tools to collect information about the target domain. I learned how WHOIS can provide domain information, WhatWeb can identify web technologies, Nslookup can resolve domain names, Curl can inspect HTTP headers, Wafw00f can identify a WAF, and DNSRecon can provide additional DNS information.

In the network scanning activity, I used Zenmap to identify my local network configuration and discover active hosts. I also collected IP and MAC address information and created a network topology.

The exercises showed me that information gathering is an important part of cybersecurity. Even before attempting to exploit a system, a security professional can learn a significant amount about an environment by carefully analyzing publicly available information and network responses.
I also learned that technical findings should be documented clearly. A good cybersecurity report should explain what was performed, what was discovered, what the observation means, what risk it may create, and what can be done to reduce that risk.
Finally, I learned that reconnaissance and scanning must always be performed within an authorized scope. These activities were completed as part of the assigned educational cybersecurity lab.

## Evidences Collected

<img width="698" height="414" alt="curl results" src="https://github.com/user-attachments/assets/78281879-fa8b-4769-92cd-3f6bc134b659" />
<img width="910" height="493" alt="dnsrecon results" src="https://github.com/user-attachments/assets/b203aecc-3c9a-476f-ab45-963500cf75bf" />
<img width="694" height="313" alt="nslookup results" src="https://github.com/user-attachments/assets/7652add9-6286-4217-87a3-78725e327c78" />
<img width="710" height="473" alt="wafw00f" src="https://github.com/user-attachments/assets/863c055a-c84f-43d7-9884-eb085dbdc78d" />
<img width="694" height="366" alt="whatweb results" src="https://github.com/user-attachments/assets/7acf0383-1059-4bff-80b9-47b18eebcce2" />
<img width="702" height="626" alt="whois result" src="https://github.com/user-attachments/assets/f8eff2f3-d93e-4678-9e63-c6e347a24bb4" />









