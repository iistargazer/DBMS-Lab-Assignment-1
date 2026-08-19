# DBMS-Lab-Assignment-1

# Question 1 — University Course Registration
Issue 1: Direct ENROLLS relationship between Student and Course
1. Flaw: Missing the Section entity concept.
2. Information Loss: Students register for generic courses rather than specific offerings/sections running in a
given semester.
3. Minimal ER Correction: Introduce a Section entity between Course and Student, shifting ENROLLS to link
Student to Section.

Issue 2: Semester and Year stored as attributes of Course
1. Flaw: Temporal course attributes placed directly on static Course entity.
2. Information Loss: Prevents offering the same course across multiple semesters/years without duplicating
course master records.
3. Minimal ER Correction: Relocate Semester and Year attributes from Course to the new Section entity.
   
Issue 3: TEACHES relationship connects Instructor directly to Course
1. Flaw: Instructor assigned at course level instead of section level.
2. Information Loss: Cannot represent different instructors teaching different sections of the same course.
3. Minimal ER Correction: Re-anchor the TEACHES relationship from Instructor to Section instead of
Course.

Issue 4: HELD_IN relationship connects Classroom directly to Course
1. Flaw: Physical room scheduling attached to course master.
2. Information Loss: Classroom allocations are static per course, so different sections cannot be scheduled in
different rooms.
3. Minimal ER Correction: Re-anchor HELD_IN relationship to connect Classroom to Section.


# Question 2 — Hospital Prescription System
Issue 1: Binary relationships used for Prescription tracking
1. Flaw: Independent PRESCRIBES, TAKES, and CONSULTS binary relationships.
2. Information Loss: Cannot correlate which doctor prescribed which medicine to which patient during a specific
visit.
3. Minimal ER Correction: Replace disconnected binary relationships with a central Consultation /
Prescription entity (or ternary entity) linking Patient, Doctor, and Medicine.

Issue 2: Dosage stored as an attribute of Medicine
1. Flaw: Dosage defined globally on the medicine master record.
2. Information Loss: Dosage becomes static across all patients and visits, ignoring patient-specific dosage
requirements.
3. Minimal ER Correction: Move Dosage attribute from Medicine to the Prescription / PrescribedItem
relationship.

Issue 3: Missing time-dependent instruction attributes
1. Flaw: Temporal and execution details missing from prescriptions.
2. Information Loss: Cannot record re-prescriptions or distinct frequency/duration parameters over time.
3. Minimal ER Correction: Add Frequency, Duration, and PrescriptionDate attributes to the
Prescription entity.

Issue 4: Inability to log repeated patient-doctor visits
1. Flaw: CONSULTS is modeled as a simple binary relationship without visit identifiers.
2. Information Loss: History of multiple consultations between the same patient and doctor is overwritten or
lost.
3. Minimal ER Correction: Model Consultation as a distinct entity with ConsultationID and VisitDate
attributes.

# Question 3 - E-Commerce Order Fulfilment
Issue 1: Quantity stored directly on Product entity
1. Flaw: Quantity is placed on the catalog item rather than line items.
2. Information Loss: Represents generic inventory stock rather than individual order item quantities.
3. Minimal ER Correction: Move Quantity to an OrderLine / OrderItem entity (or onto the CONTAINS
relationship).

Issue 2: ShippingAddress stored on Customer entity
1. Flaw: Delivery address anchored to customer master profile.
2. Information Loss: Overwrites historical addresses and prevents specifying distinct delivery addresses per
order.
3. Minimal ER Correction: Relocate ShippingAddress to Order (or link Order to a separate Address
entity).

Issue 3: ShipmentDate placed on Order entity and direct Order-Shipment link
1. Flaw: Assumes 1-to-1 fulfillment event per entire order.
2. Information Loss: Cannot handle split shipments across multiple dates or track individual dispatch dates.
3. Minimal ER Correction: Move dispatch date to Shipment entity and establish a 1-to-many relationship from
Order to Shipment.

Issue 4: Shipments linked to Order rather than Order Items / Warehouses
1. Flaw: Fulfillment linked to header level instead of item level.
2. Information Loss: Partial fulfillment where different line items ship from different warehouses cannot be
tracked.
3. Minimal ER Correction: Link Shipment and Warehouse to OrderLine via a ShipmentLine entity
containing ShippedQuantity

# Question 4 — Project Staffing and Roles
Issue 1: Role stored as an attribute of Employee
1. Flaw: Job role attached directly to the employee record.
2. Information Loss: An employee is constrained to a single global role and cannot take on different roles on
different projects.
3. Minimal ER Correction: Move Role attribute from Employee to the WORKS_ON relationship (or Assignment
entity).

Issue 2: HoursWorked stored directly on Project
1. Flaw: Aggregated hours placed on the project entity.
2. Information Loss: Cannot track hours logged per employee-project pair or track hours over distinct time
periods.
3. Minimal ER Correction: Move HoursWorked to WORKS_ON (or a WorkLog entity) with a TimePeriod/Date
attribute.

Issue 3: Binary WORKS_ON relationship lacks temporal tracking
1. Flaw: Stateless relationship between Employee and Project.
2. Information Loss: Cannot track historical start/end dates or rejoin history when an employee leaves and
rejoins a project.
3. Minimal ER Correction: Promote WORKS_ON to a ProjectAssignment entity with StartDate and
EndDate.

Issue 4: Direct MANAGED_BY relationship without historical retention
1. Flaw: Single pointer to current project manager.
2. Information Loss: Changing project managers overwrites previous management history required for auditing.
3. Minimal ER Correction: Replace MANAGED_BY with a ProjectManagementHistory entity with
StartDate and EndDate attributes.

# Question 5 — Airline Booking and Seat Assignment
Issue 1: Flight mixes schedule master data with specific dates
1. Flaw: Flight entity combines route schedule metadata with instance date/time.
2. Information Loss: Cannot represent recurring flight schedules operating across multiple dates independently.
3. Minimal ER Correction: Separate into FlightSchedule (Route info) and FlightInstance (Date,
Departure Time).

Issue 2: Missing Booking / PNR entity
1. Flaw: BOOKS connects Passenger directly to Flight.
2. Information Loss: Cannot group multiple passengers onto a single booking reservation (PNR) or track multileg itineraries.
3. Minimal ER Correction: Introduce a Booking (PNR) entity linked to Passenger and FlightSegment.
   
Issue 3: USES links Aircraft directly to abstract Flight schedule
1. Flaw: Aircraft assignment fixed at abstract flight schedule level.
2. Information Loss: Aircraft swaps for a specific daily flight instance alter the whole schedule definition.
3. Minimal ER Correction: Move USES relationship to link Aircraft to FlightInstance.
   
Issue 4: SEATED_ON connects Passenger directly to Aircraft
1. Flaw: Seat assignment decoupled from flight instances/segments.
2. Information Loss: Passengers cannot hold different seat assignments across different segments or dates.
3. Minimal ER Correction: Link seat assignment to Passenger + FlightInstance (or a BoardingPass
entity with SeatNumber).


