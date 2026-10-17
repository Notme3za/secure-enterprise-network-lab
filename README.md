# Secure Enterprise Network Infrastructure & Monitoring Lab

A simulated enterprise network built in Cisco Packet Tracer, with a separate Linux Mint VM in VirtualBox for basic network observation.

## Project scope

- **Packet Tracer:** VLANs, router-on-a-stick routing, access control, management access, syslog, and SSH.
- **Linux Mint in VirtualBox:** checked its own route and gateway traffic with `ip`, `ping`, and `tcpdump`.
- **Boundary:** Linux Mint was kept separate from the Packet Tracer network; no direct integration was built.

## Topology

- One Cisco 2911 router
- One Cisco 2960 managed switch
- Two HR PCs, two IT PCs, and one simulated server
- Router-on-a-stick over an 802.1Q trunk

Switch ports: Fa0/1–2 for HR, Fa0/3–4 for IT, Fa0/5 for the server, and Gi0/1 as the trunk.

## VLANs and addressing

| VLAN | Purpose | Network | Gateway | Endpoints |
|---:|---|---|---|---|
| 10 | HR | `192.168.10.0/24` | `192.168.10.1` | `192.168.10.11`, `.12` |
| 20 | IT | `192.168.20.0/24` | `192.168.20.1` | `192.168.20.11`, `.12` |
| 30 | Servers | `192.168.30.0/24` | `192.168.30.1` | Server: `192.168.30.10` |
| 99 | Management | `192.168.99.0/24` | `192.168.99.1` | Switch: `192.168.99.2` |

## Security and monitoring

- Router subinterfaces provide the VLAN gateways on `GigabitEthernet0/0`.
- ACLs block HR-to-IT and IT-to-HR traffic. HR and the server are also blocked from the management subnet.
- Router SSH version 2 uses local login and is restricted to the IT subnet.
- Router and switch syslog messages are sent to the simulated server at `192.168.30.10`.
- Credentials and private keys are intentionally omitted.

## Verification

- Router VLAN gateway subinterfaces showed `up/up`.
- Switch VLAN membership, trunk, and VLAN 99 management SVI were checked.
- HR-to-IT and IT-to-HR pings were blocked; HR and IT could reach the server.
- Syslog messages appeared in the Packet Tracer server’s SYSLOG service.
- SSH from IT-PC1 successfully reached the router prompt (`R1#`).
- Linux Mint captured an ICMP request to its VirtualBox network gateway with `tcpdump`.

## Reproducing the lab

1. Recreate the devices and cabling using the port plan above.
2. Create VLANs 10, 20, 30, and 99; assign access ports and configure the trunk.
3. Configure router subinterfaces and endpoint addresses from the table.
4. Apply the ACLs, switch management SVI, syslog destination, and SSH settings.
5. Verify permitted and blocked traffic, syslog reception, and SSH from the IT VLAN.

Add your saved Packet Tracer `.pkt` file and reviewed screenshots before publishing. Check screenshots for passwords, keys, and personal information.

## Tools and learning outcomes

Tools: Cisco Packet Tracer, Oracle VirtualBox, Linux Mint, `ip`, `ping`, and `tcpdump`.

Practiced VLAN segmentation, 802.1Q routing, IPv4 ACLs, switch management, syslog, SSH, and basic packet observation.