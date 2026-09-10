# Network Security & Protocol Analysis Labs

Practical network-security work spanning packet analysis, man-in-the-middle attacks, TCP/IP attack mechanics, trust abuse, HTTPS defenses, and Linux packet filtering.

> **Academic context:** Computer Science / Cybersecurity engineering coursework at Amar Telidji University, Laghouat (2025-2026).

## What this repository demonstrates

- Demonstrated ARP spoofing/MITM positioning and analyzed the result in Wireshark.
- Built an HTTPS impersonation scenario and demonstrated the role of trusted Certification Authorities in server authentication.
- Performed TCP/IP security exercises in isolated Docker networks: SYN flooding and SYN-cookie defense, forged RST injection, session hijacking, and a controlled reverse-shell extension.
- Recreated the trust assumptions behind the classic Mitnick attack in a controlled lab environment.
- Implemented packet-filtering concepts with Linux kernel modules, Netfilter hooks, and iptables.
- Completed Wireshark protocol-analysis labs for UDP, TCP, and HTTP.

## Tools & technologies

`Wireshark` · `Kali Linux` · `Docker` · `Scapy` · `C raw sockets` · `arpspoof` · `OpenSSL` · `iptables` · `Netfilter` · `Linux kernel modules` · `TCP/IP`

## Included academic work

| # | Lab | Portfolio write-up |
|---:|---|---|
| 1 | ARP Spoofing / MITM | [`docs/01-arp-spoofing-mitm.md`](docs/01-arp-spoofing-mitm.md) |
| 2 | ARP Spoofing, HTTPS & CA Defense | [`docs/02-arp-spoofing-https-ca-defense.md`](docs/02-arp-spoofing-https-ca-defense.md) |
| 3 | TCP/IP Attacks | [`docs/03-tcp-ip-attacks.md`](docs/03-tcp-ip-attacks.md) |
| 4 | Mitnick Attack Simulation | [`docs/04-mitnick-attack-simulation.md`](docs/04-mitnick-attack-simulation.md) |
| 5 | Netfilter Kernel Firewall | [`docs/05-netfilter-kernel-firewall.md`](docs/05-netfilter-kernel-firewall.md) |
| 6 | Wireshark UDP Analysis | [`docs/06-wireshark-udp-analysis.md`](docs/06-wireshark-udp-analysis.md) |
| 7 | Wireshark TCP Analysis | [`docs/07-wireshark-tcp-analysis.md`](docs/07-wireshark-tcp-analysis.md) |
| 8 | Wireshark HTTP Analysis | [`docs/08-wireshark-http-analysis.md`](docs/08-wireshark-http-analysis.md) |

## Evidence policy

This repository uses only the academic reports and evidence actually supplied for the portfolio. The original reports contain screenshots/tool output; no additional screenshots, scripts, packet captures, or results have been fabricated or claimed. The GitHub write-ups focus on the technical work that can be supported directly by those reports.

## Responsible use

All attack techniques were performed in controlled academic environments. Use them only on systems you own or have explicit authorization to test.
