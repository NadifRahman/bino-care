# Wardkeeper specification

**Status:** Draft

This document defines the agreed scope and testable requirements for Wardkeeper

## 1. Purpose and users

The purpose of Wardkeeper is to provide a smart building management system for hospitals. It will primarily support two use cases: **bed/room assignment with AI assistance** and **building access management with tracking and AI assistance**.

**Use case 1: Bed/room assignment.** Designated hospital staff (such as a doctor) enter a patient’s accommodation requirements and use current room information to find suitable accommodation. AI provides a recommendation and explanation, while the staff member makes the final assignment.

**Use case 2: Building access management and tracking.** The system controls access to hospital spaces according to users’ permissions and patient room assignments. It records access activity and uses AI to highlight unusual patterns for staff review.

The primary users are designated staff responsible for room assignments, hospital staff who maintain room and access information, and security staff who review access activity. Patients do not make their own room assignments.

Potential user/role list:

- **Room assignment staff:** Designated personnel who enter accommodation requirements, review AI recommendations, and make final bed/room assignments.
- **Doctors:** Access permitted clinical areas and view relevant room information. They may also hold the bed/room assignment role if designated.
- **Nurses:** View patient room assignments and update room information or status.
- **Reception and admissions staff:** Register patients, manage assigned access credentials, and record arrivals and departures.
- **Patients:** Access their assigned room and other permitted areas. They do not make room assignments.
- **Visitors and caregivers:** Access approved visitor areas and patient areas where permission has been granted.
- **Security staff:** Review access attempts, investigate denied access, and review AI summaries of unusual activity.
- **Housekeeping staff:** View rooms requiring cleaning and update their cleaning or readiness status.
- **Maintenance and facilities staff:** Access relevant service areas and mark rooms as unavailable or ready following maintenance.
- **Laboratory technicians:** Access laboratories and other areas required for their assigned work.
- **System administrators:** Manage user accounts, roles, access points, and system configuration.

A user may hold multiple roles. Permissions depend on their assigned roles.

## 2. Scope

### In scope

* [TODO Work In Progress]

### Out of scope

* [TODO Work In Progress]

## 3. System context

Wardkeeper will be accessible through a web application using browsers on both PCs and mobile devices. It may also interact with IoT devices installed in the hospital.

## 4. Functional requirements

| ID | Requirement | Priority | Acceptance criteria | Status |
|----|----|----|----|----|
| FR-001 | Authorized administrators shall be able to manage user accounts and assign roles. | Must | An administrator can create, deactivate, and assign roles to accounts. Other users cannot perform these actions. | Proposed |
| FR-002 | The system shall maintain bed/room information, including type, equipment, accessibility, location, and status. | Must | Staff can view these attributes for a bed/room, and saved changes appear when the information is reopened. | Proposed |
| FR-003 | Authorized staff shall be able to update room status, including Ready, Occupied, Cleaning, and Unavailable. | Must | A permitted user can change a room’s status, and the updated status is reflected in room searches. | Proposed |
| FR-004 | Designated room assignment staff shall be able to enter accommodation requirements and find suitable, available beds/rooms. | Must | A search returns beds/rooms that meet the entered requirements and excludes occupied or unavailable accommodation. | Proposed |
| FR-005 | The system shall provide an AI-assisted bed/room recommendation with an explanation. | Must | For a request with suitable accommodation available, the system recommends a suitable bed/room and explains its recommendation. | Proposed |
| FR-006 | Designated staff shall make the final room assignment, accepting the recommendation or choosing another suitable bed/room. | Must | Designated staff can confirm either choice. A patient account cannot make an assignment. | Proposed |
| FR-007 | The system shall record and end patient assignments and prevent conflicting active assignments to the same bed/room. | Must | An assigned bed/room cannot receive a conflicting assignment. Staff can end an assignment and update the room’s status. | Proposed |
| FR-008 | Authorized staff shall be able to assign, revoke, and reassign access credentials. | Must | An assigned credential identifies its current user. A revoked credential no longer grants access, and a reassigned credential uses the new user’s permissions. | Proposed |
| FR-009 | The system shall grant or deny access according to configured permissions, including user roles and patient room assignments. | Must | A permitted user is granted access. An unauthorized user is denied access. Patients can access their assigned room and permitted public areas. | Proposed |
| FR-010 | The system shall record access attempts and allow authorized staff to review them. | Must | Successful and denied attempts appear with the access point, time, outcome, and associated user when identifiable. | Proposed |
| FR-011 | The system shall track user locations and allow authorized staff to view the latest available location and its timestamp. | Should | When a location update is recorded, authorized staff can view the updated location and time. The tracking method will be determined during design. | Proposed |
| FR-012 | The system shall provide AI-assisted summaries highlighting unusual access activity for staff review. | Must | A test history containing repeated denied attempts produces a summary highlighting that activity for authorized staff. | Proposed |
| FR-013 | The system shall immediately update a patient’s assignment-based access permissions when their room assignment is confirmed, changed, or ended. | Must | Following confirmation, access decisions reflect the current assignment. A previous or ended assignment no longer grants access to that room. | Proposed |
| FR-014 | Users shall receive clear feedback when an access attempt fails, distinguishing a permission denial from a technical or communication failure. | Must | An unauthorized attempt displays an access-denied message. An attempt that cannot be verified due to a technical or communication failure displays an appropriate error rather than incorrectly reporting a permission denial. | Proposed |
| FR-015 | The system shall monitor room occupancy and make detected occupancy available to authorized staff and the room assignment system, separately from room readiness. | Could | A detected occupancy change is reflected in the room’s occupancy information. Detecting that a room is empty does not automatically mark it as Ready. | Proposed |

## 5. Non-functional requirements

| ID | Requirement | Target or acceptance criteria | Status |
|----|----|----|----|
| NFR-001 | Patient information, assignments, and access records shall be protected according to users’ roles. | Users without the required permission cannot view or modify protected information, including through direct requests to the system. | Proposed |
| NFR-002 | Core staff workflows shall be usable through browsers on PCs and mobile devices. | Room searches, assignments, status updates, and access-record review can be completed on both screen sizes without missing or inaccessible controls. | Proposed |
| NFR-003 | Confirmed records shall remain available after a system restart. | Saved room information, assignments, access permissions, and access records remain intact after restarting the system. | Proposed |
| NFR-004 | Core operations shall remain available when AI assistance is unavailable. | Staff can manually assign suitable accommodation, manage room status, and use access control while the AI service is unavailable. | Proposed |
| NFR-005 | Standard viewing and update operations shall respond promptly. | Room searches, status updates, and access-record views complete within three seconds on the demonstration setup. AI processing is excluded from this initial target. | Proposed |

## 6. Constraints and assumptions

- The project must follow course deadlines and fit the team’s budget.
- Hardware and hosting choices are still to be determined.
- We assume the prototype will use a small set of rooms and users with simulated patient data.
- Network connectivity is assumed during normal operation.

## 7. Open questions

* What level of tracking is required for users? Mobile tracking devices, RFID scanners?