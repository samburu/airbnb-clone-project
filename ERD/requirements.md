# 🏗️ Entity-Relationship Diagram (ERD) – AirBnB Clone DB

Legend:
- (PK): Primary Key
- (FK): Foreign Key
- ENUM/VARCHAR/etc.: Data type

-----------------------------------------------------------
|                        USER                             |
-----------------------------------------------------------
| user_id (PK) UUID            | email (UNIQUE, Indexed)  |
| first_name VARCHAR           | phone_number VARCHAR     |
| last_name VARCHAR            | role ENUM(guest,host,admin) |
| password_hash VARCHAR        | created_at TIMESTAMP     |
-----------------------------------------------------------
           | 1
           |
           | hosts / books / sends / receives
           |
           |<------------------------|
           |                         |
           v                         v
-----------------------------------------------------------       -----------------------------------------------------------
|                      PROPERTY                          |       |                      MESSAGE                           |
-----------------------------------------------------------       -----------------------------------------------------------
| property_id (PK) UUID         | location VARCHAR        |       | message_id (PK) UUID         | message_body TEXT       |
| host_id (FK) → USER           | pricepernight DECIMAL   |       | sender_id (FK) → USER        | sent_at TIMESTAMP       |
| name VARCHAR                  | created_at TIMESTAMP    |       | recipient_id (FK) → USER     |                         |
| description TEXT              | updated_at TIMESTAMP    |       -----------------------------------------------------------
-----------------------------------------------------------
           | 1
           | has
           v
-----------------------------------------------------------
|                      BOOKING                           |
-----------------------------------------------------------
| booking_id (PK) UUID         | start_date DATE          |
| property_id (FK) → PROPERTY  | end_date DATE            |
| user_id (FK) → USER          | total_price DECIMAL      |
| status ENUM(pending/...)     | created_at TIMESTAMP     |
-----------------------------------------------------------
           | 1
           | has
           v
-----------------------------------------------------------
|                      PAYMENT                           |
-----------------------------------------------------------
| payment_id (PK) UUID         | payment_date TIMESTAMP   |
| booking_id (FK) → BOOKING    | payment_method ENUM(...) |
| amount DECIMAL               |                          |
-----------------------------------------------------------

PROPERTY <--- has ---< REVIEW >--- written by --- USER

-----------------------------------------------------------
|                      REVIEW                            |
-----------------------------------------------------------
| review_id (PK) UUID          | rating INT (1–5)         |
| property_id (FK) → PROPERTY  | comment TEXT             |
| user_id (FK) → USER          | created_at TIMESTAMP     |
-----------------------------------------------------------
