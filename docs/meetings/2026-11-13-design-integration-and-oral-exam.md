# Meeting: Design integration and oral exam preparation

**Date:** 2026-11-13

**Purpose:** Review the staff UI workflow and revised tracking hardware, agree on the remaining fall-term design work, and discuss the oral exam and report schedule.

## Discussion

* Omar presented the preliminary staff UI workflow for bed assignment and transfers, and visitor monitoring and security response. Staff log in to a dashboard with access based on their roles. Nadif clarified that visitors interact with staff, who use the system on their behalf. The [UI design](../design/software/ui.md) is intended for staff.
* The bed workflow covers entering patient requirements, reviewing suitable beds, confirming a reservation, and scheduling a transfer. Completing a transfer occupies the destination bed and marks the previous bed for cleaning where applicable. Cancelling releases the destination reservation and preserves the existing assignment. Proposed screens also cover discharge and bed release.
* The visitor workflow covers registration, permitted destinations, tracking setup, a hospital map with floors and zones, security events, and closing a visit. Green observations are recorded, orange or yellow observations prompt a warning or review, and red observations notify security. Closing the visit ends temporary permissions and the tracking association. Omar confirmed that the premises map is planned and still needs to be added to the UI design.
* Bilal proposed BLE identification badges issued on lanyards, with receivers alongside presence sensors at gateways. Badge observations would pass through the Raspberry Pi to the backend so staff can associate a visitor with an observed location. This develops the identity-tracking approach discussed at the [previous meeting](2026-11-06-preliminary-design-review.md). Receiver power and deployment cost still need investigation. MJ suggested considering battery-powered equipment, with the actual equipment and power requirements to be verified.
* For room monitoring, Bilal described PIR motion, magnetic door, and DHT11 sensors connected to an ESP32. He reported preliminary testing with resistors and planned further compatibility testing. MJ emphasized checking both signal levels and supply voltages when connecting 5 V sensors and 3.3 V electronics. The design needs suitable power regulation as well as any signal-level conversion. See the [hardware compatibility review](../design/hardware/overview.md).
* Nadif proposed using the remaining design work to integrate the hardware, software platform, UI, and analytics. The designs had developed separately, and the more detailed hardware and UI work can now inform the platform's data model and interfaces. MJ agreed that this should be the work item for the following week, which would be the final project meeting before the oral exam. See the [integration design](../design/interfaces/integration.md).
* MJ targeted November 27, in week 12, for the oral exam and requested a draft report for it. Each member should understand the overall project and be prepared for detailed questions about their own contribution. The exam is expected to take about 40–60 minutes for the four members. A possible 3–4 p.m. slot was discussed, with the time to be settled at the next meeting. MJ stated that the final report could be submitted through December 4, leaving a week after the exam for refinement.

## Decisions

* Keep the UI focused on staff, with staff handling visitor interactions through the system.
* Make integration of the hardware, platform, UI, and analytics designs the main task for the next project meeting.
* Target **Friday, November 27, 2026**, for the oral exam, with a draft report available for the examiner. Confirm the time at the next meeting.
* The following week's meeting will be the final project meeting. With the exam targeted for week 12, MJ confirmed that a week 13 meeting would be unnecessary.

## Action items

The November 20 preparation date is inferred from the following-week discussion. Individual owners for the integration work were not assigned. Other dates below reflect the schedule discussed with MJ.

| Action | Owner | Due date | Issue / link |
|----|----|----|----|
| Refine the hardware, platform, UI, and analytics designs together so their data needs, interfaces, and workflows align. | Team | 2026-11-20 | [Integration design](../design/interfaces/integration.md) |
| Continue checking sensor compatibility, signal levels, and power supplies, including BLE receiver deployment options. | Bilal | TBD | [Hardware compatibility review](../design/hardware/overview.md) |
| Agree on the oral exam time and reserve approximately one hour. | Team and MJ | 2026-11-20 | — |
| Prepare a draft report for MJ and review the overall project and each member's own contribution for the oral exam. | Team | 2026-11-27 (target exam date) | — |
| Refine and submit the final report. | Team | 2026-12-04 | — |

## Open questions

* What data and interfaces must connect the hardware observations, platform model, UI, and analytics workflows?
* What time will the November 27 oral exam take place?
