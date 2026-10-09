# Meeting: Hospital scenarios and project scope

**Date:** 2026-10-09

**Purpose:** Develop fuller hospital use cases before choosing the parts of BINO Care to implement.

## Discussion

* MJ suggested writing full scenarios first: describe the people, setting, events, and checkpoints in the whole situation, then choose a feasible subset to build. The current short use-case descriptions need more context.
* A patient-placement scenario could start when a patient arrives through one of several routes, then follow the steps to assign a room or bed. Hospitals and units may offer different specialties; a patient might need transfer to a specialized unit or another hospital. The scenario should cover short- and long-term assignments and remote bed booking where relevant.
* The team can describe room context and required equipment at an abstract level. Detailed medical data and clinical equipment decisions are outside the team's expertise.
* An emergency department scenario was suggested as a possible focus, with room assignment and equipment needs developed from that narrative.
* A security scenario could follow someone who enters as a visitor, gives a destination, and then wanders toward a restricted ward. The visitor's stated purpose could define permitted areas or a route. The discussion proposed green areas, red restricted areas, and an intermediate area for reasonable wrong turns. A small detour should prompt a proportionate response rather than an immediate security escalation.
* Role-based access was proposed for staff, patients, and visitors, with an administrator setting area permissions. A patient's assigned ward might also affect access. The group had not settled how detailed the roles and rules should be; the detail should follow the scenario's safety goal.
* An intruder might pose as a visitor, staff member, or patient. The discussion identified temporary visitor access as a more practical scenario to examine because staff credentials generally involve an earlier vetting process, while visitors may move through a hospital without an escort or continued supervision.
* One possible implementation was a temporary badge, scanner, or other identifier issued to a visitor and linked to them in the system. Scans or location events could record movement; returning the device at exit could confirm departure, with a notification if it is not returned. This was an example for scenario analysis, not a selected design.

## Decisions

* The next step is to write detailed scenarios and analyze the people, events, and system interactions in them. The emergency department focus, access zones, and visitor device were suggestions, not agreed implementation scope.


