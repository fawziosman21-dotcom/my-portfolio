# Enterprise Network Infrastructure

Cisco Packet Tracer project.

## Project

Enterprise network with:

- VLANs
- Inter-VLAN routing
- DHCP
- Cisco ASA firewall
- NAT/PAT
- ACL
- ISP router
- Simulated Internet

## VLANs

VLAN 10 - Users - 10.10.10.0/24

VLAN 20 - Servers - 10.10.20.0/24

VLAN 30 - Management - 10.10.30.0/24

VLAN 40 - Wireless - 10.10.40.0/24

## Firewall

Inside: 10.10.254.1/30

Outside: 203.0.113.1/30

ISP Router: 203.0.113.2/30

Default route: 0.0.0.0/0 -> 203.0.113.2

## NAT

Internal network: 10.10.0.0/16

NAT/PAT through the ASA outside interface.

## Testing

PC -> 8.8.8.8

4/4 replies

0% packet loss

## Files

Packet Tracer project

Project topology and configuration screenshot
