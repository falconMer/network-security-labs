# 07 Wireshark TCP Analysis

> Portfolio write-up derived from the original university lab report provided by Smail Mersad. The original report contains screenshots and a Time–Sequence graph; this GitHub edition uses only results from that report and does not invent additional assets.

**Academic context:** Amar Telidji University, Computer Science / Cybersecurity Engineering, 2025-2026.

## Objective

Inspect a real TCP transfer in Wireshark and analyze handshake state, sequence/acknowledgment numbers, segmentation, RTT, receiver windows, acknowledgments, throughput, and congestion-control behavior.

## Three-way handshake

The HTTP connection used client port `61996` to server port `80`. The report isolated the correct SYN, SYN/ACK, and ACK packets from unrelated traffic.

The client's raw initial sequence number was `440868314`. The SYN/ACK acknowledgment was `440868315`, exactly ISN + 1, and the TCP options indicated that Selective Acknowledgment (SACK) was permitted.

## Data transfer and reassembly

The first data-carrying segment contained the HTTP POST header and 603 bytes of TCP payload. The uploaded file did not fit in one segment; Wireshark reassembled the POST from multiple TCP packets into a much larger application message.

## RTT analysis

The first measured sample RTT was approximately **200.575 ms** and the second approximately **200.329 ms**. Applying the exercise's estimated-RTT formula produced approximately **200.544 ms**.

## Flow control and ACK behavior

The smallest advertised receiver window observed among the early ACKs was 63,744 bytes, so receiver-buffer exhaustion was not throttling the sender during the inspected segment group.

No packets were marked as TCP retransmissions or fast retransmissions in the inspected client-to-server trace. Early ACK behavior also demonstrated cumulative/delayed acknowledgment, with a single ACK covering more than one received segment.

## Throughput

The report measured 152,922 bytes transferred over approximately 0.760047 seconds, giving about **201,201 bytes/s** for the application-data phase.

## Congestion control

The Time–Sequence (Stevens) graph showed packet "fleets" roughly one RTT apart. Early bursts grew rapidly, consistent with **slow start**, while later growth became steadier, consistent with transition to **congestion avoidance**. No retransmission-driven collapse was visible in the analyzed graph.

## Takeaway

The lab connects TCP theory to packet-level evidence: handshake mechanics, sequence space, SACK, segmentation/reassembly, RTT estimation, advertised windows, delayed ACKs, throughput, slow start, and congestion avoidance.
