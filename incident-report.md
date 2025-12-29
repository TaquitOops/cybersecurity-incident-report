# Cybersecurity Incident Report  
**Network Traffic Analysis**

---

## Part 1: Problem Summary

During the analysis of a network traffic capture file (tcpdump), multiple outbound DNS queries were observed from a web browser to the domain **yummyrecipesforme.com** using the **UDP protocol on port 53**. Each DNS query attempt was followed by an **ICMP Destination Unreachable – Port Unreachable** response, indicating that the destination host was not accepting traffic on port 53.

As a result, DNS name resolution failed, preventing users from accessing the website.

**Impact:**  
Service unavailability for end users due to the inability to resolve the domain name.

---

## Part 2: Analysis and Probable Cause

The incident occurred around **1:24 p.m.** and was identified after users reported receiving error messages when attempting to access the website. Packet analysis using tcpdump revealed a consistent pattern: valid DNS queries (including standard query flags and record type **A**) followed immediately by ICMP error messages indicating that port 53 was unreachable.

This pattern suggests that the issue is not client-side, but rather related to the DNS service or network path.

### Probable Causes (Prioritized)
1. **DNS service is down or not listening on UDP port 53** (high likelihood).
2. **Firewall or ACL blocking UDP port 53 traffic** (medium likelihood).
3. **Denial-of-Service (DoS) attack or recent misconfiguration** affecting the DNS server (medium to low likelihood).

---

## Recommended Next Steps
- Verify the operational status of the DNS service and associated processes.
- Review firewall and ACL rules affecting UDP port 53.
- Test DNS resolution from an external network using tools such as `dig` or `nslookup`.
- Review system and network logs for abnormal traffic patterns or spikes.

---

## Preventive Mitigation
- Implement continuous DNS monitoring and ICMP alerting.
- Configure redundant or secondary DNS servers for high availability.
- Apply version-controlled firewall rule management and change reviews.

---

**Disclaimer:**  
This report is based on a simulated academic exercise and does not represent a real-world incident.
