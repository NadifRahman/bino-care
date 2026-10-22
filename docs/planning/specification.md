# BINO Care specification

**Status:** Draft

This living draft defines the proposed scope, use-case scenarios, and testable requirements for BINO Care.

## 1. Purpose and users

The purpose of BINO Care is to provide a smart building management system for hospitals. It will primarily support two use cases: **bed/room assignment with AI assistance** and **building access management with tracking and AI assistance**.

**Use case 1: Bed/room assignment.** Designated admissions staff enter a patient’s accommodation requirements and review suitable beds/rooms and AI recommendations. They select and reserve the destination, while nurses schedule and track the move. Completing the transfer updates the patient’s current assignment and releases the previous bed for cleaning.

**Use case 2: Building access management and tracking.** The system monitors people registered for monitoring, including visitors, patients, and staff, in the background. It evaluates their locations against permitted, caution, and restricted zones based on their roles and situation. It records movement and security responses, notifies security of restricted-zone events, and uses AI to highlight unusual patterns for staff review.

The primary users are reception and admissions staff, nurses coordinating transfers, hospital staff maintaining room and permission information, and security staff reviewing monitoring events. Patients do not make their own room assignments.

Potential user/role list:

* **Doctors:** Specify patients’ accommodation needs, access permitted clinical areas, and view relevant room information.
* **Nurses:** View patient room assignments, update room information or status, and schedule and record patient transfers, including their progress, completion, and cancellation.
* **Reception and admissions staff:** Register patients and visitors, including their monitoring information and visit permissions, and record arrivals and departures. Designated admissions staff also enter accommodation requirements, review AI recommendations, and select and reserve destination beds/rooms.
* **Patients:** Access their assigned room and other permitted areas. They do not make room assignments.
* **Visitors and caregivers:** Access approved visitor areas and patient areas where permission has been granted.
* **Security staff:** Review monitored people’s locations, monitoring events and security notifications, investigate restricted-zone activity, and review AI summaries of unusual patterns.
* **Housekeeping staff:** View rooms requiring cleaning and update their cleaning or readiness status.
* **Maintenance and facilities staff:** Access relevant service areas and mark rooms as unavailable or ready following maintenance.
* **Laboratory technicians:** Access laboratories and other areas required for their assigned work.
* **System administrators:** Manage user accounts, roles, staff monitoring registrations, hospital map zones, permission rules, and system configuration.

A user may hold multiple roles. Zone permissions depend on the person’s applicable roles and situation, such as staff duties, a patient’s current bed/unit assignment, or a visitor’s permitted destination. Background tracking applies to people registered for monitoring; having a system account alone does not register someone for monitoring.

## 2. Scope

### In scope

* \[TODO Work In Progress\]

### Out of scope

* \[TODO Work In Progress\]

## 3. Use-case scenarios

### 3.1. Inpatient bed assignment

A construction worker arrives in the ER after an accident. After treatment, the doctor requests an inpatient bed with suitable equipment and accessibility. Admissions enters these needs into BINO Care, which excludes occupied, reserved, cleaning, and unavailable beds and explains its recommendation. Admissions reserves a suitable bed; a nurse schedules the move from the treatment bay and records its progress and completion.

The next day, the patient needs a different unit. Admissions reserves another bed, and a nurse schedules the transfer. The existing assignment remains active until the move is completed. BINO Care then updates the current bed and permissions and marks the previous bed for cleaning. Staff must confirm it is ready before reuse. Cancelling a scheduled move releases the destination reservation and preserves the existing assignment.

### 3.2. Visitor monitoring and security response

A visitor registers at reception to visit a patient. Staff record the visit and permitted destination, linking the visitor’s tracking identity to green, orange, and red zones. As the visitor walks through open hospital areas, background monitoring records their location and time without requiring active scans and shows the latest observation on a hospital map.

Movement in green areas is recorded without an alert. An orange-area detour prompts a proportionate warning or review; entry into a red area notifies security with the visitor, location, and time. AI may highlight repeated unusual movement for review. On departure, reception closes the visit and revokes its temporary permissions and identifier association.

## 4. System context

BINO Care will be accessible through a web application using browsers on both PCs and mobile devices. It will receive background location observations from a monitoring solution and relate them to registered people’s identities and applicable zones on a hospital map. It may also interact with room-occupancy sensors. Tracking hardware, communication methods, and hosting choices will be determined during design.

## 5. Functional requirements

| ID | Requirement | Priority | Acceptance criteria | Status |
|----|----|----|----|----|
| FR-001 | Authorized administrators shall be able to manage user accounts and assign roles. | Must | Admins can create or deactivate accounts and assign roles; other users cannot. | Proposed |
| FR-002 | The system shall maintain bed/room information, including unit, type, equipment, accessibility, location, and status. | Must | Staff can view unit, type, equipment, accessibility, location, and status; saved edits persist. | Proposed |
| FR-003 | Authorized staff shall be able to update room readiness, including Ready, Cleaning, and Unavailable, while the system reflects active assignments and reservations. | Must | Searches reflect readiness changes and omit assigned or reserved beds. Beds awaiting cleaning stay unavailable until marked Ready. | Proposed |
| FR-004 | Designated admissions staff shall be able to enter accommodation requirements and find suitable, available beds/rooms. | Must | Searches return suitable Ready beds and omit occupied, reserved, cleaning, or unavailable beds. If none fit, the system reports no match and makes no assignment. | Proposed |
| FR-005 | The system shall provide an AI-assisted bed/room recommendation with an explanation. | Must | The system recommends a suitable bed/room and explains why. | Proposed |
| FR-006 | Designated admissions staff shall select the destination bed/room, accepting the recommendation or choosing another suitable bed/room. | Must | Admissions staff can accept the recommendation or choose another suitable bed/room to reserve. The patient keeps the current assignment until transfer completion; patient accounts cannot select or reserve beds. | Proposed |
| FR-007 | The system shall record and end current patient assignments and prevent conflicting active assignments to the same bed/room. | Must | A patient has at most one current bed, and a bed has at most one current patient. Scheduled moves keep the source assignment; discharge ends it and marks the bed for cleaning. | Proposed |
| FR-010 | The system shall record monitoring events and responses and allow authorized staff to review them. | Must | Each record shows location, time, person when identified, zone, and any warning, review, or notification. | Proposed |
| FR-011 | The system shall monitor the locations of people registered for monitoring, including visitors, patients, and staff, in the background and allow authorized staff to view their latest observed location and timestamp on a hospital map. | Must | Test movements by registered visitors, patients, and staff update their identity-linked map locations without active scans. Authorized staff see the latest location and timestamp; stale observations are not shown as current. | Proposed |
| FR-012 | The system shall provide AI-assisted summaries highlighting unusual movement or access activity for staff review. | Must | A history with repeated restricted-zone visits produces a summary for authorized staff. | Proposed |
| FR-016 | Authorized nurses shall be able to schedule patient transfers and view their records. | Must | Each transfer lists the patient, source, reserved destination, planned time, nurse, and status (Scheduled, In progress, Completed, or Cancelled). The initial move may start from a treatment bay without a source inpatient-bed assignment. | Proposed |
| FR-017 | The system shall reserve destination beds selected by designated admissions staff and prevent conflicting reservations or assignments. | Must | A reserved Ready bed is excluded from other searches and selections. Competing requests cannot reserve it, and the patient keeps the source assignment during the transfer. | Proposed |
| FR-018 | Authorized nurses shall be able to start and complete scheduled transfers, with completion updating the related bed records together. | Must | A transfer moves from Scheduled to In progress to Completed. Completion uses the reservation, assigns the destination, ends the source assignment, and marks its bed for cleaning. It cannot release the source early, leave two current beds, or apply completion twice. | Proposed |
| FR-020 | Authorized staff shall be able to register visitors, patients, and staff for monitoring and maintain the context needed to evaluate their zone permissions. | Must | Records link identity and roles to visitor purpose/destination, patient assignment, or staff duties. Reception/admissions register visitors and patients; admins register staff. Closing a visit records departure and ends visit monitoring and permissions while keeping its history. | Proposed |
| FR-022 | The system shall classify observed people’s locations against their applicable zone permissions. | Must | Recorded observations include a timestamp and a green, orange, or red classification based on the person’s role and situation. | Proposed |
| FR-023 | The system shall apply configured zone responses and notify authorized security staff of red-zone events independently of AI summaries. | Must | Green movement is logged without an alert; orange triggers its configured warning or review; red notifies security with identity, location, and time, without AI. Authorized staff can record their response. | Proposed |

## 6. Non-functional requirements

| ID | Requirement | Target or acceptance criteria | Status |
|----|----|----|----|
| NFR-001 | Patient information, assignments, transfer records, monitored people’s identities and locations, permissions, and security records shall be protected according to users’ roles. | Users without permission cannot view or change protected data, including through direct requests. Nurses can manage authorized transfers. Monitoring registration alone grants no access to location records, zone rules, or bed reservations. | Proposed |
| NFR-002 | Core staff workflows shall be usable through browsers on PCs and mobile devices. | Room searches, reservations, transfer scheduling and status updates, monitoring registration, visitor visit management, map viewing, and event review work on PC and mobile without missing or inaccessible controls. | Proposed |
| NFR-003 | Confirmed records shall remain available after a system restart. | Room data, assignments, reservations, transfers, monitoring records, visits, permissions, observations, and security records remain after restart. | Proposed |
| NFR-004 | Core operations shall remain available when AI assistance is unavailable. | Without AI, staff can select and reserve beds, manage transfers and readiness, and review observations. Background monitoring, zone checks, and basic security alerts continue. | Proposed |
| NFR-005 | Standard viewing and update operations shall respond promptly. | Room searches, reservations, transfer and room-status updates, map views, and security records respond within three seconds on the demo setup. AI is excluded; sensor-to-notification timing will be set during design. | Proposed |

## 7. Constraints and assumptions

* The project must follow course deadlines and fit the team’s budget.
* Hardware, tracking technology, communication methods, AI implementation, and hosting choices are still to be determined.
* The prototype covers one hospital with a small set of rooms, patients, visitors, and staff and uses simulated patient data.
* Staff supply accommodation requirements and clinical readiness decisions. The system supports coordination; staff perform the physical move and record its status.
* Nurses handle transfers in the prototype. A separate transport-staff role is not required.
* A reservation holds the destination bed; it does not establish the patient’s current bed or confirm that the patient has arrived.
* Background monitoring reports observations within the configured coverage area. Its accuracy and coverage must be established during design.
* Network connectivity is assumed during normal operation.

## 8. Open questions

* Which background tracking technology and identity-association method should be used: automatically read identifiers, cameras, or another approach?
* What coverage, location accuracy, observation freshness, and sensor-to-notification delay can the demonstration setup support?
* How should the hospital map represent zones, boundaries, and uncertain or missing location observations?
* What orange-zone warning/review thresholds and red-zone escalation, acknowledgement, and repeat-notification rules should be configured?
* Should people registered for monitoring use hospital-issued equipment or personal devices, and how should missing or misleading tracking information be handled?
* How should zone permissions be resolved when someone has multiple roles or changes situation, such as a staff member becoming a patient?
* Which AI approach should support bed recommendations and activity summaries, and how should its output be evaluated?
* Should the prototype include optional room-occupancy sensors, and at which locations?
