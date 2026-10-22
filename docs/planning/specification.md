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
| FR-001 | Authorized administrators shall be able to manage user accounts and assign roles. | Must | An administrator can create, deactivate, and assign roles to accounts. Other users cannot perform these actions. | Proposed |
| FR-002 | The system shall maintain bed/room information, including unit, type, equipment, accessibility, location, and status. | Must | Staff can view these attributes for a bed/room, and saved changes appear when the information is reopened. | Proposed |
| FR-003 | Authorized staff shall be able to update room readiness, including Ready, Cleaning, and Unavailable, while the system reflects active assignments and reservations. | Must | Searches reflect readiness updates and exclude assigned or reserved beds. An empty bed awaiting cleaning remains unavailable until staff mark it Ready. | Proposed |
| FR-004 | Designated admissions staff shall be able to enter accommodation requirements and find suitable, available beds/rooms. | Must | A search returns suitable Ready beds/rooms in the hospital and excludes occupied, reserved, cleaning, and unavailable accommodation. If none are suitable, it reports no available match without making an assignment. | Proposed |
| FR-005 | The system shall provide an AI-assisted bed/room recommendation with an explanation. | Must | For a request with suitable accommodation available, the system recommends a suitable bed/room and explains its recommendation. | Proposed |
| FR-006 | Designated admissions staff shall select the destination bed/room, accepting the recommendation or choosing another suitable bed/room. | Must | Designated admissions staff can confirm either choice and reserve it for the planned transfer. Selection does not change the patient’s current assignment before transfer completion. A patient account cannot select or reserve a bed. | Proposed |
| FR-007 | The system shall record and end current patient assignments and prevent conflicting active assignments to the same bed/room. | Must | A patient has at most one current inpatient bed, and a bed has at most one current patient. A scheduled move preserves the source assignment. Discharge ends the assignment and marks the vacated bed for cleaning. | Proposed |
| FR-010 | The system shall record monitoring events and responses and allow authorized staff to review them. | Must | Records show the observed location, time, associated person when identifiable, zone classification, and any warning, review, or notification. | Proposed |
| FR-011 | The system shall monitor the locations of people registered for monitoring, including visitors, patients, and staff, in the background and allow authorized staff to view their latest observed location and timestamp on a hospital map. | Must | Test movements by a registered visitor, patient, and staff member produce location updates linked to each person’s identity without active scans. Authorized staff can view the latest observations on the map with their timestamps; an old observation is not presented as a fresh location update. | Proposed |
| FR-012 | The system shall provide AI-assisted summaries highlighting unusual movement or access activity for staff review. | Must | A test history containing repeated restricted-zone visits produces a summary highlighting that activity for authorized staff. | Proposed |
| FR-016 | Authorized nurses shall be able to schedule patient transfers and view their records. | Must | A transfer records the patient, source location, reserved destination bed, planned time, responsible nurse, and status: Scheduled, In progress, Completed, or Cancelled. The initial inpatient move can use a treatment bay as its source without requiring a source inpatient assignment. | Proposed |
| FR-017 | The system shall reserve destination beds selected by designated admissions staff and prevent conflicting reservations or assignments. | Must | Reserving a suitable Ready bed excludes it from other patients’ searches and selections. Competing requests cannot both reserve it. During a transfer, the patient may retain a source assignment and a separate destination reservation. | Proposed |
| FR-018 | Authorized nurses shall be able to start and complete scheduled transfers, with completion updating the related bed records together. | Must | A Scheduled transfer can become In progress and then Completed. Completion consumes the destination reservation and establishes the current assignment; any source assignment ends and its bed is marked for cleaning. The update never leaves two current beds or releases the source before completion, and repeated completion does not duplicate the changes. | Proposed |
| FR-020 | Authorized staff shall be able to register visitors, patients, and staff for monitoring and maintain the context needed to evaluate their zone permissions. | Must | A monitoring record links a person’s identity and applicable roles to relevant context: visitor purpose/destination, patient assignment, or staff duties. Reception/admissions staff register patients and visitors; administrators register staff. Reception/admissions staff can close a visitor’s visit, recording departure and ending visit-specific monitoring and permissions while retaining its history. | Proposed |
| FR-022 | The system shall classify observed people’s locations against their applicable zone permissions. | Must | Test observations for registered visitors, patients, and staff produce green, orange, or red classifications according to each person’s roles and situation and are recorded with a timestamp. | Proposed |
| FR-023 | The system shall apply configured zone responses and notify authorized security staff of red-zone events independently of AI summaries. | Must | Green movement is recorded without an alert. An orange event produces the configured warning or review action. A red event creates a security notification with the person’s identity, location, and time without waiting for AI analysis. The response applies to registered visitors, patients, and staff, and authorized staff can record the resulting action. | Proposed |

## 6. Non-functional requirements

| ID | Requirement | Target or acceptance criteria | Status |
|----|----|----|----|
| NFR-001 | Patient information, assignments, transfer records, monitored people’s identities and locations, permissions, and security records shall be protected according to users’ roles. | Users without the required permission cannot view or modify protected information, including through direct requests. Nurses can manage authorized transfers. Being registered for monitoring does not itself grant access to location records, zone rules, or bed reservations; those operations require the appropriate staff permissions. | Proposed |
| NFR-002 | Core staff workflows shall be usable through browsers on PCs and mobile devices. | Room searches, reservations, transfer scheduling and status updates, monitoring registration, visitor-visit management, map viewing, and security-event review can be completed on both screen sizes without missing or inaccessible controls. | Proposed |
| NFR-003 | Confirmed records shall remain available after a system restart. | Saved room information, assignments, reservations, transfer states, monitoring registrations, visitor visits, permissions, timestamped observations, and security records remain intact after restarting the system. | Proposed |
| NFR-004 | Core operations shall remain available when AI assistance is unavailable. | Staff can select and reserve suitable accommodation, manage transfers and room readiness, and review observations. Background monitoring, zone evaluation, and basic security notifications continue without AI. | Proposed |
| NFR-005 | Standard viewing and update operations shall respond promptly. | Room searches, reservations, transfer updates, room-status updates, map views, and security-record views complete within three seconds on the demonstration setup. AI processing is excluded from this initial target. Sensor-to-notification timing will be specified during design. | Proposed |

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
