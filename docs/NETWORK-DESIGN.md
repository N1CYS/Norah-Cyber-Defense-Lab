# Network Design

**Status: Planned design - subnets and VLANs are not deployed**

The table below is a proposed segmentation model and example private addressing scheme. Final allocations depend on the selected hypervisor and firewall.

## Segmentation plan

| VLAN | Name | Example subnet | Planned assets | Default posture |
|---:|---|---|---|---|
| 10 | Management | `10.10.10.0/24` | Jump host, hypervisor management | Deny inbound from other workload VLANs |
| 20 | Identity | `10.10.20.0/24` | AD DS and DNS | Permit only required domain, DNS, telemetry, and management flows |
| 30 | Users | `10.10.30.0/24` | Windows endpoints | Permit required identity, DNS, telemetry, and controlled egress |
| 40 | Linux | `10.10.40.0/24` | Linux endpoint | Permit required DNS, telemetry, and controlled egress |
| 50 | Security | `10.10.50.0/24` | SIEM, Wazuh, Velociraptor | Accept defined ingestion; analyst access from management only |
| 60 | Sensors | `10.10.60.0/24` | Zeek and Suricata management interfaces | No transit routing; management and log export only |
| 90 | Adversary | `10.10.90.0/24` | Kali Linux | Isolated by default; temporary exercise-specific rules |

These ranges are examples. Planned servers will use static addresses or reservations; endpoints will use lab DHCP where appropriate.

## Traffic policy

OPNsense or pfSense will route between VLANs and enforce a default-deny inter-VLAN policy. Rules will be specific by source, destination, port, and purpose.

| Source | Destination | Planned allowance |
|---|---|---|
| User/Linux | Identity | DNS, Kerberos, LDAP/LDAPS, SMB, NTP, and other documented domain dependencies |
| Monitored hosts | Security | Agent, forwarder, syslog, and forensic-control traffic on defined ports |
| Sensors | Security | Zeek/Suricata log export and health monitoring |
| Management | Infrastructure | Restricted administrative protocols from the jump host |
| Adversary | Lab target | Disabled by default; narrow source/destination/time window per exercise |
| Any lab VLAN | Management | Denied unless an explicit administrative dependency is documented |
| Lab egress | Internet | Updates and approved dependencies; logged and restricted where practical |

Domain-controller internet access will be minimized. DNS recursion, forwarding, and egress behavior will be explicitly documented after deployment.

## Sensor placement

Zeek and Suricata are planned to receive mirrored virtual-switch or firewall traffic through a dedicated monitoring interface. Their management interfaces will remain in the sensor segment. The capture interface should not have a routable IP address. Visibility tests will verify which east-west and north-south paths are actually observed before network coverage is claimed.

## Adversary isolation

The Kali host will have no standing route to the management VLAN, hypervisor administration, or non-lab private networks. Exercise access will require:

1. a documented target and expected telemetry;
2. a snapshot or recovery point where appropriate;
3. a temporary firewall rule limited to the required path;
4. monitoring enabled before execution;
5. removal and verification of the rule after the exercise.

No uncontrolled bridging or shared clipboard/file transfer is assumed. Internet access will be disabled during exercises unless a specific, safe dependency is documented.

## Foundational controls

- Central NTP with timezone-aware event handling
- Internal DNS through AD-integrated DNS where appropriate
- Unique administrative and standard-user accounts
- Host firewall enabled on endpoints
- Central log transport protected and access-controlled
- Configuration backups for firewall and critical security services
- Asset inventory mapping hostname, IP, role, owner, and telemetry status
- Health checks for collection gaps, clock drift, and parser failures

## Validation criteria

Segmentation is only considered implemented after evidence shows:

- allowed flows succeed and denied flows fail;
- the adversary VLAN cannot reach management services;
- sensors observe the intended traffic paths;
- firewall events arrive in the selected analytics platform;
- DNS and time synchronization work consistently across the domain;
- rule exports and sanitized test results are stored under [`configs/`](../configs/README.md) and [`evidence/`](../evidence/README.md).

## Related documents

- [Architecture](ARCHITECTURE.md)
- [Roadmap](ROADMAP.md)
- [Repository overview](../README.md)
