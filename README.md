# ⚽ Football Ticket Booking System

A SQL-based project that models a simple football match ticket booking platform. It covers database schema design, sample data, and a set of practice queries demonstrating filtering, pattern matching, NULL handling, joins, aggregation, and pagination concepts.

## 📁 Repository Structure

```
Football-Ticket-Booking-System/
└── Query.sql   # All SQL queries for the exercises below
```

## 🗄️ Database Schema & Sample Data

### 1. Users Table

| user_id | full_name | email | role | phone_number |
|---|---|---|---|---|
| 1 | Tanvir Rahman | tanvir@mail.com | Football Fan | +8801711111111 |
| 2 | Asif Haque | asif@mail.com | Football Fan | +8801722222222 |
| 3 | Sajjad Rahman | sajjad@mail.com | Ticket Manager | +8801733333333 |
| 4 | Jannat Ara | jannat@mail.com | Football Fan | NULL |

### 2. Matches Table

| match_id | fixture | tournament_category | base_ticket_price | match_status |
|---|---|---|---|---|
| 101 | Real Madrid vs Barcelona | Champions League | 150 | Available |
| 102 | Man City vs Liverpool | Premier League | 120 | Selling Fast |
| 103 | Bayern Munich vs PSG | Champions League | 130 | Available |
| 104 | AC Milan vs Inter Milan | Serie A | 90 | Sold Out |
| 105 | Juventus vs Roma | Serie A | 80 | Available |

### 3. Bookings Table

| booking_id | user_id | match_id | seat_number | payment_status | total_cost |
|---|---|---|---|---|---|
| 501 | 1 | 101 | A-12 | Confirmed | 150 |
| 502 | 1 | 102 | B-04 | Confirmed | 120 |
| 503 | 2 | 101 | A-13 | Confirmed | 150 |
| 504 | 2 | 101 | NULL | NULL | 150 |
| 505 | 3 | 102 | C-20 | Pending | 120 |

## 🧩 SQL Queries & Expected Output

All queries live in [`Query.sql`](./Query.sql).

### Query 1 — Champions League matches available for booking

Retrieve all upcoming football matches belonging to the **Champions League** where the match status is **Available**.

| match_id | fixture | base_ticket_price |
|---|---|---|
| 101 | Real Madrid vs Barcelona | 150 |
| 103 | Bayern Munich vs PSG | 130 |

### Query 2 — Search users by name pattern

Search for all users whose full names start with `Tanvir` or contain the phrase `Haque` (case-insensitive).

**Concepts used:** `LIKE`, `ILIKE`

| user_id | full_name | email |
|---|---|---|
| 1 | Tanvir Rahman | tanvir@mail.com |
| 2 | Asif Haque | asif@mail.com |

### Query 3 — Bookings missing payment status

Retrieve all booking records where the payment status is missing (`NULL`), replacing the empty result with `Action Required`.

**Concepts used:** `IS NULL`, `COALESCE`

| booking_id | user_id | match_id | systematic_status |
|---|---|---|---|
| 504 | 2 | 101 | Action Required |

### Query 4 — Booking details with user and match info

Retrieve match booking details along with the user's full name and the scheduled match fixture teams.

**Concepts used:** `INNER JOIN`

| booking_id | full_name | fixture | total_cost |
|---|---|---|---|
| 501 | Tanvir Rahman | Real Madrid vs Barcelona | 150 |
| 502 | Tanvir Rahman | Man City vs Liverpool | 120 |
| 503 | Asif Haque | Real Madrid vs Barcelona | 150 |
| 504 | Asif Haque | Real Madrid vs Barcelona | 150 |
| 505 | Sajjad Rahman | Man City vs Liverpool | 120 |

### Query 5 — All users including those with no bookings

Display a comprehensive list of all users and their booking IDs, ensuring that fans who have never bought a ticket are still listed.

**Concepts used:** `LEFT JOIN` / `FULL JOIN`

| user_id | full_name | booking_id |
|---|---|---|
| 1 | Tanvir Rahman | 501 |
| 1 | Tanvir Rahman | 502 |
| 2 | Asif Haque | 503 |
| 2 | Asif Haque | 504 |
| 3 | Sajjad Rahman | 505 |
| 4 | Jannat Ara | NULL |

### Query 6 — Bookings above average cost

Find all ticket bookings where the total cost is strictly higher than the average cost of all ticket bookings.

**Concepts used:** Subquery, `AVG()`

| booking_id | match_id | total_cost |
|---|---|---|
| 501 | 101 | 150 |
| 503 | 101 | 150 |
| 504 | 101 | 150 |

### Query 7 — Second and third most expensive matches

Retrieve the top 2 most expensive matches sorted by base ticket price, skipping the absolute highest premium match (skips *Real Madrid vs Barcelona* at 150).

**Concepts used:** `ORDER BY`, `LIMIT`, `OFFSET`

| match_id | fixture | base_ticket_price |
|---|---|---|
| 103 | Bayern Munich vs PSG | 130 |
| 102 | Man City vs Liverpool | 120 |

## 🚀 Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/st-shourov12/Football-Ticket-Booking-System.git
   cd Football-Ticket-Booking-System
   ```
2. Create the `users`, `matches`, and `bookings` tables in your SQL environment (PostgreSQL, MySQL, or similar) using the schema above and insert the sample data.
3. Open [`Query.sql`](./Query.sql) and run each query against the sample data to see the expected output.

## 🛠️ Concepts Covered

- Filtering with `WHERE`
- Pattern matching with `LIKE` / `ILIKE`
- NULL handling with `IS NULL` and `COALESCE`
- `INNER JOIN` and `LEFT JOIN`
- Aggregate functions (`AVG`)
- Sorting and pagination with `ORDER BY`, `LIMIT`, and `OFFSET`

## 👤 Author

**st-shourov12**
[GitHub Profile](https://github.com/st-shourov12)

## 📄 License

This project is open source and available for learning and practice purposes.
