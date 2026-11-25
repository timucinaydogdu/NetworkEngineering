# NetworkEngineering

A structured, hands-on learning repository for **network and data center engineering**. Each topic has concise study notes followed by a lab report: the real command run on macOS and its (redacted) output.

The scope grows with my learning roadmap: **networking, server systems, virtualization, data center, network security, monitoring and automation**. Module A (networking fundamentals) is the first block.

> Study notes are written in Turkish. Commands, outputs and technical terms are universal.

## Repository layout

```text
NetworkEngineering/
├── README.md
└── A_NetworkEngineeringBasics/
    ├── A1_NetworkBasics.md
    ├── A2_NetworkTypes.md
    ├── A3_CableAndDevices.md
    ├── A4_ProtocolsAndPorts.md
    ├── A5_TCP-IP-AndOSI_Models.md
    ├── A6_BinarySystemAndIPv4.md
    ├── A7_SubnettingCalculations.md
    ├── A8_VLSM-Calculations.md
    ├── A9_IPv6.md
    ├── A10_RoutingBasics.md
    └── LabCodes.md
```

## Module A: Networking basics

| # | Note | Topics | Status |
|---|---|---|---|
| A1 | [Network basics](A_NetworkEngineeringBasics/A1_NetworkBasics.md) | Client/server, host, IP, MAC, port, socket, protocol, packet, frame | Published |
| A2 | [Network types](A_NetworkEngineeringBasics/A2_NetworkTypes.md) | Bandwidth, latency, throughput, PAN/LAN/WLAN/MAN/WAN/SAN/VPN/Cloud, client-server vs P2P | Published |
| A3 | [Cables and devices](A_NetworkEngineeringBasics/A3_CableAndDevices.md) | CAT5e/6/6a, DAC, multi-mode and single-mode fiber, hub, switch, router, modem, access point, MAC learning | Published |
| A4 | [Protocols and ports](A_NetworkEngineeringBasics/A4_ProtocolsAndPorts.md) | Common ports, encrypted vs plaintext services, TCP vs UDP, ARP | Published |
| A5 | [OSI and TCP/IP models](A_NetworkEngineeringBasics/A5_TCP-IP-AndOSI_Models.md) | Seven layers, encapsulation, bottom-up troubleshooting | Published |
| A6 | [Binary system and IPv4](A_NetworkEngineeringBasics/A6_BinarySystemAndIPv4.md) | Binary conversion, 32-bit addresses, masks, CIDR, private and special ranges | In progress |
| A7 | [Subnetting calculations](A_NetworkEngineeringBasics/A7_SubnettingCalculations.md) | Network, broadcast and host range, block-size method | In progress |
| A8 | [VLSM](A_NetworkEngineeringBasics/A8_VLSM-Calculations.md) | Variable-length subnet planning, overlap checks | In progress |
| A9 | [IPv6](A_NetworkEngineeringBasics/A9_IPv6.md) | Address notation, /64, address types, NDP | In progress |
| A10 | [Routing basics](A_NetworkEngineeringBasics/A10_RoutingBasics.md) | Routing table, default route, longest prefix match | In progress |

## Lab approach

Every note ends with a **Lab-Raporu** section. The same commands are collected in [`LabCodes.md`](A_NetworkEngineeringBasics/LabCodes.md), organised by lesson.

| Goal | Command |
|---|---|
| Interface, IP, MAC | `ifconfig en0` |
| Neighbours on the LAN | `arp -a` |
| Reachability | `ping -c 4 <host>` |
| Path to a host | `traceroute -n 1.1.1.1` |
| Port check | `nc -zv -w 3 example.com 443` |
| Listening ports | `sudo lsof -iTCP -sTCP:LISTEN -n -P` |
| Default gateway | `netstat -rn \| grep default` |
| ARP capture | `sudo tcpdump -i en0 -n arp -c 4` |
| DNS and HTTP | `dig +short example.com`, `curl -sI https://example.com` |

**Conventions**

- Environment: macOS, Wi-Fi interface `en0`.
- MAC addresses and other identifiers in outputs are masked (`xx`).
- Labs run in a personal network. No employer or customer data is used.

## Roadmap

- Next in networking: switching and VLANs, DNS/DHCP/NAT, ACLs, CCNA-style labs.
- Then: Linux server administration, virtualization and storage, network security, monitoring and automation.

This repository supports my path toward data center systems administration and auditing. See my [profile](https://github.com/timucinaydogdu) for the full roadmap.