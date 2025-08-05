# cybersecurity_internship_task-1
# 🔍 Nmap Scan Report & Analysis: Port 53 Exposure

### 📅 Scan Date: Mon Aug 4, 2025  
### 🧰 Nmap Version: 7.95  
### 🌐 Target Subnet: `192.168.245.0/24`  

### Tools Used:
->Nmap:For port scanning and host scanning

->Wireshark:For capturing and analyzing network traffic

### 🖥️ Summary of Detected Hosts

| IP Address        | MAC Address         | Host Status | Open Ports    | Service    |
| ----------------- | ------------------- | ----------- | ------------- | ---------- |
| `192.168.245.1`   | 00:50:56\:C0:00:08  | Up          | None          | -          |
| `192.168.245.2`   | 00:50:56\:EA\:BE:27 | Up          | `53/tcp open` | tcpwrapped |
| `192.168.245.254` | 00:50:56\:E9:28:33  | Up          | None          | -          |
| `192.168.245.131` | Not Shown           | Up          | None          | -          |


### 🚨 Analysis of Findings

✅ Host: 192.168.245.2
Port 53/tcp is open and tcpwrapped, indicating a DNS service with additional security layers (e.g., firewall, proxy, or access control).

All other ports on all other hosts are either filtered or closed.

What Does "tcpwrapped" Mean?

It typically indicates that the service is protected by a generic TCP wrapper.

Access control might be applied using tools like /etc/hosts.allow or firewalls.


### 🔐 Security Implications of Port 53 Being Open

| **Risk**               | **Description**                                                                                                     |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Zone Transfer Leak** | If TCP port 53 is misconfigured, attackers can perform DNS zone transfers (AXFR) to enumerate internal DNS records. |
| **DNS Tunneling**      | Port 53 is commonly abused to exfiltrate data over DNS queries.                                                     |
| **Reconnaissance**     | Attackers can use the DNS service to map out internal infrastructure.                                               |
| **DDoS Amplification** | If this host is also handling UDP DNS queries, it could be abused in amplification attacks.                         |


### 🛡️ Recommendations

1.Restrict TCP port 53 access to trusted IPs only.

2.If DNS is unnecessary on this machine, disable it.

3.Audit the DNS server configuration to ensure:

4.Zone transfers are disabled or restricted.

5.Logging is enabled for DNS queries.

6.DNSSEC is implemented if public-facing.

### 📌 Notes
-Only 1 out of 4 active hosts responded with an open TCP port (Port 53).

-All other ports were either filtered (firewalled) or reset (closed).

### 🧪 Command Used:
```bash
/usr/lib/nmap/nmap --privileged -sS -sV -oN scanned_subnet.txt 192.168.245.0/24
