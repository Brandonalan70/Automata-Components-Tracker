---
output:
  pdf_document: default
  html_document: default
---
# Automata Components Tracker

## Overview
This project designs and implements a relational database system for Automata, Inc., a specialty vehicle manufacturer. The database streamlines inventory management, order tracking, and supplier coordination across multiple production departments. Data modeling, SQL implementation, and query development were all completed as part of Penn State's DS 220 – Team Projects on Relational Database Design & Implementation.

**Key Objectives:**
- Design a comprehensive Enhanced Entity-Relationship (EER) model to represent Automata's operational structure.
- Implement the EER model into a fully functional PostgreSQL database using DDL and DML scripts.
- Develop targeted SQL queries to answer real operational questions faced by Automata's purchasing department.

---

## Methodology

### 1. Data Modeling
- Developed an Enhanced Entity-Relationship (EER) model capturing all core entities: Departments, Orders, Parts, Inventory, Vehicles, and Suppliers.
- Translated the EER model into a Logical Data Model defining primary keys, foreign keys, and cardinality constraints between all tables.

### 2. Database Implementation
- Implemented the logical model in PostgreSQL using DDL to create tables with appropriate constraints (NOT NULL, CHECK, UNIQUE, SERIAL).
- Populated the database using DML INSERT statements covering all entities and junction tables.
- Junction tables (PartsSupplier, OrderParts, VehicleParts, DepartmentVehicle) were created to resolve many-to-many relationships using composite primary keys.

### 3. Query Development
- Formulated six SQL queries addressing key operational scenarios using JOIN operations, aggregate functions (COUNT, SUM), GROUP BY, and conditional filtering.

---

## Tools & Libraries
- **PostgreSQL** — relational database engine
- **DBeaver** — database GUI and query execution environment
- **SQL (DDL & DML)** — schema creation and data insertion

---

## Database Schema

| Table | Primary Key | Foreign Key(s) |
|---|---|---|
| Department | DepartmentID | — |
| Parts | PIN | — |
| Vehicle | VIN | — |
| Orders | OrderNum | DepartmentID → Department |
| Inventory | InventoryID | PIN → Parts |
| Supplier | SupplierID | — |
| PartsSupplier | (PIN, SupplierID) | PIN → Parts, SupplierID → Supplier |
| OrderParts | (OrderNum, PIN) | OrderNum → Orders, PIN → Parts |
| VehicleParts | (VIN, PIN) | VIN → Vehicle, PIN → Parts |
| DepartmentVehicle | (DepartmentID, VIN) | DepartmentID → Department, VIN → Vehicle |

---

## Sample Queries

1. **Which departments have ordered a 'Steering Wheel'?**
   Joins Department, Orders, OrderParts, and Parts; filters by part name.

2. **What are the current inventory levels for each part?**
   Joins Parts and Inventory to report quantity on hand per part.

3. **List all parts supplied by 'Supplier A'.**
   Joins Parts, PartsSupplier, and Supplier; filters by supplier name.

4. **Which supplier has been used most frequently by the Engineering department?**
   Aggregates across Supplier, PartsSupplier, OrderParts, Orders, and Department; sorts by order count.

5. **How many orders have been placed by each department?**
   Uses LEFT JOIN on Department and Orders with GROUP BY and COUNT.

6. **What is the total number of parts ordered for trucks?**
   Joins Vehicle, VehicleParts, and OrderParts; filters by vehicle type and sums quantity.

---

## Results
- The implemented database successfully supports all core purchasing department workflows at Automata, Inc.
- All six queries executed correctly, returning accurate results consistent with the inserted test data.
- Query results confirmed logical correctness of the schema — for example, only the Engineering department had ordered a Steering Wheel, and Supplier A was identified as Engineering's most-used supplier.
- The schema design enforces referential integrity through foreign key constraints and prevents invalid inventory entries via CHECK constraints on quantity fields.

---

## Team
| Name | Role |
|---|---|
| Brandon Barber | Lead Developer |
| Michael Ridgeway | Project Manager |
| Li Zhu | Analyst |

**Course:** DS 220 – Team Projects on Relational Database Design & Implementation
**Institution:** College of Information Sciences and Technology, Pennsylvania State University
