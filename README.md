# Network Security & Protocol Analysis Labs

Practical network security work spanning packet analysis, man-in-the-middle attacks, TCP/IP attack techniques, trust abuse, HTTPS defenses, and Linux packet filtering.

> **Academic context:** Completed as part of Computer Science / Cybersecurity engineering coursework at Amar Telidji University, Laghouat (2025-2026). This repository is intended as a technical portfolio of controlled university lab work.

## What this repository demonstrates

- Demonstrated ARP spoofing and man-in-the-middle positioning, then analyzed the resulting traffic in Wireshark.
- Built an HTTPS interception scenario and showed how trusted Certification Authorities protect server identity.
- Performed TCP/IP attack labs in isolated Docker environments, including SYN-flood and spoofing-oriented exercises.
- Recreated the trust assumptions behind the Mitnick attack in a controlled lab environment.
- Implemented Linux packet-filtering concepts with loadable kernel modules and Netfilter hooks.
- Completed Wireshark protocol analysis labs for UDP, TCP, and HTTP.

## Tools & technologies

`Wireshark` · `Kali Linux` · `Docker` · `Docker Compose` · `arpspoof` · `OpenSSL` · `iptables` · `Netfilter` · `Linux kernel modules` · `TCP/IP`

## Included lab reports

| # | Lab | Report |
|---:|---|---|
| 1 | 01 Arp Spoofing Mitm | [`docs/01-arp-spoofing-mitm.md`](docs/01-arp-spoofing-mitm.md) |
| 2 | 02 Arp Spoofing Https Ca Defense | [`docs/02-arp-spoofing-https-ca-defense.md`](docs/02-arp-spoofing-https-ca-defense.md) |
| 3 | 03 Tcp Ip Attacks | [`docs/03-tcp-ip-attacks.md`](docs/03-tcp-ip-attacks.md) |
| 4 | 04 Mitnick Attack Simulation | [`docs/04-mitnick-attack-simulation.md`](docs/04-mitnick-attack-simulation.md) |
| 5 | 05 Netfilter Kernel Firewall | [`docs/05-netfilter-kernel-firewall.md`](docs/05-netfilter-kernel-firewall.md) |
| 6 | 06 Wireshark Udp Analysis | [`docs/06-wireshark-udp-analysis.md`](docs/06-wireshark-udp-analysis.md) |
| 7 | 07 Wireshark Tcp Analysis | [`docs/07-wireshark-tcp-analysis.md`](docs/07-wireshark-tcp-analysis.md) |
| 8 | 08 Wireshark Http Analysis | [`docs/08-wireshark-http-analysis.md`](docs/08-wireshark-http-analysis.md) |

## Repository structure

```text
.
├── README.md
├── docs/        # GitHub text editions of the academic lab reports
└── src/         # Add original code/configs/scripts here when available
```

## Notes

The reports document the work actually completed in the university labs. For GitHub portability, the reports are included as searchable Markdown text editions; the original PDF screenshots and figures are not embedded in these conversions. The `src/` directory is intentionally left as a place to add original source code, configuration files, packet captures, notebooks, or scripts where those artifacts are available. No source code has been fabricated from the reports.

## Responsible use

Security techniques in this repository were performed in controlled academic environments. Use attack and exploitation techniques only on systems you own or have explicit authorization to test.
