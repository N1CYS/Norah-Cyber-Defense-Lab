# Network Design

**Status: Implemented for NCDL v1**

NCDL currently uses a single lab LAN behind OPNsense. Multiple VLANs are not required or implemented for v1.

## Current network

| Network or interface | Addressing | Purpose | Status |
|---|---|---|---|
| OPNsense WAN | VMware NAT | Upstream connectivity through VMware Workstation | **Completed** |
| OPNsense LAN | `10.10.10.1/24` | Default gateway for the NCDL LAN | **Completed** |
| NCDL LAN | `10.10.10.0/24` | Isolated network containing the domain controller and Wazuh server | **Completed** |

## Current systems

| Host | Operating system | Address | Role | Status |
|---|---|---|---|---|
| `NCDL-DC01` | Windows Server 2022 | `10.10.10.10` static | AD DS, DNS, Group Policy, Windows security auditing, Wazuh agent 001 | **Operational** |
| `NCDL-SIEM01` | Ubuntu Server 24.04 LTS | `10.10.10.20` static | Wazuh Manager, Indexer, and Dashboard | **Operational** |

## Traffic and access paths

| Source | Destination | Purpose | Current state |
|---|---|---|---|
| `NCDL-DC01` | `NCDL-SIEM01` | Wazuh agent communication and Windows security telemetry | **Validated** |
| Windows 11 host | Wazuh Dashboard on `NCDL-SIEM01` | Administrative browser access through OPNsense Destination NAT/firewall rule | **Validated and restricted** |
| OPNsense WAN | VMware NAT | Upstream network path | **Implemented** |

The Windows 11 host is not directly connected to `10.10.10.0/24`. Dashboard access depends on the restricted OPNsense rule rather than broad host access to the lab LAN.

## Security design

- OPNsense is the network boundary and router for the lab.
- Server addresses are static to keep identity and telemetry paths stable.
- Administrative dashboard access is restricted through an explicit firewall/NAT path.
- The current single-subnet design is intentionally small enough to operate, observe, and document accurately.
- Any future rule or topology change must be documented before broader access is claimed.

No claim is made here about unlisted firewall rules, ports, DNS forwarding behavior, time synchronization, configuration backups, or formal segmentation tests.

## Optional future segmentation

Dedicated management, sensor, adversary, or workload VLANs may be considered after NCDL v1. They are not needed for the current goals and are not implemented.

## Related documents

- [Architecture](ARCHITECTURE.md)
- [Roadmap](ROADMAP.md)
- [Repository overview](../README.md)
