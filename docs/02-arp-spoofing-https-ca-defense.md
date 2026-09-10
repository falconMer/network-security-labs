# 02 ARP Spoofing, HTTPS & CA Defense

[← Repository overview](../README.md) · [Original PDF report](02-arp-spoofing-https-ca-defense.pdf)

> Portfolio write-up derived from the original university lab report provided by Smail Mersad. The original report contains screenshots; this GitHub edition uses only evidence and results from that report and does not invent additional assets.

**Academic context:** Amar Telidji University, Computer Science / Cybersecurity Engineering, 2025-2026.

## Objective

Build an HTTPS service, intercept a client's connection through ARP spoofing, then demonstrate how trusted certificate validation protects the client against an impersonating server.

## Topology

The lab used three virtual machines on a private `10.10.0.0/24` network:

- Legitimate Apache HTTPS server
- Attacker / fake web server
- Client

## Tools

`Apache2` · `arpspoof` · `OpenSSL` · `Linux` · `HTTPS/TLS`

## Attack phase

The legitimate host served HTTPS content. The attacker then impersonated the legitimate server's network address and poisoned the client's ARP mapping so the client's traffic reached the attacker's Apache instance instead.

When the client connected over HTTPS during the attack, the browser displayed a severe certificate warning. Bypassing that warning exposed the fake server's page, demonstrating that encryption alone does not prove server identity when certificate trust is ignored.

## Defense phase

A Certification Authority was created with OpenSSL and used to sign the legitimate server certificate. Once the client trusted the CA and the ARP state was restored, the legitimate HTTPS service was accepted without a certificate exception.

## Takeaway

This lab connects a Layer-2 MITM attack with TLS identity verification: HTTPS provides strong protection only when the client validates that the certificate belongs to the intended server and chains to a trusted authority.
