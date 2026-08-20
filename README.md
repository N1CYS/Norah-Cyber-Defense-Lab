# Norah Cyber Defense Lab

NCDL is a practical Cyber Defense and SOC home lab built to develop and document network and Active Directory security, centralized Windows monitoring with Wazuh, detection engineering, alert investigation, and evidence-based reporting.

> **Current status: Core infrastructure and telemetry operational / Detection validation is next**
>
> VMware Workstation, OPNsense, Active Directory, DNS, Wazuh 4.14.7, and Windows event collection are implemented and validated. Custom detections, a complete SOC investigation, MITRE ATT&CK mapping, and an incident report remain planned for NCDL v1.

![NCDL v1 logical architecture](assets/diagrams/ncdl-logical-architecture.svg)

## Implemented Capabilities

- Isolated VMware-based lab networking with OPNsense
- Windows Server 2022 Active Directory Domain Services and DNS
- Group Policy and Windows security auditing
- Wazuh 4.14.7 centralized security monitoring
- Active Wazuh agent on `NCDL-DC01`
- Windows security telemetry ingestion
- Visibility into process creation, authentication/logon activity, and Security Configuration Assessment findings
- Restricted administrative access to the Wazuh Dashboard through OPNsense

## NCDL v1 Next Deliverables

- Controlled generation of security-relevant activity
- Custom Wazuh detection development and validation
- SOC alert triage and investigation
- MITRE ATT&CK mapping based on validated behavior
- One complete evidence-backed investigation
- One sanitized incident-style report

## Technology stack

| Layer | Current implementation |
|---|---|
| Hypervisor | VMware Workstation |
| Firewall and routing | OPNsense; WAN through VMware NAT; LAN `10.10.10.1/24` |
| Identity and auditing | `NCDL-DC01`; Windows Server 2022; AD DS, DNS, Group Policy, and Windows security auditing; `10.10.10.10` |
| Security monitoring | `NCDL-SIEM01`; Ubuntu Server 24.04 LTS; Wazuh 4.14.7 all-in-one; `10.10.10.20` |
| Endpoint telemetry | Wazuh agent 001 on `NCDL-DC01`, active and communicating |
| Analyst access | Windows 11 host through a restricted OPNsense Destination NAT/firewall rule |

## NCDL v1 architecture

The current lab uses one isolated `10.10.10.0/24` LAN behind OPNsense. The domain controller sends Windows security telemetry to the Wazuh all-in-one server. The Windows 11 host is not directly attached to NCDL-LAN; dashboard access crosses a restricted OPNsense Destination NAT/firewall rule.

See [Architecture](docs/ARCHITECTURE.md) for component and telemetry detail, and [Network Design](docs/NETWORK-DESIGN.md) for the implemented addressing and access path.

## Project status

| Workstream | Status |
|---|---|
| VMware Workstation lab and OPNsense routing | **Completed** |
| AD DS and DNS on `NCDL-DC01` | **Completed** |
| Wazuh 4.14.7 all-in-one deployment | **Completed** |
| Wazuh agent enrollment and Windows telemetry ingestion | **Completed** |
| Controlled generation and analysis of security-relevant activity | **Planned for NCDL v1 (next)** |
| Custom Wazuh detection engineering and validation | **Planned for NCDL v1** |
| End-to-end SOC investigation and ATT&CK mapping | **Planned for NCDL v1** |
| Sanitized incident-style report with supporting evidence | **Planned for NCDL v1** |
| Additional SIEM, NSM, DFIR tooling, or network segmentation | **Optional future enhancement** |

"Completed" reflects only the implementation and validation facts stated in this repository. It does not imply that unfinished detections, investigations, or reporting exist.

## Repository guide

| Section | Purpose |
|---|---|
| [Architecture](docs/ARCHITECTURE.md) | Current components, access paths, and telemetry flow |
| [Network design](docs/NETWORK-DESIGN.md) | Current subnet, addressing, VMware NAT, and firewall access |
| [Roadmap](docs/ROADMAP.md) | Completed foundation and remaining v1 work |
| [Detections](detections/README.md) | Future custom Wazuh rules and validation records |
| [Investigations](investigations/README.md) | Future SOC case notes, queries, timelines, and conclusions |
| [Attack simulations](attack-simulations/README.md) | Controlled event-generation scope and safeguards |
| [Incident reports](incident-reports/README.md) | Future sanitized incident-style report |
| [Evidence](evidence/README.md) | Standards for supporting artifacts |
| [Configurations](configs/README.md) | Future sanitized defensive configuration records |

## Evidence integrity

No screenshot, alert, detection, investigation, or report is claimed unless it was produced by actual NCDL activity and stored with enough context to evaluate it. Repository evidence will identify its source, time, method, redactions, and limitations. No screenshots or raw evidence have been added yet.

## Scope and safety

Security-relevant activity will be generated only in the controlled lab and only to validate defensive telemetry and detections. This repository will not contain malware, credentials, persistence tooling, or executable offensive scripts.

Splunk, Elastic, Zeek, Suricata, Velociraptor, Linux endpoints, and additional VLANs are not required for NCDL v1. They may be evaluated later only if they add a clear defensive learning objective.

Licensed under the [MIT License](LICENSE).
