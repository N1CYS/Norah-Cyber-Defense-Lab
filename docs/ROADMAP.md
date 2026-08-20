# Roadmap

**Status: Core infrastructure complete / SOC workflow planned next**

The roadmap distinguishes deployed infrastructure from work that still requires validation and evidence.

## Completed

### Platform and networking

- VMware Workstation selected and in use.
- OPNsense deployed with WAN through VMware NAT.
- NCDL LAN deployed as `10.10.10.0/24`; OPNsense LAN is `10.10.10.1/24`.
- Restricted OPNsense Destination NAT/firewall access established from the Windows 11 host to the Wazuh Dashboard.

### Identity and monitoring

- `NCDL-DC01` deployed on Windows Server 2022 at `10.10.10.10`.
- Active Directory Domain Services, DNS, Group Policy, and Windows security auditing implemented.
- `NCDL-SIEM01` deployed on Ubuntu Server 24.04 LTS at `10.10.10.20`.
- Wazuh 4.14.7 all-in-one deployed; Manager, Indexer, and Dashboard are operational.
- `NCDL-DC01` enrolled as Wazuh agent 001; the agent is active and communicating.
- Windows process creation, authentication/logon/logoff, and Security Configuration Assessment data are visible in Wazuh.

## In progress

No detection, investigation, controlled activity record, ATT&CK mapping, or incident report is currently documented as in progress. The next work is listed below and will move to this section only after work begins.

## Planned for NCDL v1

### Controlled activity and telemetry analysis

- Generate security-relevant activity within the controlled lab.
- Identify the corresponding Wazuh events and alerts.
- Record queries, timestamps, expected observations, actual observations, and limitations.

This work has not started and no result is claimed in the repository yet.

### Custom Wazuh detections

- Select one or more behaviors supported by current Windows telemetry.
- Create custom Wazuh detection logic.
- Test expected matches and relevant non-matches.
- Record rule logic, data dependency, tuning rationale, and reproducible validation evidence.

### End-to-end SOC investigation

- Triage a validated alert or event set.
- Scope the affected host, account, activity, and time range.
- Build a timeline from Wazuh data.
- Separate facts, interpretations, alternative explanations, and gaps.
- Map only validated behavior to the applicable MITRE ATT&CK technique or sub-technique.

### Incident-style report

- Publish one sanitized report based on the completed investigation.
- Link the report to its detection, queries, timeline, and supporting evidence.
- Include findings, impact assessment, limitations, and defensive recommendations.

## NCDL v1 completion criteria

NCDL v1 will be complete when the repository contains:

1. At least one validated custom Wazuh detection.
2. A reproducible end-to-end SOC investigation.
3. A supported MITRE ATT&CK mapping.
4. One sanitized incident-style report.
5. Supporting evidence captured from actual lab activity.

## Optional future enhancements

Multiple VLANs, Splunk, Elastic, Zeek, Suricata, Velociraptor, Linux endpoints, and a dedicated adversary environment may be evaluated after v1. None is a v1 requirement or current implementation.

## Quality gates

- No completion claim without reproducible evidence.
- No secrets, personal data, malware, or executable offensive tooling in the public repository.
- Detections must state their data requirements, test method, and limitations.
- ATT&CK mappings must be supported by observed behavior.
- Documentation must be updated when the implemented environment changes.

## Related documents

- [Architecture](ARCHITECTURE.md)
- [Network Design](NETWORK-DESIGN.md)
- [Repository overview](../README.md)
