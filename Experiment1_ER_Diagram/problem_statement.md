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
<img width="1536" height="1024" alt="er1" src="https://github.com/user-attachments/assets/2e27a507-50e3-4e01-9cc5-93769e6d1d36" />


## Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|----------------------|-------|
| **Member** | **MemberID (PK)**, Name, MembershipType, StartDate | Stores registered gym members. |
| **Program** | **ProgramID (PK)**, ProgramName, Description, Duration | Fitness programs such as Yoga, Zumba, Weight Training. |
| **Trainer** | **TrainerID (PK)**, Name, Specialization, Phone | Trainers assigned to one or more programs. |
| **Member_Program** | **MemberID (PK, FK)**, **ProgramID (PK, FK)**, JoinDate | Associative entity for Member–Program relationship. |
| **Session_Booking** | **BookingID (PK)**, MemberID (FK), TrainerID (FK), SessionDate, SessionTime | Records personal training bookings. |
| **Attendance** | **AttendanceID (PK)**, BookingID (FK), AttendanceStatus | Stores attendance for each booked session. |
| **Payment** | **PaymentID (PK)**, MemberID (FK), BookingID (FK), Amount, PaymentDate, PaymentType | Records membership and session payments. |

---

## Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|-------------|-------------|---------------|-------|
| Member **enrolls in** Program | M : N | Total (Member), Partial (Program) | A member can enroll in multiple programs; each program has many members. |
| Program **assigned to** Trainer | M : N | Total (Program), Partial (Trainer) | A program may have multiple trainers; a trainer can teach multiple programs. |
| Member **books** Session_Booking | 1 : N | Total (Session), Partial (Member) | One member can book many personal training sessions. |
| Trainer **conducts** Session_Booking | 1 : N | Total (Session), Partial (Trainer) | One trainer can conduct many personal training sessions. |
| Session_Booking **has** Attendance | 1 : 1 | Total (Both) | Every booked session has one attendance record. |
| Member **makes** Payment | 1 : N | Total (Payment), Partial (Member) | A member can make multiple payments. |
| Session_Booking **may generate** Payment | 1 : 1 | Partial | Session payment is linked to a booking when applicable. |

---

## Assumptions

- Every member has a unique **MemberID**.
- Every trainer has a unique **TrainerID**.
- Every fitness program has a unique **ProgramID**.
- Members can enroll in multiple fitness programs.
- A fitness program may have one or more trainers.
- Personal training sessions are booked by exactly one member with one trainer.
- Attendance is recorded for every booked session.
- Payments can be for either **Membership** or **Personal Training Session**.
- Membership types (Basic, Premium, Elite, etc.) are predefined.
- A booking cannot exist without both a valid member and a valid trainer.
- Only active members can enroll in programs and book training sessions.
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
<img width="1536" height="1024" alt="er2" src="https://github.com/user-attachments/assets/3d584b06-41ff-46d7-97c6-a4e5f834c2ad" />

## Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|----------------------|-------|
| **Member** | **MemberID (PK)**, Name, Email, Phone, Address, JoinDate | Stores library member information. |
| **Book** | **BookID (PK)**, Title, Author, CategoryID (FK), ISBN, Publisher, Year | Stores details of library books. |
| **Category** | **CategoryID (PK)**, CategoryName, Description | Classifies books into categories. |
| **Book_Loan** | **LoanID (PK)**, MemberID (FK), BookID (FK), LoanDate, DueDate, ReturnDate, Status | Tracks book borrowing and returns. |
| **Fine** | **FineID (PK)**, LoanID (FK), FineAmount, FineDate, PaymentStatus | Stores overdue fines for late returns. |
| **Event** | **EventID (PK)**, EventName, EventDate, EventType, Description | Stores cultural and educational events. |
| **Speaker** | **SpeakerID (PK)**, Name, Profession, ContactNo | Stores speaker/author details. |
| **Event_Speaker** | **EventID (PK, FK)**, **SpeakerID (PK, FK)** | Associative entity connecting events and speakers. |
| **Event_Registration** | **RegistrationID (PK)**, MemberID (FK), EventID (FK), RegistrationDate | Tracks member registrations for events. |
| **Room** | **RoomID (PK)**, RoomName, Capacity, RoomType | Stores library room details. |
| **Room_Booking** | **BookingID (PK)**, RoomID (FK), MemberID (FK), BookingDate, StartTime, EndTime, Purpose | Records room bookings for study or events. |

---

## Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|-------------|-------------|---------------|-------|
| Member **borrows** Book | 1 : N | Total (Book_Loan), Partial (Member) | A member can borrow multiple books. |
| Book **has** Book_Loan | 1 : N | Total (Book_Loan), Partial (Book) | A book can be borrowed multiple times over time. |
| Book **belongs to** Category | N : 1 | Total (Book), Partial (Category) | Every book belongs to one category. |
| Book_Loan **generates** Fine | 1 : 0..1 | Partial (Fine) | A fine is generated only for overdue returns. |
| Member **registers for** Event | M : N | Total (Registration), Partial (Member & Event) | Members can register for multiple events. |
| Event **has** Speaker | M : N | Total (Event), Partial (Speaker) | An event may have multiple speakers/authors. |
| Room **is booked for** Event/Study | 1 : N | Total (Room_Booking), Partial (Room) | Rooms can be booked multiple times. |
| Member **books** Room | 1 : N | Partial (Member) | Members can reserve rooms for study or events. |

---

## Assumptions

- Every member has a unique **MemberID**.
- Every book has a unique **BookID**.
- Every category has a unique **CategoryID**.
- Every event has a unique **EventID**.
- Every speaker has a unique **SpeakerID**.
- A member can borrow multiple books, but a book can be loaned to only one member at a time.
- Overdue fines are generated only when the return date exceeds the due date.
- Members can register for multiple events.
- Each event must have at least one speaker/author.
- Rooms can be booked for either library events or study purposes.
- Room bookings cannot overlap for the same room and time slot.
- All dates and times are stored using the system date and time format.

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
<img width="1672" height="941" alt="er3" src="https://github.com/user-attachments/assets/35ab7b38-ea17-4e8d-b87a-4727abc99ed5" />

## Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|----------------------|-------|
| **Customer** | **CustomerID (PK)**, Name, Phone, Email | Stores customer details. |
| **Reservation** | **ReservationID (PK)**, CustomerID (FK), TableID (FK), WaiterID (FK), ReservationDate, ReservationTime, NoOfGuests, ReservationType (Reserved/Walk-in), Status | Stores reservation and walk-in details. |
| **Table** | **TableID (PK)**, TableNumber, Capacity, Status | Stores restaurant table information. |
| **Waiter** | **WaiterID (PK)**, Name, Phone, Shift | Stores waiter details. |
| **Order** | **OrderID (PK)**, ReservationID (FK), OrderDateTime, OrderStatus | Stores food orders placed for a reservation. |
| **Dish** | **DishID (PK)**, DishName, CategoryID (FK), Price | Stores menu items. |
| **Category** | **CategoryID (PK)**, CategoryName | Categories such as Starter, Main Course, Dessert, Beverage. |
| **Order_Item** | **OrderID (PK, FK)**, **DishID (PK, FK)**, Quantity, UnitPrice | Associative entity between Order and Dish. |
| **Bill** | **BillID (PK)**, ReservationID (FK), FoodCharge, ServiceCharge, Tax, TotalAmount, PaymentStatus | Stores billing information for each reservation. |

---

## Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Customer **makes** Reservation | 1 : N | Total (Reservation), Partial (Customer) | A customer can make multiple reservations. |
| Reservation **allocates** Table | N : 1 | Total (Reservation), Partial (Table) | Each reservation is assigned one table. |
| Waiter **serves** Reservation | 1 : N | Total (Reservation), Partial (Waiter) | One waiter can serve multiple reservations. |
| Reservation **places** Order | 1 : N | Total (Order), Partial (Reservation) | A reservation can have multiple food orders. |
| Order **contains** Dish | M : N | Total (Order), Total (Dish) | Implemented using **Order_Item**. |
| Dish **belongs to** Category | N : 1 | Total (Dish), Partial (Category) | Every dish belongs to one category. |
| Reservation **generates** Bill | 1 : 1 | Total (Both) | One reservation generates one bill. |

---

## Assumptions

- Every customer has a unique **CustomerID**.
- Walk-in customers are also stored as customer records.
- Each reservation is assigned exactly one table.
- A table can have multiple reservations on different dates and times but only one active reservation at a specific time.
- Each reservation is served by one waiter.
- A reservation can have multiple food orders.
- An order contains one or more dishes.
- A dish belongs to exactly one category.
- Bills include food charges, service charges, taxes, and the total amount.
- One bill is generated for each reservation.
- Payment status can be **Pending**, **Paid**, or **Cancelled**.


## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
