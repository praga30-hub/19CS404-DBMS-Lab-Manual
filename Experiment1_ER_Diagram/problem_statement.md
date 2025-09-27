# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
*Paste or attach your diagram here*  
![ER Diagram](er_diagram_fitness.png)

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|              |            |               |       |
|              |            |               |       |
|              |            |               |       |

### Assumptions
- 
- 
- 

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
 
<img width="599" height="332" alt="image" src="https://github.com/user-attachments/assets/a79f8002-e4e6-479b-bf38-903b16fb9ee3" />


### Entities and Attributes

| Entity | Attributes (PK, FK)                   | Notes |
|--------|---------------------------------------|-------|
|Member  |Member_ID(PK),Name,Email,Phone         |stores detail of library members     |
|Book    |Book_ID(PK),Title,Author,Category      |Stores information of books       |
|Loan    |Loan_Id(PK)Loan_Date, Return_Date, Fine_Amount, Member_ID (FK), Book_ID (FK)        |Records book borrowing and returning       |
|Event   |Event_ID (PK), Event_Name, Event_Date, Type, Room_ID (FK)| Stores event details      |
|Speaker |Speaker_ID (PK), Name, Profession, Expertise|Event speaker details|
|Room    |Room_ID (PK), Room_Name, Capacity, Type|Rooms used for events|
|Registration|Reg_ID (PK), Member_ID (FK), Event_ID (FK)|Tracks event registrations by members |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Member – Loan             |1 : N            | Member (1,1), Loan (0,N)              |   One member can have many loans; each loan belongs to only one member.    |
|   Book – Loan           |   1 : N         |   Book (1,1), Loan (0,N)            |  One book can appear in many loans; each loan is for one book.     |
| Member – Event (via Registration)             |  M : N          |  Member (0,N), Event (0,N)             | Many-to-many resolved through Registration entity.      |
|  Event – Speaker           |M : N| Event (0,N), Speaker (0,N)|An event can have many speakers, and speakers can participate in multiple events.|
| Event – Room    |N : 1| Event (1,1), Room (0,N)|Each event takes place in one room; a room can host many events at different times.|

### Assumptions
- Unique Identifiers: Every entity has a unique primary key (e.g., Member_ID, Book_ID, Loan_ID, Event_ID, Speaker_ID, Room_ID, Reg_ID).
- One Active Loan per Book: A book can only be borrowed in one loan at a time; it cannot be issued to multiple members simultaneously.
- Membership Requirement: Only registered members are allowed to borrow books and register for events.
- Loan Rules: Each loan must be linked to exactly one member and one book.
- Events and Rooms: An event must take place in exactly one room, but a room can host multiple events (not at the same time).
- Speakers: A speaker may participate in multiple events, and an event can have multiple speakers.
- Registrations: Event registrations are done only through members, and one member can register for many events.
- Fines: Fine_Amount in the Loan entity is calculated based on library policy if the book is returned late.
- Event Scheduling: Two events cannot be scheduled in the same room at the same time.
- Data Consistency: Attributes like Email, Phone, and Event_Date are assumed to follow valid formats.
---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
*Paste or attach your diagram here*  
![ER Diagram](er_diagram_restaurant.png)

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|              |            |               |       |
|              |            |               |       |
|              |            |               |       |

### Assumptions
- 
- 
- 

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
