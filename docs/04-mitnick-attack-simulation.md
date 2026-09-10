# 04 Mitnick Attack Simulation

[← Repository overview](../README.md) · [Original PDF report](04-mitnick-attack-simulation.pdf)

> Portfolio write-up derived from the original university lab report provided by Smail Mersad. The original report contains screenshots; this GitHub edition uses only evidence and results from that report and does not invent additional assets.

**Academic context:** Amar Telidji University, Computer Science / Cybersecurity Engineering, 2025-2026.

## Environment

The classic Mitnick attack was recreated in an isolated Docker network with three roles:

- Attacker
- X-Terminal target
- Trusted Server

The X-Terminal was deliberately configured to trust the Trusted Server through `.rhosts`, reproducing the passwordless trust assumption that makes source impersonation valuable.

## Stage 1 — Preparing the trusted relationship

The target was configured so that remote commands from the Trusted Server were accepted without a password. A test `rsh` command confirmed that the trust relationship was active.

## Stage 2 — Silencing the trusted host

The exercise required the real trusted host to remain quiet so that it would not disrupt spoofed TCP state with unexpected reset packets. In the modern lab, the server container was stopped to emulate that condition. A static ARP entry was placed on the target first so the target could still send traffic toward the trusted server's address.

## Stage 3 — Spoofing the primary TCP connection

A sniff-and-spoof script sent a SYN packet that appeared to originate from the Trusted Server. It observed the target's SYN/ACK, derived the required acknowledgment state, completed the handshake, and supplied an `rsh` request.

The target then attempted to create the secondary TCP connection required by `rshd`, matching the lab's expected behavior.

## Stage 4 — Spoofing the secondary connection

A second script listened for the target's secondary SYN and replied as the Trusted Server. With both TCP connections emulated, the controlled `rsh` command was executed and a test file was created on the target, confirming success.

## Stage 5 — Persistence demonstration

The final exercise used the spoofed trusted session to modify the lab target's `.rhosts` trust configuration, after which the attacker container could open an `rsh` session without a password. This was performed only inside the intentionally vulnerable academic environment.

## Tools & concepts

`Docker` · `Scapy/Python` · `Wireshark` · `rsh/rshd` · `.rhosts` · TCP spoofing · sequence-state synchronization · trust relationships

## Takeaway

The lab demonstrates why network-address-based trust is unsafe: if a system treats source identity as sufficient authentication, an attacker who can suppress the trusted peer and reproduce the required TCP state may impersonate it. Modern cryptographic authentication protocols avoid this class of implicit trust.
