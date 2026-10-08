# Additive Cloud SBC Resiliency for Teams Direct Routing

## Overview

This reference architecture describes an additive resiliency model in
which cloud-hosted Session Border Controllers supplement an existing
physical SBC deployment.

The objective is to introduce an additional voice-edge hosting and
recovery domain without requiring the immediate retirement of the
existing infrastructure.

This is a generic reference design. It does not represent the deployment,
configuration, carrier arrangements, or infrastructure of any specific
organization.

## Design Objectives

- Preserve the existing Teams Direct Routing model.
- Maintain existing physical SBC services during cloud adoption.
- Add cloud-hosted SBCs as an alternate voice path.
- Reduce dependence on a single infrastructure hosting domain.
- Support controlled failover and failback.
- Minimize user-facing changes.
- Validate cloud operations before considering future consolidation.

## Conceptual Architecture

The design contains two SBC infrastructure tiers:

1. Existing physical SBC tier
2. Additional cloud-hosted SBC tier

Both tiers may connect to:

- Microsoft Teams Direct Routing
- One or more SIP carriers
- Enterprise monitoring and logging services
- Approved certificate, DNS, and identity services

## Conceptual Call Path

Microsoft Teams Phone
→ Teams Direct Routing
→ Available physical or cloud SBC
→ SIP carrier
→ PSTN

## Potential Traffic Models

### Physical Preferred, Cloud Recovery

The physical SBC tier remains the preferred production path. Cloud SBCs
provide an alternate path during maintenance, service degradation, or
loss of the physical environment.

### Controlled Active Traffic

A defined portion of production traffic uses the cloud SBC tier. This
continuously exercises the cloud path while preserving the physical tier.

### Service-Specific Routing

Selected services, sites, number ranges, or test users use the cloud tier
while other services continue through the physical tier.

The selected model must align with the SBC vendor, Microsoft Teams,
carrier routing, and organizational recovery requirements.

## Resiliency Considerations

The design should consider failure of:

- A single SBC instance
- A cloud availability zone or equivalent failure domain
- The existing physical SBC site
- A cloud region
- A carrier signaling path
- A media path
- DNS or certificate services
- Administrative and monitoring services

## Cloud SBC Instance Considerations

A resilient deployment normally begins by evaluating at least two cloud
SBC instances. The final quantity depends on:

- Concurrent call volume
- Calls per second
- Codec and transcoding requirements
- Media bypass design
- Maintenance capacity
- Failure capacity
- Regional recovery requirements
- SBC licensing
- Vendor-supported high-availability patterns

## Carrier Connectivity Options

Potential designs include:

- SIP connectivity over the public internet
- Private connectivity
- Carrier-managed cloud interconnect
- Cloud connectivity exchange
- VPN-based connectivity
- Multiple carrier destinations

The carrier must confirm supported routing, health detection, failover,
restoration, source addressing, encryption, and media behavior.

## Operating States

The architecture should define behavior for:

1. Normal operation
2. Cloud-path testing
3. Physical SBC failure
4. Cloud SBC failure
5. Carrier-path failure
6. Regional failure
7. Planned maintenance
8. Controlled failback

## Capacity Principle

Capacity should be evaluated for each required failure state, not only
for the combined capacity of all SBCs.

If the cloud tier is expected to recover the physical tier, the cloud tier
must support the defined recovery load with the required availability
margin.

## Security Considerations

- Use supported TLS and SRTP configurations.
- Protect SBC management interfaces.
- Apply least-privilege administrative access.
- Monitor certificate expiration.
- Restrict signaling and media traffic to approved sources.
- Centralize security and operational logs.
- Maintain tested configuration backups.
- Document patching and vulnerability-management ownership.

## Operational Requirements

Monitor:

- SBC instance health
- SIP trunk status
- Teams connectivity
- Call failures
- Concurrent sessions
- Media quality
- Certificate expiration
- Licensing status
- Cloud platform health
- Carrier-path availability

## Validation Scenarios

Validate at minimum:

- Inbound calling through each production path
- Outbound calling through each production path
- Caller ID presentation
- Call transfer
- Auto attendant and call queue routing
- Voicemail behavior
- Emergency calling
- Single-SBC failure
- Physical-tier failure
- Cloud-tier failure
- Carrier rerouting
- Failback
- Configuration restoration
- Monitoring and alert generation

## Future-State Decision

Deployment of cloud SBCs does not automatically require retirement of
physical SBCs.

After the cloud tier has demonstrated stability, the organization may
separately evaluate whether to:

- Maintain the hybrid model
- Increase cloud traffic
- Expand to additional cloud regions
- Reduce physical infrastructure
- Consolidate onto cloud-hosted SBCs

That decision should be based on technical evidence, service reliability,
cost, operational readiness, carrier support, and organizational risk
tolerance.

## Related Pages

- ../01-Architecture
- ../03-Direct-Routing
- ../05-Session-Border-Controllers
- ../06-Networking
- ../07-Security
- ../09-Disaster-Recovery
- ../10-Operations

## Disclaimer

This page contains a generic reference architecture for educational and
design-discussion purposes. It does not document the infrastructure,
network topology, configuration, carrier relationships, phone numbers,
security controls, or recovery procedures of any specific organization.

All names, domains, addresses, regions, capacity values, and examples
must be fictional or illustrative.
