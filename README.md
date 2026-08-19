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

erDiagram
    COURSE ||--|{ SECTION : HAS
    SECTION ||--|{ ENROLLMENT : HAS
    STUDENT ||--|{ ENROLLMENT : ENROLLS_IN
    INSTRUCTOR ||--o{ SECTION : TEACHES
    CLASSROOM ||--o{ SECTION : HOSTS

    COURSE {
        string CourseID PK
        string Title
        int Credits
    }
    SECTION {
        string SectionNo PK
        string Semester
        int Year
    }
    STUDENT {
        string StudentID PK
        string Name
        string Email
    }
    ENROLLMENT {
        string Grade
    }
    INSTRUCTOR {
        string InstructorID PK
        string Name
    }
    CLASSROOM {
        string RoomNo PK
        string Building
    }
