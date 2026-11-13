# ui.md
BINO Care — User Interface Design
This file contains the preliminary user interface (UI) design for the BINO Care smart hospital platform. It describes the primary staff-facing workflows, proposed screens, and the relationship between UI actions and the software platform's data model.

The UI is planned as a responsive web application accessible through desktop and mobile browsers. It provides authorized hospital personnel with interfaces for inpatient bed assignment and transfer, visitor monitoring, and security response.
High-Level UI Modules
The preliminary UI is organized around two primary operational workflows:
1. Inpatient Bed Assignment and Transfer
2. Visitor Monitoring and Security Response
The main staff dashboard provides navigation to these workflows. Access to screens and actions is controlled by the signed-in person's account and assigned roles.
UI Workflow Diagram

Note: Will add svg in here later.
1. Inpatient Bed Assignment and Transfer
Primary users: Admissions staff and nurses.

Objective: Find and reserve a suitable inpatient bed, schedule a patient move, and update the assignment only when the move is completed.
Proposed screens
Screen	Main UI purpose	Related data
Bed Management	Show bed readiness and current availability; start a bed search	bed, bed_assignment
Patient Requirements	Enter the patient's identity and required unit, equipment, and accessibility needs	person, bed
Bed Recommendations	Display matching beds and explain why beds are excluded or recommended	bed, bed_assignment
Reservation Confirmation	Confirm a selected bed reservation	bed_assignment, user_account
Transfer Management	Schedule, view, and update a patient's move	transfer, bed_assignment, zone, user_account
Discharge / Bed Release	End the active stay and show the bed as awaiting cleaning	bed_assignment, bed

The UI must distinguish a reservation from actual occupancy. It must not display a newly reserved bed as occupied until a nurse confirms the patient's arrival.
2. Visitor Monitoring and Security Response
Primary users: Reception staff and security personnel.

Objective: Register a visitor and permitted destination, associate a tracking identifier for the visit, display location observations on the hospital map, and support proportionate security responses to zone activity.
Proposed screens
Screen	Main UI purpose	Related data
Visitor Registration	Identify or create a visitor and record the visit and permitted destination	person, visit, zone
Tracking Setup	Associate the tracking identifier with the visitor for the visit period	tracking_identifier, tracking_registration, visit
Visitor Monitoring Map	Display floors, zones, permitted destinations, and latest available location observations	floor, zone, role_zone_rule, location_observation
Security Events	Display warnings, notifications, and relevant observation details	security_event, location_observation
Security Event Details	Allow authorized personnel to review an event and record a response	security_event, user_account
Visit Closure	End the visit and temporary tracking association	visit, tracking_registration

The map should distinguish the visitor's latest observation from historical movement records. It should also make clear when an observation is unresolved or when its location cannot be confidently assigned to a zone.
UI and Data Model Considerations
- Role-aware access: The signed-in staff member's role determines which screens and actions are available. A visitor does not need a user login merely to be registered and monitored.
- Backend-owned state: The UI requests operations and displays backend results. It should not independently decide whether a bed is available, whether a transfer is complete, or what zone colour applies.
- Reservation and transfer consistency: The UI must preserve the current assignment until the transfer is completed and show cancellation or delayed-transfer states clearly.
- Person-specific zone permissions: The map and event details should display the resolved classification for the tracked person, not assume that a physical zone always has one universal colour.
- Time-aware tracking: Location observations must be associated with the tracking registration valid at the time the observation was captured.
- Privacy and security: Visitor identities, tracking details, patient information, and security events should only be visible to authorized personnel.
- Responsive layout: The web interface should support desktop and mobile browser layouts.
