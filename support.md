# Support

Last updated: 12 May 2026

This document provides support information for the Power BI
custom visual published by Implement Consulting Group ("AI chat visual"). The Visual is a thin client for an internal generative
AI service operated by Implement.

## Getting help
For questions, bug reports, or feature requests, contact:

- Email: JesperSvenningsen@Jesperforretning.onmicrosoft.com
- Response time: best effort, typically within 5 business days.

When reporting a bug, please include:

- A description of what you expected to happen.
- What actually happened (including any error messages shown in
  the Visual).
- The Power BI environment you encountered the issue in (Power BI
  Desktop version, Power BI Service, mobile, etc.).
- A small sample `.pbix` file demonstrating the issue, if
  possible.

## Intended audience
The Visual is intended for use by Implement Consulting Group and
parties authorized by Implement to access its backend service.
Users outside this scope will not be able to authenticate and the
Visual will not function for them. This is by design — see the
"Security and data flow" section below.

## Troubleshooting

### The Visual loads but does not respond to prompts
Likely causes, in order of probability:

1. **The Power BI Authentication API is disabled at the tenant
   level.** This API is disabled by default. The user's Power BI
   or Fabric tenant administrator must enable the relevant
   organizational visual setting. See:
   https://learn.microsoft.com/en-us/fabric/admin/organizational-visuals

2. **The tenant has not granted consent for the Visual's backend
   application.** A tenant administrator may need to grant consent
   so the backend can receive tokens issued in the tenant. See:
   https://learn.microsoft.com/en-us/power-bi/developer/visuals/entra-id-authentication

3. **The user is not authorized on the backend itself.** Even with
   a valid Entra ID token, the backend applies its own access
   controls. Contact Implement to confirm the user is provisioned.

4. **The backend is unreachable.** Network issues, backend
   downtime, or regional connectivity problems can prevent
   responses. Contact Implement to confirm service status.

### Requests appear to be blocked at the network layer
The Visual is restricted to a fixed list of permitted hosts
declared in its signed package (see "Security and data flow"
below). Requests to any other host are blocked by the Power BI
host before they leave the visual's iframe. If a deployment
requires the Visual to reach a different host, the Visual must
be re-packaged with an updated allowlist and re-published to
Microsoft AppSource.

### The Visual will not authenticate in Power BI Report Server, embedded analytics, or Teams
The Power BI Authentication API does not currently support these
environments. The Visual works in:

- Power BI Service (web).
- Power BI Desktop.
- Power BI Report Server Desktop.
- Power BI mobile applications.

It does not work in Power BI Report Server (server-side), embedded
analytics, or Microsoft Teams. This is a Power BI platform
limitation, not a limitation of the Visual.

## Security and data flow

The Visual is designed so that the data it transmits, and the
audience of the tokens it obtains, are constrained by the Power
BI platform itself rather than by the Visual's own code. Two
independent enforcement layers apply.

### 1. Network allowlist (WebAccess privilege)
The Visual's manifest (`capabilities.json`) declares a fixed list
of hosts the Visual is permitted to contact over the network.
This list is enforced by the Power BI host before any request
leaves the visual's iframe. Requests to hosts outside the list
are blocked at the network layer, regardless of any configuration
applied to the Visual within the report.

The allowlist is baked into the signed `.pbiviz` package.
Changing it requires repackaging and republishing the Visual
through Microsoft AppSource.

### 2. Token audience binding (AADAuthentication privilege)
The Microsoft Entra ID access token the Visual obtains through
the Power BI Authentication API is minted for a specific
pre-declared audience corresponding to Implement's registered
application. The Visual cannot request a token for any other
audience. Only a backend pre-authorized to validate tokens for
that audience can accept the request.

The audience is also baked into the signed `.pbiviz` package.

### What this means in practice
The combination of these two enforcement layers means:

- Tokens issued for the Visual cannot be redirected to a
  third-party service.
- Report data transmitted by the Visual cannot reach hosts other
  than those on the allowlist.
- A malicious or misconfigured report cannot cause the Visual to
  exfiltrate data or tokens.

These constraints are enforced by the Power BI runtime — not by
the Visual's own code — and cannot be modified without
republishing the Visual through Microsoft AppSource.


## Updates and versioning
Updates to the Visual are distributed through Microsoft AppSource.
Existing reports using the Visual will receive updates
automatically when a new version is approved and published. To
report issues with a specific version, please include the version
number from the Visual's "About" or formatting pane.
