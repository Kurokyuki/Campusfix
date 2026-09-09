# CampusFix --- Database Design

## 1. Purpose

This document describes a proposed database structure for the CampusFix
maintenance reporting system.

The project material states that students report problems by selecting
the room and issue type, while staff manage maintenance requests and
update their status. The database design below is based on those
functions.

## 2. Proposed Entities

### 2.1 Users

Stores information about people who use the system.

  Field     Description
  --------- -------------------------------------
  user_id   Unique identifier for the user
  name      User's name
  email     User's email address
  role      User role, such as student or staff

### 2.2 Rooms

Stores information about campus rooms.

  Field         Description
  ------------- --------------------------------
  room_id       Unique identifier for the room
  building      Building containing the room
  room_number   Room number/name

### 2.3 Reports

Stores maintenance reports submitted by users.

  Field         Description
  ------------- ---------------------------------------
  report_id     Unique identifier for the report
  user_id       User who submitted the report
  room_id       Room where the problem occurred
  issue_type    Type of maintenance problem
  description   Description of the problem
  status        Current report status
  created_at    Date/time the report was created
  updated_at    Date/time the report was last updated

## 3. Relationships

### Users → Reports

One user can submit multiple reports.

**Relationship:** `Users 1 : Many Reports`

### Rooms → Reports

One room can have multiple maintenance reports.

**Relationship:** `Rooms 1 : Many Reports`

## 4. Entity Relationship Diagram

``` text
+----------------+          +----------------+
|     Users      |          |     Rooms      |
+----------------+          +----------------+
| PK user_id     |          | PK room_id     |
| name           |          | building       |
| email          |          | room_number    |
| role           |          +----------------+
+-------+--------+                   |
        |                            |
        | 1                          | 1
        |                            |
        | *                          | *
        +----------+-----------------+
                   |
                   v
          +----------------+
          |    Reports     |
          +----------------+
          | PK report_id   |
          | FK user_id     |
          | FK room_id     |
          | issue_type     |
          | description    |
          | status         |
          | created_at     |
          | updated_at     |
          +----------------+
```

## 5. Example Issue Types

The CampusFix project identifies several common campus problems:

-   Broken air conditioner
-   Broken light
-   Broken fan
-   Toilet problem
-   Wi-Fi problem
-   Other campus facility problem

## 6. Report Status

The project description specifically identifies a status flow from:

``` text
Reported → Fixed
```

Additional statuses should only be added if the project group decides
that they are necessary.

## 7. Notes and Assumptions

The provided project presentation does not specify the exact database
technology or every field required by the final implementation.

Therefore, this is a proposed logical database design based only on the
functions described in the CampusFix project material. The final
database schema should be updated to match the actual implementation in
the Visual Studio project.
