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
<img width="1612" height="1035" alt="image" src="https://github.com/user-attachments/assets/aea42e43-9a23-4e35-8bf4-837463a3a93f" />


### Entities and Attributes

<img width="845" height="430" alt="image" src="https://github.com/user-attachments/assets/f0c7750b-1977-4914-b211-e856139aa8ba" />


### Relationships and Constraints

<img width="691" height="376" alt="image" src="https://github.com/user-attachments/assets/808dd01b-690b-4529-845a-f7e93057d223" />


### Assumptions

- A member can join multiple programs.
- Trainers can be assigned to multiple programs.
- Personal training sessions always involve one trainer and one member.

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
<img width="887" height="515" alt="image" src="https://github.com/user-attachments/assets/24449aee-9c85-41e3-a77c-d1f2726d2ecb" />

### Entities and Attributes

<img width="840" height="780" alt="image" src="https://github.com/user-attachments/assets/5591cdcb-de4c-4ccd-8099-699c1ed80d99" />


### Relationships and Constraints
<img width="847" height="737" alt="image" src="https://github.com/user-attachments/assets/e5481b2c-3f58-49a4-a1a4-ef8fa7026dfc" />


### Assumptions
1.A member can borrow multiple books, but each loan entry is for one book at a time.
2.FineAmount is calculated separately and stored in the Loan entity.
3.A room can host many events but an event can take place in only one room.

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
<img width="1292" height="902" alt="resturant draw drawio (1)" src="https://github.com/user-attachments/assets/19355cec-b56d-4e55-9d54-ef9b3471b610" />

### Entities and Attributes
<img width="840" height="767" alt="image" src="https://github.com/user-attachments/assets/43d8b4ac-9c1c-4c79-80c7-b6153eb3c994" />


### Relationships and Constraints

<img width="863" height="882" alt="image" src="https://github.com/user-attachments/assets/10715ce1-5dac-49cc-aade-4fbb2dcbe5fd" />

### Assumptions
- A customer may or may not make a reservation before ordering.
- Each order contains one dish per entry (multiple dishes = multiple order entries).
- Billing is done per reservation, not per individual order.
- A waiter can serve multiple orders but an order is handled by exactly one waiter.

---

