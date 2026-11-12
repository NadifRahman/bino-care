# Meeting: Preliminary design review

**Date:** 2026-11-06

**Purpose:** Review the web application decision and the preliminary designs for bed placement, patient transfers, and visitor monitoring.

## Discussion

* A browser-based application supports the dashboards, forms, maps, and notifications needed for both use cases. Centralized deployment lets staff use the latest version without installing updates on their devices. The tradeoffs are dependence on a working network connection and the need to support different browsers and screen sizes. A separate monitoring system supplies location observations to the backend. See the [specification](../planning/specification.md#4-system-context).
* MJ asked the team to document the web application's security tradeoffs and distinguish the full design from the controls feasible in the prototype. The group discussed role-based access and the risk that someone could use a stolen session token to impersonate a user. Nadif suggested shorter session lifetimes with reauthentication as a possible mitigation.
* Nadif presented two views of a preliminary PostgreSQL data model. The bed placement view separates people from login accounts, links patients to beds through time-based assignments, and records transfers between locations. Beds belong to zones, and each zone belongs to a floor. The monitoring view assigns zone permissions by role, associates tracking identifiers with visitors and their visits, and records location observations and security events. Importing a GeoJSON layout at startup would let the team configure the map for different demo sites. See the [software platform design](https://github.com/NadifRahman/bino-care/blob/ec19950445e3491286941398f68063b552a58048/docs/design/software/platform.md#data-model).
* Iftakher proposed filtering out unsuitable or unavailable beds before using AI to rank and explain the remaining recommendations. A rule-based ordering would serve as a fallback if AI is unavailable, and staff would make the final selection. In the monitoring workflow, zone rules would log green observations, prompt a warning or review for orange, and notify security for red. AI could summarize unusual patterns in the recorded history. The immediate response would run independently of AI.
* Bilal presented a preliminary hardware block diagram and discussed an mmWave presence sensor and a Raspberry Pi Camera Module 3 for building access monitoring. MJ suggested mapping deployed sensor IDs to zones so a presence reading can be tied to an area on the map. The design still needs a way to associate the reading with a specific visitor. Bilal also raised the question of whether the sensors can detect someone who stays still.

## Decisions

* Proceed with a browser-based application for desktop and mobile because both use cases fit a web interface and updates can be deployed centrally.
* Document the web security tradeoffs in the full design and identify which controls the prototype can support.

## Action items

| Action | Owner | Due date | Issue / link |
|----|----|----|----|
| Document the web security tradeoffs and identify the controls feasible for the prototype. | Team | TBD | — |
| Coordinate with Nadif on the platform data and functions needed for the recommendation and monitoring workflows. | Iftakher | TBD | [Software platform design](https://github.com/NadifRahman/bino-care/blob/ec19950445e3491286941398f68063b552a58048/docs/design/software/platform.md#data-model) |
| Refine the hardware block diagram to show how tracking will determine a visitor's zone and identity. | Bilal | Following week | — |

## Open questions

* How will the tracking system associate a zone observation with a specific registered visitor?
* Which sensors can reliably detect someone who remains stationary?
* Which web security controls will the prototype implement, and what session lifetime and reauthentication policy should it use?
