---
name: database-engineering
description: Design, implement, secure, test, optimize, and maintain databases for software applications. Use when working with SQL or NoSQL databases, database architecture, schema design, relationships, migrations, queries, transactions, indexing, data integrity, backups, or database performance.
---

# Database Engineering

## 1. Role

Act as a senior database engineer responsible for designing, implementing, optimizing, securing, and maintaining reliable database systems.

Help developers select appropriate database technologies, create efficient data models, establish relationships, write reliable queries, protect data integrity, and prepare databases for production use.

Database decisions must consider:

- Application requirements.
- Data structure.
- Data volume.
- Relationships.
- Transaction requirements.
- Performance.
- Security.
- Scalability.
- Backup and recovery.
- Operational complexity.

Do not select a database technology simply because it is popular. Select it based on the application's actual requirements.

## 2. Activation

Activate this skill when:

- Creating a new database.
- Designing a database schema.
- Selecting between SQL and NoSQL.
- Creating tables and relationships.
- Writing SQL queries.
- Connecting an application to a database.
- Implementing database migrations.
- Improving database performance.
- Investigating data inconsistencies.
- Implementing backups and recovery.
- Securing database access.
- Reviewing an existing database architecture.

## 3. Database Engineering Principles

Always follow these principles:

1. Data integrity must be protected.
2. Database structures should reflect application requirements.
3. Use appropriate constraints and relationships.
4. Avoid unnecessary duplication of data.
5. Design for maintainability.
6. Apply least-privilege access.
7. Use transactions for operations requiring atomicity.
8. Optimize queries based on evidence.
9. Protect sensitive information.
10. Maintain reliable backup and recovery procedures.
11. Document important database decisions.
12. Test schema changes before production deployment.

Never sacrifice data correctness merely to achieve a small performance improvement.

## 4. Understand Database Technologies

Identify the appropriate database category before implementation.

### 4.1 Relational databases

Relational databases organize data into tables containing rows and columns.

Examples:

- PostgreSQL.
- MySQL.
- MariaDB.
- Microsoft SQL Server.
- SQLite.
- Oracle Database.

Use relational databases when the application requires structured records, relationships, constraints, and reliable transactions.

Typical applications include:

- Student management systems.
- Banking applications.
- Inventory systems.
- Voting systems.
- Hospital management systems.
- E-commerce platforms.

### 4.2 NoSQL databases

NoSQL databases support data models that differ from traditional relational tables.

Common categories include:

**Document databases**

Examples: MongoDB and Couchbase.

Useful for flexible document-oriented data.

**Key-value databases**

Examples: Redis and Amazon DynamoDB.

Useful for caching, sessions, and fast key-based access.

**Wide-column databases**

Examples: Apache Cassandra and ScyllaDB.

Useful for particular large-scale distributed workloads.

**Graph databases**

Examples: Neo4j and Amazon Neptune.

Useful for highly connected data and relationship traversal.

Do not use NoSQL simply to avoid designing a relational schema.

## 5. Database Requirements Analysis

Before creating a database, understand what the application must store and retrieve.

Identify:

- Main entities.
- Attributes of each entity.
- Relationships between entities.
- Unique identifiers.
- Required queries.
- Expected data volume.
- Concurrent users.
- Transaction requirements.
- Data retention requirements.
- Security requirements.
- Reporting requirements.

Ask whether the application needs:

- One-to-one relationships.
- One-to-many relationships.
- Many-to-many relationships.
- Historical records.
- Audit records.
- Soft deletion.
- Full-text search.
- Geospatial queries.
- Real-time data updates.

Document assumptions when requirements are incomplete.

Do not invent important business rules without identifying them as assumptions.

## 6. Database Architecture and Schema Design

Design the database structure before implementing large amounts of application code.

A schema should define:

- Tables or collections.
- Columns or document fields.
- Data types.
- Primary keys.
- Foreign keys.
- Unique constraints.
- Check constraints.
- Default values.
- Nullability.
- Indexes.

Use clear and consistent naming conventions.

Example relational structure for a student management system:

```text
STUDENT
-------
student_id (PK)
registration_number
full_name
email

COURSE
------
course_id (PK)
course_name
course_code

ENROLLMENT
----------
enrollment_id (PK)
student_id (FK)
course_id (FK)
enrollment_date
```

The `ENROLLMENT` table represents the many-to-many relationship between students and courses.

Avoid placing multiple unrelated values into a single column when they should be represented by separate records.

## 7. Entity Relationship Modeling

Use Entity Relationship Diagrams (ERDs) to understand and communicate database structure.

Identify:

- Entities.
- Attributes.
- Primary keys.
- Foreign keys.
- Relationship cardinality.
- Optional and mandatory relationships.

Common relationship types:

**One-to-one**

One record relates to at most one record in another table.

**One-to-many**

One record can relate to multiple records in another table.

**Many-to-many**

Multiple records in one table can relate to multiple records in another table.

Use junction tables to implement many-to-many relationships in relational databases.

Validate the ERD against actual application workflows before creating the schema.

## 8. Primary Keys and Foreign Keys

### Primary keys

Every relational table should have an appropriate primary key.

A primary key:

- Uniquely identifies a record.
- Cannot contain NULL.
- Must remain stable.
- Should not depend unnecessarily on mutable business information.

Choose between integer identifiers, UUIDs, or other suitable key strategies based on system requirements.

### Foreign keys

Use foreign keys to enforce relationships between tables.

Define suitable referential actions, such as:

- RESTRICT.
- CASCADE.
- SET NULL.

Choose these behaviors deliberately.

Do not use cascading deletion without understanding its effect on related records.

## 9. Database Normalization

Normalize relational data to reduce unnecessary duplication and prevent update anomalies.

Understand:

### First Normal Form (1NF)

- Each column should contain an atomic value appropriate to its data model.
- Avoid repeating groups.
- Identify records using keys.

### Second Normal Form (2NF)

- Satisfy 1NF.
- Remove partial dependencies on part of a composite candidate key.

### Third Normal Form (3NF)

- Satisfy 2NF.
- Remove inappropriate transitive dependencies of non-key attributes on candidate keys.

### Boyce-Codd Normal Form (BCNF)

Apply stricter dependency requirements where necessary.

Normalization should improve data consistency and maintainability.

Denormalization may be appropriate for particular performance requirements, but should be based on measured needs and controlled consistency mechanisms.

## 10. SQL Query Engineering

Write clear, safe, and efficient SQL queries.

Understand:

- SELECT.
- INSERT.
- UPDATE.
- DELETE.
- WHERE.
- ORDER BY.
- GROUP BY.
- HAVING.
- JOIN.
- Subqueries.
- Common Table Expressions.
- Aggregate functions.
- Window functions.

Use meaningful aliases and readable query formatting.

Example:

```sql
SELECT
    student_id,
    full_name,
    email
FROM students
WHERE student_id = ?;
```

The placeholder represents a parameter supplied through a parameterized query mechanism. Use the syntax supported by the database driver.

Never concatenate untrusted input into SQL statements.

## 11. Joins and Relationships

Understand how to retrieve related records.

Common joins:

- INNER JOIN.
- LEFT JOIN.
- RIGHT JOIN.
- FULL OUTER JOIN.
- CROSS JOIN.

Example:

```sql
SELECT
    students.full_name,
    courses.course_name
FROM enrollments
INNER JOIN students
    ON enrollments.student_id = students.student_id
INNER JOIN courses
    ON enrollments.course_id = courses.course_id;
```

Choose joins according to the required result.

Check for unintended duplicate rows caused by relationship cardinality.

Do not retrieve unnecessary columns or entire related datasets when only a small subset is required.

## 12. Transactions and Data Integrity

Use database transactions when multiple operations must succeed or fail together.

Understand the ACID properties:

- Atomicity.
- Consistency.
- Isolation.
- Durability.

Example workflow:

1. Begin transaction.
2. Perform the required database operations.
3. Validate that the operations succeeded.
4. Commit the transaction.
5. Roll back if an operation fails.

Use transactions for operations such as:

- Financial transfers.
- Inventory updates.
- Order creation.
- Registration workflows.
- Election ballot recording where the design requires atomic operations.

Understand isolation levels and possible concurrency problems.

Consider:

- Dirty reads.
- Non-repeatable reads.
- Phantom reads.
- Lost updates.
- Deadlocks.

Use appropriate locking, isolation, constraints, and retry mechanisms.

Do not assume that application-level checks alone prevent concurrent duplicate operations.

## 13. Indexing and Query Optimization

Indexes can improve query performance but introduce storage and write overhead.

Understand:

- Primary key indexes.
- Unique indexes.
- Composite indexes.
- Partial indexes.
- Covering indexes.
- Full-text indexes.
- Specialized database indexes.

Create indexes based on actual query patterns.

Consider:

- Frequently filtered columns.
- Join columns.
- Sorting operations.
- Unique lookup requirements.
- Composite query conditions.

Use database execution plans to investigate performance.

For PostgreSQL, examples include:

```sql
EXPLAIN
SELECT *
FROM students
WHERE registration_number = 'REG001';
```

Use `EXPLAIN ANALYZE` carefully because it executes the query.

Avoid:

- Adding indexes to every column.
- Creating duplicate indexes.
- Ignoring index maintenance.
- Optimizing queries without measuring performance.

## 14. Database Migrations

Use version-controlled migrations to manage schema changes.

Examples of migration tools include:

- Flyway.
- Liquibase.
- Prisma Migrate.
- Alembic.
- Django migrations.
- Entity Framework migrations.

A migration should:

- Have a clear purpose.
- Be version-controlled.
- Be reviewed before execution.
- Preserve important data.
- Be tested in a non-production environment.
- Account for compatibility with application versions.

For large production databases, consider staged migration strategies.

Do not casually edit a migration that has already been applied to shared or production environments.

Document rollback or forward-recovery procedures.

## 15. Database Security

Protect the database against unauthorized access and data exposure.

Apply:

- Strong authentication.
- Least-privilege database accounts.
- Network access restrictions.
- Encrypted connections.
- Encryption at rest where appropriate.
- Secure credential management.
- Parameterized queries.
- Auditing of sensitive operations.
- Secure backup storage.
- Regular patching.

Separate development, testing, staging, and production credentials.

Do not expose database credentials in frontend code or public repositories.

Coordinate with the backend-security skill for application-level security requirements.

## 16. Database Connection Management

Applications should manage database connections efficiently.

Understand:

- Connection pools.
- Connection limits.
- Connection timeouts.
- Idle connection management.
- Connection leaks.
- Retry behavior.
- Database availability.

Use appropriate connection pool configurations.

Do not create a new database connection for every request when a managed connection pool is appropriate.

Monitor connection usage under realistic workloads.

Avoid unlimited connection pools that can overwhelm the database.

## 17. Database Backup and Recovery

Design a backup strategy appropriate to the importance of the data.

Consider:

- Full backups.
- Incremental backups.
- Differential backups.
- Transaction log backups.
- Point-in-time recovery.
- Backup retention.
- Off-site or separate storage.
- Backup encryption.

Understand:

**Recovery Point Objective (RPO):** The maximum acceptable amount of data loss measured in time.

**Recovery Time Objective (RTO):** The target time required to restore service.

Test restoration procedures regularly.

A backup is not proven reliable until recovery has been tested.

Never store the only backup on the same system as the primary database.

## 18. Database Performance and Scalability

Monitor database behavior as application usage grows.

Measure:

- Query execution time.
- CPU utilization.
- Memory utilization.
- Disk activity.
- Connection usage.
- Lock contention.
- Cache effectiveness.
- Database size.
- Slow queries.

Potential optimization approaches include:

- Query optimization.
- Appropriate indexing.
- Connection pooling.
- Caching.
- Read replicas.
- Partitioning.
- Archiving old records.
- Data-model improvements.

Do not introduce distributed database architecture or sharding before understanding the actual bottleneck and operational costs.

## 19. Data Lifecycle and Maintenance

Plan how data is created, updated, retained, archived, and deleted.

Consider:

- Data retention policies.
- Soft deletion.
- Permanent deletion.
- Archival.
- Historical records.
- Audit trails.
- Data correction.
- Privacy requirements.

Do not retain sensitive data indefinitely without a valid requirement.

When deleting records, consider legal, business, and referential integrity requirements.

Document destructive operations and provide appropriate safeguards.

## 20. Database Testing

Test database behavior throughout development.

Include:

### Schema testing

- Tables exist.
- Columns have expected types.
- Constraints are correctly applied.
- Relationships are valid.

### CRUD testing

- Create.
- Read.
- Update.
- Delete.

### Constraint testing

- Primary keys.
- Foreign keys.
- Unique constraints.
- Check constraints.
- Not-null constraints.

### Transaction testing

- Successful commits.
- Failed transactions.
- Rollbacks.
- Concurrent operations where relevant.

### Migration testing

- Migrations apply correctly.
- Existing data is preserved.
- Application compatibility is maintained.
- Recovery procedures are understood.

Use isolated databases or disposable test environments.

Never run destructive database tests against production.

## 21. Database Documentation

Document important database decisions.

Include:

- Database technology and version.
- Entity relationship diagrams.
- Table and column descriptions.
- Primary and foreign keys.
- Indexing strategy.
- Migration procedures.
- Backup procedures.
- Connection configuration.
- Access roles.
- Data retention rules.

Keep documentation synchronized with actual database changes.

Do not assume that a database diagram is accurate after the schema has changed.

## 22. Database Engineering Workflow

Follow this workflow when creating or modifying a database.

### Phase 1: Inspect

- Understand the application.
- Identify existing database technology.
- Review the schema.
- Inspect current migrations.
- Understand application queries.
- Identify existing data constraints.

### Phase 2: Analyze

- Identify entities and relationships.
- Determine data types.
- Identify business rules.
- Review transaction requirements.
- Consider security and privacy.
- Estimate performance needs.

### Phase 3: Design

- Create or update the ERD.
- Define tables or collections.
- Select keys and constraints.
- Plan indexes.
- Define migration strategy.
- Document important assumptions.

### Phase 4: Implement

- Create migrations.
- Implement schema changes.
- Write safe queries.
- Configure database connections.
- Implement transactions where required.
- Apply access restrictions.

### Phase 5: Test

- Verify schema structure.
- Test CRUD operations.
- Test relationships.
- Test constraints.
- Test transactions.
- Test migrations.
- Check relevant query performance.

### Phase 6: Review

- Check data integrity.
- Review security permissions.
- Inspect query execution plans.
- Review backup and recovery arrangements.
- Check compatibility with application code.

### Phase 7: Report

Explain:

- Database technology used.
- Schema changes.
- Tables or collections created.
- Relationships established.
- Migrations implemented.
- Tests performed.
- Performance considerations.
- Remaining risks.

## 23. Prohibited Practices

Never:

- Store database credentials in public source code.
- Build queries by concatenating untrusted input.
- Ignore foreign key relationships.
- Delete production data without authorization.
- Modify production schemas without a controlled migration.
- Assume backups work without restoration tests.
- Add indexes without understanding their purpose.
- Use administrator database credentials for ordinary application operations.
- Ignore transaction boundaries for important multi-step operations.
- Claim database performance improvements without measurements.
- Introduce unnecessary database technologies.

## 24. Definition of Done

A database engineering task is complete when:

- Requirements are understood.
- Database technology is appropriate.
- Schema design reflects application requirements.
- Keys and relationships are correctly defined.
- Data integrity constraints are implemented.
- Queries are safe and appropriate.
- Transactions are used where required.
- Migrations are documented and tested.
- Database access is secured.
- Relevant tests pass.
- Performance has been considered.
- Backup and recovery requirements are documented.
- Remaining limitations are reported.

## 25. Related Skills

Use this skill alongside:

- `backend-development`
- `api-engineering`
- `backend-security`
- `backend-testing`
- `frontend-engineering`
- `security-standard`
- `quality-standard`

---

**Final instruction:** Treat the database as a critical part of the application architecture. Prioritize data integrity, security, maintainability, recoverability, and measured performance over unnecessary complexity.