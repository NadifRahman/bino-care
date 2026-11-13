# BINO Care — User Interface Design

This file contains the preliminary user interface (UI) design for the BINO Care smart hospital platform. It describes the primary staff-facing workflows, proposed screens, and the relationship between UI actions and the software platform's data model.

The UI is planned as a responsive web application accessible through desktop and mobile browsers. It provides authorized hospital personnel with interfaces for inpatient bed assignment and transfer, visitor monitoring, and security response.

## High-Level UI Modules

The preliminary UI is organized around two primary operational workflows:

1. **Inpatient Bed Assignment and Transfer** — supports admissions staff and nurses in finding and reserving suitable beds, scheduling patient moves, recording transfer completion, and handling discharge.
2. **Visitor Monitoring and Security Response** — supports reception staff in registering visitors and their permitted destinations, and security personnel in reviewing location observations and responding to zone-based security events.

The main staff dashboard provides navigation to these workflows. Access to screens and actions is controlled by the signed-in person's account and assigned roles.

## UI Workflow Diagram

!\[BINO Care UI workflow diagram]

This will be included at some point in the future.

## 1\. Inpatient Bed Assignment and Transfer

**Primary users:** Admissions staff and nurses.

**Objective:** Find and reserve a suitable inpatient bed, schedule a patient move, and update the assignment only when the move is completed.

### Proposed screens

|Screen|Main UI purpose|Related data|
|-|-|-|
|Bed Management|Show bed readiness and current availability; start a bed search|`bed`, `bed\_assignment`|
|Patient Requirements|Enter the patient's identity and required unit, equipment, and accessibility needs|`person`, `bed`|
|Bed Recommendations|Display matching beds and explain why beds are excluded or recommended|`bed`, `bed\_assignment`|
|Reservation Confirmation|Confirm a selected bed reservation|`bed\_assignment`, `user\_account`|
|Transfer Management|Schedule, view, and update a patient's move|`transfer`, `bed\_assignment`, `zone`, `user\_account`|
|Discharge / Bed Release|End the active stay and show the bed as awaiting cleaning|`bed\_assignment`, `bed`|

### Workflow and backend alignment

1. Admissions staff open Bed Management and enter patient requirements.
2. The backend uses the patient and bed information to find suitable beds. Beds that are not Ready or have an active Reserved or Occupied assignment are not offered.
3. Admissions reviews the recommendations and reserves a selected bed. The bed assignment is created in the **Reserved** state.
4. A nurse schedules the move. The transfer records the destination assignment, source (the current bed assignment or a zone such as a treatment bay), scheduling nurse, and planned time.
5. The nurse updates the transfer as it progresses through **Scheduled**, **In progress**, and **Completed**, or marks it **Cancelled**.
6. Until the move is completed, the existing bed assignment remains active and the destination bed remains reserved.
7. On completion, the destination assignment becomes **Occupied**. If the patient moved from another bed, the previous assignment ends and that bed becomes **Cleaning**.
8. If the transfer is cancelled, the destination reservation is released and the existing assignment remains unchanged. On discharge, the current assignment ends and its bed becomes **Cleaning**.

The UI must distinguish a reservation from actual occupancy. It must not display a newly reserved bed as occupied until a nurse confirms the patient's arrival.

## 2\. Visitor Monitoring and Security Response

**Primary users:** Reception staff and security personnel.

**Objective:** Register a visitor and permitted destination, associate a tracking identifier for the visit, display location observations on the hospital map, and support proportionate security responses to zone activity.

### Proposed screens

|Screen|Main UI purpose|Related data|
|-|-|-|
|Visitor Registration|Identify or create a visitor and record the visit and permitted destination|`person`, `visit`, `zone`|
|Tracking Setup|Associate the tracking identifier with the visitor for the visit period|`tracking\_identifier`, `tracking\_registration`, `visit`|
|Visitor Monitoring Map|Display floors, zones, permitted destinations, and latest available location observations|`floor`, `zone`, `role\_zone\_rule`, `location\_observation`|
|Security Events|Display warnings, notifications, and relevant observation details|`security\_event`, `location\_observation`|
|Security Event Details|Allow authorized personnel to review an event and record a response|`security\_event`, `user\_account`|
|Visit Closure|End the visit and temporary tracking association|`visit`, `tracking\_registration`|

### Workflow and backend alignment

1. Reception staff register the visitor and record the permitted destination and visit arrival information.
2. The tracking identifier is associated with the visitor through a time-bounded tracking registration, optionally linked to the visit.
3. The monitoring map displays the hospital floors and zones, together with the latest location observations received by the platform.
4. The backend resolves each observation against the tracking registration valid at the observation's capture time and applies the applicable role-zone rule and visit destination permissions.
5. Green observations are recorded without an alert. Orange observations can prompt a warning or review. Red observations trigger a security notification.
6. Security personnel review relevant events and record their response where applicable. AI-generated indications of repeated unusual movement, if implemented, are supporting information for staff review.
7. When the visitor leaves, reception closes the visit. The visit's temporary permission ends and its tracking registration is ended so later use of the same identifier is not associated with the previous visit.

The map should distinguish the visitor's latest observation from historical movement records. It should also make clear when an observation is unresolved or when its location cannot be confidently assigned to a zone.

## UI and Data Model Considerations

* **Role-aware access:** The signed-in staff member's role determines which screens and actions are available. A visitor does not need a user login merely to be registered and monitored.
* **Backend-owned state:** The UI requests operations and displays backend results. It should not independently decide whether a bed is available, whether a transfer is complete, or what zone colour applies.
* **Reservation and transfer consistency:** The UI must preserve the current assignment until the transfer is completed and show cancellation or delayed-transfer states clearly.
* **Person-specific zone permissions:** The map and event details should display the resolved classification for the tracked person, not assume that a physical zone always has one universal colour.
* **Time-aware tracking:** Location observations must be associated with the tracking registration valid at the time the observation was captured.
* **Privacy and security:** Visitor identities, tracking details, patient information, and security events should only be visible to authorized personnel.
* **Responsive layout:** The web interface should support desktop and mobile browser layouts.

## Scope and Dependencies

The UI depends on backend services for authentication, bed matching and reservation, transfer state changes, visit and tracking registration, map and zone data, location observations, and security events.

The visitor map displays observations supplied by the separate monitoring solution. The web application is not assumed to perform continuous background tracking itself. The exact tracking hardware, communication method, hosting arrangement, and location-observation format remain part of the wider system design.

Detailed visual styling and implementation will be refined after the team confirms the backend API contracts and the data supplied by the monitoring hardware.

