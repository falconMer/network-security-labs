# 01 ARP Spoofing MITM

[← Repository overview](../README.md) · [Original PDF report](01-arp-spoofing-mitm.pdf)

> Portfolio write-up derived from the original university lab report provided by Smail Mersad. The original report contains screenshots; this GitHub edition uses only evidence and results from that report and does not invent additional assets.

**Academic context:** Amar Telidji University, Computer Science / Cybersecurity Engineering, 2025-2026.

## Objective

Demonstrate a Man-in-the-Middle attack using ARP spoofing and analyze the manipulated ARP traffic with Wireshark to understand the lack of authentication in ARP.

## Lab environment

The controlled lab used two Kali Linux virtual machines and a gateway on the same subnet:

- Attacker: Kali VM
- Target: Kali VM
- Gateway/router

## Tools

`dsniff / arpspoof` · `Wireshark` · `sysctl` · `Kali Linux`

## Method

IP forwarding was enabled on the attacker so intercepted packets could continue to the legitimate gateway instead of producing a simple denial of service. `arpspoof` was then used to send forged ARP replies to the target, claiming that the gateway IP belonged to the attacker's MAC address.

## Observation

Wireshark showed ARP traffic in which the sender MAC address belonged to the attacker while the sender IP represented the gateway. Wireshark flagged the conflict as a duplicate IP condition, confirming that the target's ARP mapping had been poisoned and traffic redirection was working.

## Restoration

After the test, the spoofing process was stopped, IP forwarding was disabled, and the target's ARP state was restored.

## Takeaway

The lab demonstrates how ARP's lack of authentication enables local-network traffic redirection and why monitoring and protections such as Dynamic ARP Inspection are important.
