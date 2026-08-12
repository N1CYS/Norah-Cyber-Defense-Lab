# Roadmap

**Status: Foundation complete / deployment planned**

Each phase remains planned or in progress until its exit evidence is stored in the repository. Scheduling begins after hardware capacity is confirmed.

## Phase 1 - Platform and network foundation

- Select the hypervisor and document capacity constraints.
- Deploy OPNsense or pfSense and create the planned VLANs.
- Configure default-deny inter-VLAN policy, NTP, controlled egress, and configuration backup.
- Validate allowed and denied paths, including adversary isolation.

**Exit evidence:** sanitized network configuration, rule matrix, reachability tests, and architecture updates.

## Phase 2 - Identity and representative endpoints

- Deploy AD DS and DNS with a documented domain model.
- Join Windows endpoints and establish standard and administrative identities.
- Deploy the Linux endpoint and baseline host firewalls.
- Record asset inventory and recovery procedures.

**Exit evidence:** sanitized configuration excerpts, domain and DNS validation, asset inventory, and recovery test notes.

## Phase 3 - Telemetry and platform health

- Select and deploy Splunk, Elastic, or a justified combination.
- Onboard Windows, Linux, AD, DNS, and firewall telemetry.
- Deploy Wazuh, Velociraptor, Zeek, and Suricata.
- Validate timestamps, parsing, host identity, sensor visibility, access control, and retention.

**Exit evidence:** source-by-source ingestion tests, data dictionaries, sensor visibility tests, and documented gaps.

## Phase 4 - Detection engineering

- Define a detection template with logic, data requirements, ATT&CK mapping, severity rationale, and false-positive analysis.
- Build an initial identity, endpoint, and network detection set.
- Validate each analytic with controlled inputs or representative datasets.
- Track tuning decisions and regression tests in version control.

**Exit evidence:** versioned detections with reproducible tests and linked evidence. Detection count is not an exit criterion.

## Phase 5 - SOC investigations and threat hunting

- Create repeatable triage and investigation templates.
- Conduct cross-source investigations using endpoint, identity, DNS, firewall, Zeek, and Suricata data.
- Use Velociraptor for targeted, authorized forensic acquisition.
- Document conclusions, alternative hypotheses, limitations, and recommended improvements.

**Exit evidence:** sanitized investigation records, timelines, queries, evidence hashes where appropriate, and review notes.

## Phase 6 - Controlled adversary simulation and DFIR

- Define narrowly scoped simulations tied to detection hypotheses.
- Confirm isolation, recovery, telemetry, and stop conditions before execution.
- Exercise the SOC workflow and produce incident-style reports.
- Feed validated gaps back into architecture, collection, and detection engineering.

**Exit evidence:** approved simulation plan, actual observations, linked raw evidence, incident report, cleanup confirmation, and improvement backlog.

## Ongoing quality gates

- No claim of completion without dated, reproducible evidence.
- No secrets, malware, personal data, or reusable offensive tooling in the public repository.
- Every material analytic states its data dependencies and limitations.
- Architecture and network documentation are updated when implementation diverges from design.
- ATT&CK mappings identify behavior; they do not substitute for validation.

## Related documents

- [Architecture](ARCHITECTURE.md)
- [Network Design](NETWORK-DESIGN.md)
- [Repository overview](../README.md)
