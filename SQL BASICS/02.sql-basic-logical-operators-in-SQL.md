## SQL Logical Operators

Logical operators combine or manipulate conditions in a SQL query.  

The examples below are based on the **Hotel Reservations** dataset used throughout this course.

| Operator | Purpose | Example |
|--------|--------|--------|
| `AND` | 	Returns true if both operands are true. Otherwise, returns false | `WHERE is_canceled = 0 AND adr > 100` |
| `OR` | At least one condition must be true. Otherwise returns false | `WHERE hotel = 'City Hotel' OR hotel = 'Resort Hotel'` |
| `NOT` | Negates the subsequent expression | `WHERE NOT is_canceled = 1` |
| `IN` | Matches any value in a list | `WHERE country IN ('PRT', 'ESP', 'FRA')` |
| `BETWEEN` | Filters values within a range (inclusive) | `WHERE adr BETWEEN 100 AND 300` |
| `LIKE` | Matches a text pattern | `WHERE market_segment LIKE '%Online%'` |
| `ILIKE`| Matched case-insensitive string patterns | `SELECT* FROM Hotel_reservaions WHERE no_of_week_nights`
| `EXISTS` | Returns TRUE if a subquery returns rows | `WHERE EXISTS (SELECT 1 FROM hotel_reservations hr2 WHERE hr2.country = hotel_reservations.country)` |

