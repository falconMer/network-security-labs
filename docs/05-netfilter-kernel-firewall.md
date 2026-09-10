# 05 Netfilter Kernel Firewall

> Portfolio write-up derived from the original university lab report provided by Smail Mersad. The original report contains screenshots; this GitHub edition uses only evidence and results from that report and does not invent additional assets.

**Academic context:** Amar Telidji University, Computer Science / Cybersecurity Engineering, 2025-2026.

## Objective

Understand Linux packet filtering from two levels: custom kernel-module/Netfilter hooks and administrator-defined `iptables` policies.

## Part 1 — Loadable kernel modules

A sample kernel module was compiled into a `.ko` file, inserted with `insmod`, verified with `lsmod`, removed with `rmmod`, and observed through `dmesg`. The initialization and cleanup messages confirmed that code could be dynamically loaded into and removed from the running kernel.

## Part 2 — Packet filtering with Netfilter

A custom filtering module was compiled and loaded. In the first test it intercepted and dropped UDP DNS traffic, causing a `dig` query to time out.

The filtering callback was then registered across the five major IPv4 Netfilter hook points:

- `NF_INET_PRE_ROUTING`
- `NF_INET_LOCAL_IN`
- `NF_INET_FORWARD`
- `NF_INET_LOCAL_OUT`
- `NF_INET_POST_ROUTING`

Generated traffic and kernel logs were used to observe how packets traverse those hook points.

Custom hooks were also used to block ICMP echo requests and TCP traffic to Telnet port 23 for the local host. Ping and Telnet tests failed as expected, and the drops were visible in kernel logging.

## Part 3 — Protecting the router with iptables

The router's `INPUT` and `OUTPUT` default policies were changed to `DROP`, while explicit rules permitted ICMP echo request/reply traffic. The resulting behavior matched the policy: the router could be pinged, but Telnet access was blocked.

## Part 4 — Protecting an internal network

The `FORWARD` chain default policy was set to `DROP`. Rules permitted selected outbound ICMP requests from the internal interface and corresponding replies from the external side.

Validation showed:

- outside hosts could not ping internal hosts;
- outside hosts could still ping the router itself when the local `INPUT` policy permitted it;
- internal hosts could ping outward through the specifically allowed forwarding rules.

## Tools & technologies

`Linux kernel modules` · `Netfilter` · `iptables` · `Docker` · `GCC/Make` · `dmesg` · `ICMP` · `TCP` · `UDP`

## Takeaway

The lab links firewall policy to the actual Linux packet-processing path, from custom kernel hooks through state-independent packet filtering and routed-network policy with `iptables`.
