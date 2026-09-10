# 03 TCP/IP Attacks

> Portfolio write-up derived from the original university lab report provided by Smail Mersad. The original report contains screenshots; this GitHub edition uses only evidence and results from that report and does not invent additional assets.

**Academic context:** Amar Telidji University, Computer Science / Cybersecurity Engineering, 2025-2026.

## Environment

The lab used an isolated Docker Compose LAN with one attacker container and three host containers.

## Task 1 — SYN flooding

A SYN flood was used to fill the victim's half-open TCP connection queue. Both a Python/Scapy implementation and a C/raw-socket implementation were tested.

The report observed the half-open queue plateauing near 97 entries in the lab environment. Initial legitimate Telnet attempts still succeeded because Linux TCP metrics preserved "proven destination" behavior. After flushing the cached TCP metrics, the legitimate connection stalled while the queue was flooded, confirming the denial-of-service condition.

### Countermeasure

Linux SYN cookies were enabled with `net.ipv4.tcp_syncookies=1`. After the countermeasure was enabled, legitimate Telnet connections continued working during the flood because the server did not need to allocate normal half-open queue state until the final ACK arrived.

## Task 2 — TCP reset injection

An established Telnet connection was monitored in Wireshark. The source port and current sequence state were identified, then a forged TCP packet carrying the RST flag was injected with the session's expected sequence state. The endpoint accepted the forged reset and terminated the active connection.

## Task 3 — TCP session hijacking

The active session's source port, sequence number, and acknowledgment number were captured. A spoofed ACK/data packet was then injected into the synchronized TCP stream. The controlled payload created a harmless file on the target, proving that the injected data was accepted as if it came from the authenticated Telnet client.

## Task 4 — Reverse-shell extension

The same session-hijacking mechanism was extended in the isolated lab to inject a shell command that connected back to a Netcat listener on the attacker container. The listener received the connection and the exercise demonstrated why unencrypted, unauthenticated application protocols are unsafe on hostile networks.

## Tools & concepts

`Docker` · `Scapy` · `C raw sockets` · `Wireshark` · `Telnet` · `Netcat` · TCP sequence/acknowledgment state · SYN cookies

## Takeaway

The lab connects TCP state mechanics with practical attack and defense: half-open queues, RST acceptance, sequence-number synchronization, traffic injection, and SYN-cookie mitigation.
