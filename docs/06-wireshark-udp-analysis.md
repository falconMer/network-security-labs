# 06 Wireshark UDP Analysis

> Portfolio write-up derived from the original university lab report provided by Smail Mersad. The original report contains screenshots; this GitHub edition uses only evidence and results from that report and does not invent additional assets.

**Academic context:** Amar Telidji University, Computer Science / Cybersecurity Engineering, 2025-2026.

## Objective

Analyze UDP traffic in Wireshark using real DNS request/reply packets and connect the captured fields to UDP's protocol design.

## Observations

A captured DNS request used UDP. The header contained the expected four 16-bit fields:

- Source Port
- Destination Port
- Length
- Checksum

The UDP header is therefore 8 bytes long.

For the inspected packet, the UDP length was 46 bytes: 8 bytes of header plus 38 bytes of payload. The 16-bit Length field permits a maximum UDP datagram size of 65,535 bytes and therefore a maximum payload of 65,527 bytes after subtracting the header.

The port fields are 16 bits wide, giving a maximum port number of 65,535. The IP protocol number identifying UDP is 17.

## Request/reply relationship

The DNS request was sent from the client to `8.8.8.8` on destination port 53. The DNS reply reversed the source/destination port roles, confirming the request/reply pair.

## Takeaway

The lab reinforces UDP's minimal, connectionless design and shows how its small fixed header reduces protocol overhead while leaving reliability, ordering, and recovery to higher layers when needed.
