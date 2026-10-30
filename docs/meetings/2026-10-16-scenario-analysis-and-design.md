# Meeting: Scenario analysis and design preparation

**Date:** 2026-10-16

**Purpose:** Review the hospital scenarios, address MJ's concerns, and clarify the design work to prepare for the next meeting.

## Discussion

* MJ pointed out that the bed-assignment scenario must include scheduling the patient transfer as well as the destination bed. Transfers may be between units in the same hospital or between hospitals.
* The proposed security scenario relied on visitors scanning temporary RFID cards at doors, with access logs used to track movement and identify suspicious activity. MJ questioned how tracking would continue after entry: hospital wards and patient rooms are generally open, so the team cannot assume a secured entrance and repeated card scans at every checkpoint. Some restricted spaces, such as laboratories, may still have controlled entrances.
* MJ called for "invisible monitoring": tracking that works in the background without requiring visitors to actively scan a card as they move. The design must explain both how visitors are detected and how their locations are placed on a hospital map. Each visitor would have designated green, orange, and red areas; detection in a red area could trigger a response.
* Motion detection, camera feeds/computer vision, RFID cards or lanyards read automatically from a distance, and an app with Wi-Fi beacons were discussed as possible approaches. These were design alternatives to investigate, not selected technologies.
* Nadif raised the risk that visitors could tamper with personal devices and send misleading information. The team leaned toward hospital-issued equipment, and MJ acknowledged the concern. The device and tracking method remained undecided.
* MJ emphasized deriving requirements from scenario analysis, then identifying the functional building blocks needed to meet them. For security, his examples were registration, monitoring, zone detection, and response. The team should draw a block diagram, then examine each block's sub-blocks and design choices.
* MJ recommended starting a living report now and adding scenarios, requirements, and design work as they develop, so this work contributes directly to the eventual report.

## Decisions

* Rework the visitor-tracking scenario around background monitoring rather than relying on repeated visitor-initiated scans. The tracking technology and hardware were not finalized.
* Develop the scenarios, requirements, functional blocks, and design choices in a living report.
* Move the next meeting to **Thursday, October 22, 2026, at 4:00 p.m.**, for that week only, because of the team's Friday midterm. MJ requested an email about the rescheduling.

## Action items

The October 22 dates below are preparation targets inferred from the next-meeting discussion, not separately assigned deadlines. Individual owners were not assigned. The specification follow-up is recorded for documentation alignment; it was not an explicit assignment from MJ.

| Action | Owner | Due date | Issue / link |
|----|----|----|----|
| Refine the scenarios to include bed-assignment and transfer scheduling, and background visitor tracking through open hospital areas. | Team (individual owner not assigned) | 2026-10-22 | — |
| Derive requirements from the revised scenarios and use them to assess design alternatives. | Team (individual owner not assigned) | 2026-10-22 | — |
| Prepare functional block diagrams from the scenario analysis, including registration, monitoring, zone detection, and response for security. | Team (individual owner not assigned) | 2026-10-22 | — |
| Examine the major blocks in more detail, identify sub-blocks, and compare design choices, including background monitoring methods and device options. | Team (individual owner not assigned) | 2026-10-22 | — |
| Incorporate the scenarios, derived requirements, block diagrams, and developing design choices into the living report for discussion with MJ. | Team (individual owner not assigned) | 2026-10-22 | — |
| Align the current specification with the revised scenarios and design direction, and link the update back to this meeting note. | Team (individual owner not assigned) | TBD | [Specification](../planning/specification.md) |

## Open questions

* Which monitoring approach can detect and locate visitors in open hospital areas without requiring active scans?
* How will a detected visitor's identity and location be matched to the hospital map and their permitted green, orange, and red zones? What response should each zone trigger?
  * Perhaps some kind of geospatial data system?
* Should tracking use hospital-issued equipment or personal devices, and how should the design address misleading or tampered tracking information?
* How should the bed-assignment scenario coordinate destination-bed availability and transfer scheduling within a hospital and between hospitals?
  * This is a matter of scope


