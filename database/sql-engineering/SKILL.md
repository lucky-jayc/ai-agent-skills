---
name: sql-engineering
description: Write, review, optimize, debug, and maintain SQL queries and database scripts. Use when working with relational databases, SQL statements, joins, subqueries, CTEs, window functions, stored procedures, database constraints, query plans, or SQL performance.
---

# SQL Engineering

## 1. Role

Act as a senior SQL engineer responsible for writing reliable, secure, readable, and efficient SQL.

Help developers retrieve, insert, update, delete, analyze, and manage relational data while preserving database integrity.

Understand the target database engine before writing database-specific SQL.

Common SQL database systems include:

- PostgreSQL.
- MySQL.
- MariaDB.
- Microsoft SQL Server.
- Oracle Database.
- SQLite.

Do not assume that SQL syntax, functions, data types, or features behave identically across database engines.

## 2. Activation

Activate this skill when:

- Writing SQL queries.
- Creating or modifying tables.
- Designing database constraints.
- Retrieving related records.
- Writing complex joins.
- Building reports.
- Creating stored procedures or functions.
- Debugging SQL errors.
- Optimizing slow queries.
- Analyzing query execution plans.
- Writing database scripts and migrations.
- Reviewing SQL for security and correctness.

## 3. SQL Engineering Principles

Always prioritize:

1. Correct query results.
2. Data integrity.
3. Security.
4. Readability.
5. Maintainability.
6. Performance.
7. Database compatibility.

Before optimizing a query, establish what result it is supposed to return.

Do not make queries more complicated than necessary.

Do not sacrifice correctness for a small performance improvement.

## 4. Identify the SQL Database Engine

Before writing SQL, determine:

- Database product.
- Database version.
- SQL dialect.
- Available extensions.
- Relevant table structures.
- Column types.
- Constraints.
- Existing indexes.

If the database engine is unknown, use broadly compatible SQL where practical and clearly identify any assumptions.

When using database-specific syntax, label it appropriately.

Examples:

- PostgreSQL uses `ILIKE` for case-insensitive pattern matching.
- MySQL has its own JSON functions and indexing behavior.
- SQL Server uses `TOP` and supports T-SQL features.
- SQLite has its own type-affinity and feature limitations.

Never assume a query written for one database will execute unchanged on another.

## 5. SQL Data Definition Language (DDL)

Use DDL to define and modify database structures.

Understand:

- CREATE.
- ALTER.
- DROP.
- TRUNCATE.
- CREATE INDEX.
- DROP INDEX.
- CREATE VIEW.

Example:

```sql
CREATE TABLE students (
    student_id BIGINT PRIMARY KEY,
    registration_number VARCHAR(50) NOT NULL UNIQUE,
    full_name VARCHAR(150) NOT NULL,
    email VARCHAR(150) UNIQUE
);
```

When creating tables:

- Choose suitable data types.
- Define primary keys.
- Define required constraints.
- Use meaningful names.
- Avoid unnecessary nullable columns.
- Consider indexing requirements.
- Document important business rules.

Do not execute destructive DDL against production without authorization and a verified migration plan.

## 6. SQL Data Manipulation Language (DML)

Use DML to manipulate database records.

Understand:

- INSERT.
- UPDATE.
- DELETE.
- SELECT.

### INSERT

```sql
INSERT INTO students (
    student_id,
    registration_number,
    full_name,
    email
)
VALUES (
    1,
    'REG001',
    'John Smith',
    'john@example.com'
);
```

### UPDATE

```sql
UPDATE students
SET email = 'john.new@example.com'
WHERE student_id = 1;
```

### DELETE

```sql
DELETE FROM students
WHERE student_id = 1;
```

Always inspect the effect of UPDATE and DELETE operations.

Never omit the WHERE clause accidentally.

For important operations, use transactions and verify affected rows.

## 7. SELECT Query Engineering

Write SELECT queries that retrieve only the required data.

Example:

```sql
SELECT
    student_id,
    registration_number,
    full_name
FROM students
WHERE registration_number = 'REG001';
```

Understand:

- SELECT columns.
- DISTINCT.
- WHERE.
- ORDER BY.
- LIMIT and OFFSET.
- Database-specific pagination syntax.
- Aggregate functions.
- Aliases.

Avoid `SELECT *` in application queries when only a subset of columns is required.

Explicit column selection improves clarity and reduces unnecessary data transfer.

## 8. Filtering and Conditions

Use appropriate conditions to retrieve records.

Understand:

- AND.
- OR.
- NOT.
- IN.
- BETWEEN.
- LIKE.
- IS NULL.
- IS NOT NULL.
- EXISTS.

Example:

```sql
SELECT *
FROM students
WHERE status = 'ACTIVE'
  AND registration_date >= '2026-01-01';
```

Use parentheses when combining complex conditions.

Be aware of SQL NULL behavior.

For example, comparisons involving NULL do not behave like ordinary equality comparisons.

Use `IS NULL` and `IS NOT NULL` where appropriate.

## 9. Joins

Understand how to retrieve related records from multiple tables.

### INNER JOIN

Returns matching records.

```sql
SELECT
    students.full_name,
    courses.course_name
FROM students
INNER JOIN enrollments
    ON students.student_id = enrollments.student_id
INNER JOIN courses
    ON enrollments.course_id = courses.course_id;
```

### LEFT JOIN

Returns all records from the left table, including records without matching rows on the right.

### RIGHT JOIN

Returns all records from the right table, including records without matching rows on the left.

### FULL OUTER JOIN

Returns matching and nonmatching records from both sides, where supported.

### CROSS JOIN

Produces combinations of rows from both tables.

When writing joins:

- Identify the relationship between tables.
- Use explicit join conditions.
- Avoid unintended Cartesian products.
- Check for duplicate results.
- Use aliases consistently.
- Verify NULL behavior.

## 10. Aggregate Functions and Grouping

Use aggregate functions for calculations and reporting.

Common functions:

- COUNT().
- SUM().
- AVG().
- MIN().
- MAX().

Example:

```sql
SELECT
    course_id,
    COUNT(*) AS enrolled_students
FROM enrollments
GROUP BY course_id;
```

Use HAVING to filter grouped results.

Example:

```sql
SELECT
    course_id,
    COUNT(*) AS enrolled_students
FROM enrollments
GROUP BY course_id
HAVING COUNT(*) > 50;
```

Understand the difference between WHERE and HAVING:

- WHERE filters rows before grouping.
- HAVING filters groups after grouping.

Be careful when joining multiple one-to-many relationships because aggregate results can become inflated by duplicate rows.

## 11. Subqueries

Use subqueries when a query needs results from another query.

Example:

```sql
SELECT
    full_name
FROM students
WHERE student_id IN (
    SELECT student_id
    FROM enrollments
);
```

Understand:

- Scalar subqueries.
- Single-row subqueries.
- Multiple-row subqueries.
- Correlated subqueries.
- Nested subqueries.

Use EXISTS when checking whether related records exist.

Example:

```sql
SELECT
    students.student_id,
    students.full_name
FROM students
WHERE EXISTS (
    SELECT 1
    FROM enrollments
    WHERE enrollments.student_id = students.student_id
);
```

Choose between joins, subqueries, and EXISTS based on readability, correctness, and execution plans.

Do not assume that one approach is always faster.

## 12. Common Table Expressions (CTEs)

Use CTEs to organize complex queries into understandable steps.

Example:

```sql
WITH student_counts AS (
    SELECT
        course_id,
        COUNT(*) AS total_students
    FROM enrollments
    GROUP BY course_id
)
SELECT
    course_id,
    total_students
FROM student_counts
WHERE total_students > 50;
```

Understand:

- Ordinary CTEs.
- Multiple CTEs.
- Recursive CTEs.
- CTE materialization behavior where supported.

Use recursive CTEs for appropriate hierarchical or graph-like data traversal.

Do not assume that a CTE always improves performance. Check the target database's execution behavior.

## 13. Window Functions

Use window functions for analytical queries without collapsing rows into groups.

Common functions include:

- ROW_NUMBER().
- RANK().
- DENSE_RANK().
- LAG().
- LEAD().
- FIRST_VALUE().
- LAST_VALUE().
- SUM() OVER.
- AVG() OVER.

Example:

```sql
SELECT
    student_id,
    course_id,
    score,
    RANK() OVER (
        PARTITION BY course_id
        ORDER BY score DESC
    ) AS course_rank
FROM student_results;
```

Understand:

- PARTITION BY.
- ORDER BY.
- Window frames.
- Ranking behavior.
- Running totals.
- Moving averages.
- Previous and next row comparisons.

Choose the correct ranking function based on how ties should be handled.

## 14. SQL Constraints

Use constraints to enforce data integrity.

Understand:

- PRIMARY KEY.
- FOREIGN KEY.
- UNIQUE.
- NOT NULL.
- CHECK.
- DEFAULT.

Example:

```sql
CREATE TABLE products (
    product_id BIGINT PRIMARY KEY,
    product_name VARCHAR(150) NOT NULL,
    price DECIMAL(12, 2) NOT NULL CHECK (price >= 0),
    quantity INTEGER NOT NULL DEFAULT 0
);
```

Use constraints to protect important rules even when data is inserted or modified outside the main application.

Do not rely exclusively on application validation for rules that the database can enforce safely.

## 15. Transactions and Concurrency

Understand transaction commands:

- BEGIN.
- COMMIT.
- ROLLBACK.
- SAVEPOINT.

Example:

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 100
WHERE account_id = 2;

COMMIT;
```

In production, verify that the first operation succeeded and that the required business conditions are satisfied before committing.

Understand:

- Isolation levels.
- Row-level locking.
- Deadlocks.
- Concurrent updates.
- Lost updates.
- Unique constraint conflicts.

Use appropriate database-specific locking and concurrency mechanisms.

Do not assume that checking a condition in a separate query prevents race conditions.

## 16. SQL Functions and Stored Procedures

Understand the difference between:

- Built-in functions.
- User-defined functions.
- Stored procedures.
- Triggers.

Use stored procedures and functions where they provide clear architectural or operational benefits.

Consider:

- Maintainability.
- Transaction behavior.
- Portability.
- Permissions.
- Error handling.
- Testing.
- Deployment complexity.

Do not move all application business logic into the database without a deliberate architectural reason.

Avoid unnecessary triggers that make application behavior difficult to understand.

## 17. Views and Materialized Views

Use views to provide reusable database query interfaces.

Example:

```sql
CREATE VIEW active_students AS
SELECT
    student_id,
    registration_number,
    full_name
FROM students
WHERE status = 'ACTIVE';
```

Materialized views store query results where supported and can be useful for expensive reporting workloads.

Consider:

- Refresh strategy.
- Data freshness.
- Permissions.
- Performance.
- Dependencies.
- Maintenance.

Do not expose sensitive columns through views.

## 18. Indexing and Query Performance

Understand index types and their purpose.

Common types include:

- B-tree.
- Hash.
- Composite.
- Unique.
- Partial.
- Full-text.
- Specialized indexes supported by the database.

Use execution plans to investigate slow queries.

Example for PostgreSQL:

```sql
EXPLAIN ANALYZE
SELECT *
FROM students
WHERE registration_number = 'REG001';
```

Analyze:

- Sequential scans.
- Index scans.
- Join strategies.
- Estimated versus actual rows.
- Sort operations.
- Filter operations.
- Execution time.

Consider:

- Whether the correct index exists.
- Whether the query returns too many rows.
- Whether functions prevent index usage.
- Whether data types match.
- Whether joins use suitable columns.
- Whether the query retrieves unnecessary information.

Do not add indexes blindly. Every index has a maintenance and storage cost.

## 19. SQL Injection Prevention

Never build SQL by directly concatenating untrusted user input.

Unsafe example:

```java
String sql =
    "SELECT * FROM users WHERE email = '" + email + "'";
```

Prefer parameterized queries:

```java
String sql =
    "SELECT * FROM users WHERE email = ?";
```

Use the appropriate parameter-binding mechanism provided by the database library or framework.

For dynamic identifiers such as column names or sort directions:

- Use strict allowlists.
- Do not assume ordinary query parameters can safely represent SQL identifiers.
- Reject unsupported values.

Review SQL generated by ORMs as well as manually written queries.

## 20. Pagination and Large Datasets

Use pagination to prevent unnecessarily large result sets.

Understand:

- LIMIT and OFFSET.
- Keyset pagination.
- Cursor-based pagination.
- Stable ordering.
- Pagination consistency.

Example:

```sql
SELECT
    student_id,
    full_name
FROM students
ORDER BY student_id
LIMIT 20 OFFSET 40;
```

For large datasets or frequently changing records, consider keyset pagination.

Always define deterministic ordering for paginated results.

Apply reasonable maximum page sizes.

## 21. Database-Specific Features

When using advanced SQL features:

- Check the official database documentation.
- Verify version compatibility.
- Identify extensions or configuration requirements.
- Test queries against the actual database engine.
- Document non-portable behavior.

Do not claim that a feature is supported by every SQL database.

## 22. SQL Debugging

When a query fails:

1. Read the complete error message.
2. Identify the database engine.
3. Inspect the query.
4. Verify table and column names.
5. Check data types.
6. Check constraints.
7. Review joins and aliases.
8. Check NULL handling.
9. Verify permissions.
10. Reproduce the issue using safe test data.

Do not randomly modify SQL until the error disappears.

Understand the underlying cause.

When possible, provide both the corrected query and an explanation of the correction.

## 23. SQL Testing

Test important SQL behavior.

Include:

- Correct results.
- Empty result sets.
- NULL values.
- Duplicate records.
- Boundary values.
- Invalid inputs.
- Constraint violations.
- Transaction rollbacks.
- Concurrent operations.
- Large datasets where performance matters.

Use representative test data.

Test against the actual database engine for database-specific features.

Avoid assuming that an in-memory substitute behaves exactly like the production database.

## 24. SQL Documentation and Formatting

Write SQL that other developers can understand.

Use:

- Consistent indentation.
- Meaningful aliases.
- Explicit column lists.
- Clear join conditions.
- Consistent capitalization conventions.
- Comments for non-obvious business rules.

Avoid unnecessary nested queries and overly long single-line statements.

Document important assumptions and database-specific behavior.

## 25. SQL Engineering Workflow

### Phase 1: Understand

- Identify the database engine.
- Inspect the schema.
- Understand the requested result.
- Identify relevant relationships.
- Review existing queries.

### Phase 2: Design

- Select the appropriate SQL operation.
- Determine joins and filters.
- Consider constraints and transactions.
- Identify performance requirements.
- Check security implications.

### Phase 3: Implement

- Write readable SQL.
- Use parameterized inputs.
- Apply appropriate constraints.
- Avoid unnecessary data retrieval.
- Follow database-specific conventions.

### Phase 4: Test

- Execute using safe test data.
- Verify returned results.
- Test invalid inputs.
- Test edge cases.
- Check transaction behavior.
- Inspect execution plans when appropriate.

### Phase 5: Optimize

- Measure query performance.
- Identify bottlenecks.
- Evaluate indexing opportunities.
- Reduce unnecessary work.
- Recheck result correctness after changes.

### Phase 6: Report

Provide:

- SQL statements created or modified.
- Database engine and assumptions.
- Expected behavior.
- Tests performed.
- Performance observations.
- Security considerations.
- Remaining limitations.

## 26. Prohibited Practices

Never:

- Concatenate untrusted input into SQL statements.
- Execute destructive statements without authorization.
- Ignore database constraints.
- Assume SQL dialects are identical.
- Use SELECT * unnecessarily in application queries.
- Ignore NULL semantics.
- Add indexes without a reason.
- Claim performance improvements without measurements.
- Ignore transaction requirements.
- Report unexecuted queries as tested.

## 27. Definition of Done

A SQL engineering task is complete when:

- The target database engine is understood.
- SQL syntax is compatible with the target database.
- Queries produce the expected results.
- Inputs are handled safely.
- Data integrity is preserved.
- Important edge cases are considered.
- Transactions are used where required.
- Query performance has been considered.
- Tests have been executed where possible.
- Important assumptions are documented.

## 28. Related Skills

Use this skill alongside:

- `database-engineering`
- `backend-development`
- `api-engineering`
- `backend-security`
- `backend-testing`
- `security-standard`
- `quality-standard`

---

**Final instruction:** Write SQL that is correct, secure, understandable, and appropriate for the target database engine. Verify query results before optimizing, and use measured evidence to justify performance changes.