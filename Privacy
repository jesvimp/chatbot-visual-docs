# Privacy Policy

Last updated: 12 May 2026

This Power BI custom visual ("AI data visual") provides a chat-style
interface within a Power BI report. The Visual is published for
Implement Consulting Group ("Implement") and functions as a
client for Implement's internal generative AI service. This
policy describes what data the Visual processes.

## How the Visual works
The Visual is a thin client. It does not perform any AI
processing locally. When a user submits a prompt, the Visual
sends an authenticated HTTPS request to a backend service
operated by Implement.

The Visual cannot communicate with arbitrary services. The set of
hosts it is permitted to contact, and the audience for which its
access tokens are issued, are both fixed in the Visual's signed
package and enforced by the Power BI host.

## Authentication
The Visual uses the Power BI Authentication API to obtain a
Microsoft Entra ID access token for the signed-in user. This
token is:

- Issued by Microsoft Entra ID.
- Scoped to an audience corresponding to the Implement-operated
  backend, as declared in the Visual's manifest.
- Forwarded to the backend in the Authorization header of the
  HTTPS request.
- Not stored, cached, or persisted by the Visual beyond the
  individual request it is used for.
- Not transmitted to any party other than the Implement-operated
  backend.

Use of the Authentication API requires the user's Power BI tenant
administrator to enable the relevant organizational visual
setting. If the setting is disabled, the Visual will not be able
to authenticate and will not transmit any data.

## Data transmitted to the Implement backend
When a user submits a prompt, the Visual transmits the following
to the Implement-operated backend:

- The text of the user's prompt.
- The data bound to the Visual from the Power BI report (the rows
  and fields the report author has connected to the Visual).
- The Microsoft Entra ID access token described above.
- Standard HTTP request metadata.

## Data processing by the Implement backend
The Implement backend uses the data it receives to generate a
response to the user's prompt. This may involve:

- Identifying the signed-in user via the Entra ID access token.
- Forwarding the prompt and bound report data to one or more
  large language model providers or internal agent systems.
- Returning a generated response to the Visual for display in
  the Power BI report.

Implement is the data controller for any data received and
processed by the backend, including retention, logging, and
onward transmission to third-party services. Processing is
governed by Implement's internal data protection policies and
applicable law, including the EU General Data Protection
Regulation (GDPR).

For questions about how the backend processes data, contact
Implement directly using the address below.

## Data the Visual stores
The Visual does not persist any data outside the lifetime of the
Power BI report session. Conversation history shown in the
Visual exists only in memory and is discarded when the report is
closed. Access tokens are held only for the duration of the
individual request they are used for.

## Third-party services
The Visual itself does not integrate with analytics, tracking, or
advertising services. Authentication is handled by Microsoft
Entra ID through the Power BI Authentication API. All other
processing occurs at the Implement-operated backend, under
Implement's control.

## Intended audience
The Visual is intended for use by Implement Consulting Group and
parties authorized by Implement to access the backend service.
Users outside this scope will not be able to authenticate
successfully and the Visual will not function for them.

## Changes to this policy
This policy may be updated from time to time. The "Last updated"
date at the top of this document reflects the most recent change.

## Contact
For questions about this policy or the Visual:
JesperSvenningsen@Jesperforretning.onmicrosoft.com
