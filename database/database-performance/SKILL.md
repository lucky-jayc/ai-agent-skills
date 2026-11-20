---
name: database-performance
description: Analyze, monitor, diagnose, and optimize database performance across SQL and NoSQL systems. Use when investigating slow queries, improving indexes, optimizing database schemas, reducing latency, handling high concurrency, tuning connections, implementing caching, or preparing databases for production workloads.
---

# Database Performance Engineering Skill

## 1. Role

Act as a senior database performance engineer responsible for ensuring that databases are responsive, reliable, scalable, and efficient.

Your responsibility is to identify performance bottlenecks, measure their impact, recommend appropriate optimizations, implement safe improvements, and verify that those improvements produce measurable results.

Support relational and non-relational database systems.

Examples include:
- PostgreSQL
- MySQL
- Microsoft SQL Server
- Oracle Database
- SQLite
- MongoDB
- Redis
- Other supported database technologies

Never assume that every database supports the same optimization techniques or configuration options.

## 2. Activation Conditions

Activate this skill when a task involves:

- Slow database queries.
- High database response times.
- Poor application performance caused by database operations.
- Database indexing.
- Query optimization.
- Database capacity planning.
- High concurrent user traffic.
- Connection pool optimization.
- Database caching.
- Database scaling.
- Database monitoring.
- Database load or stress testing.
- Production database performance problems.

## 3. Core Engineering Principles

Follow these principles:

1. Measure before optimizing.
2. Identify the actual bottleneck before changing the system.
3. Prefer evidence-based improvements over assumptions.
4. Preserve data integrity and application correctness.
5. Avoid unnecessary indexes and complicated database structures.
6. Consider read and write performance together.
7. Test optimizations using realistic workloads.
8. Avoid disruptive production changes.
9. Document performance improvements and trade-offs.
10. Never sacrifice security or correctness for speed.

## 4. Understand Performance Requirements

Before optimizing a database, understand the workload.

Investigate:

- Expected number of users.
- Number of concurrent connections.
- Read-to-write ratio.
- Average database request volume.
- Peak traffic periods.
- Data volume and expected growth.
- Most frequently executed queries.
- Business-critical operations.
- Acceptable response times.
- Availability and reliability requirements.

Identify measurable performance targets.

Examples:

- Query response time.
- Transaction completion time.
- Requests per second.
- Transactions per second.
- Database connection utilization.
- CPU utilization.
- Memory consumption.
- Disk I/O.
- Lock waits.
- Cache hit ratio.

Do not invent performance targets. Ask for them when they are essential or establish clearly labeled provisional baselines.

## 5. Establish a Performance Baseline

Before modifying the database:

1. Identify important queries and operations.
2. Record their current execution times.
3. Measure throughput.
4. Observe resource utilization.
5. Record connection usage.
6. Identify slow queries.
7. Measure performance under realistic concurrency.
8. Record the database version and configuration.

Use the baseline to compare results after optimization.

Where possible, compare equivalent workloads under similar conditions.

## 6. Query Performance Analysis

Investigate slow queries systematically.

Check:

- Query execution time.
- Number of rows scanned.
- Number of rows returned.
- Index usage.
- Join operations.
- Sorting operations.
- Filtering conditions.
- Aggregation operations.
- Temporary tables or disk spills.
- Repeated database requests.
- Lock contention.

Use database-specific query analysis tools.

Examples:

PostgreSQL:
- EXPLAIN
- EXPLAIN ANALYZE
- pg_stat_statements

MySQL:
- EXPLAIN
- EXPLAIN ANALYZE where supported
- Performance Schema
- Slow Query Log

SQL Server:
- Execution Plans
- Query Store
- Dynamic Management Views

MongoDB:
- explain()
- Database Profiler
- Current operation monitoring

Important: EXPLAIN ANALYZE may execute a query rather than merely inspect it. Assess the query's side effects and execution cost before using it, particularly with data-modifying statements or production workloads.

## 7. Database Index Optimization

Evaluate whether indexes can improve frequently executed queries.

Understand common index types:

- B-tree indexes.
- Composite indexes.
- Unique indexes.
- Partial indexes.
- Covering indexes.
- Full-text indexes.
- Hash indexes where supported.
- Specialized indexes such as spatial indexes.

When designing indexes:

1. Identify frequently queried columns.
2. Examine filtering conditions.
3. Examine JOIN conditions.
4. Consider sorting requirements.
5. Review existing indexes.
6. Examine execution plans.
7. Measure the effect of proposed indexes.

For composite indexes, consider column order and the actual query patterns.

Avoid creating indexes on every column.

Indexes consume storage and can increase the cost of INSERT, UPDATE, and DELETE operations.

Verify that an index improves the intended workload without causing unacceptable write-performance degradation.

## 8. SQL Query Optimization

Improve query efficiency while preserving expected results.

Consider:

- Selecting only required columns.
- Avoiding unnecessary SELECT * usage.
- Filtering records as early as practical.
- Using appropriate JOIN conditions.
- Avoiding unnecessary subqueries.
- Reducing repeated calculations.
- Optimizing GROUP BY and ORDER BY operations.
- Avoiding unnecessary DISTINCT operations.
- Using suitable pagination strategies.
- Avoiding unnecessary database round trips.
- Detecting and resolving N+1 query problems.

Do not rewrite queries solely to make them shorter.

Validate that optimized queries return equivalent results.

## 9. Schema and Data Model Optimization

Review the database structure when performance problems originate from data modeling.

Consider:

- Table relationships.
- Normalization.
- Denormalization.
- Data types.
- Column sizes.
- Primary keys.
- Foreign keys.
- Constraints.
- Frequently accessed relationships.
- Large or rapidly growing tables.

Use normalization to reduce unnecessary duplication and preserve consistency.

Use denormalization only when a measurable performance or architectural requirement justifies it.

Document the consistency and maintenance trade-offs introduced by denormalization.

Never remove important integrity constraints merely to improve speed without a justified alternative.

## 10. Transaction and Lock Optimization

Investigate transaction behavior when database operations become slow under concurrent workloads.

Check:

- Long-running transactions.
- Lock waits.
- Deadlocks.
- Transaction isolation levels.
- Excessive transaction duration.
- Concurrent updates.
- Unnecessary row locking.
- Poor transaction boundaries.

Use short, well-defined transactions where appropriate.

Do not weaken transaction isolation without understanding the possibility of dirty reads, non-repeatable reads, phantom reads, or other consistency problems.

When deadlocks occur:

1. Identify the participating transactions.
2. Examine their lock acquisition order.
3. Identify conflicting operations.
4. Reduce unnecessary transaction duration.
5. Consider consistent resource access ordering.
6. Retest under concurrency.

## 11. Connection Pool Optimization

Evaluate database connection management.

Investigate:

- Maximum pool size.
- Minimum idle connections.
- Connection acquisition timeout.
- Connection lifetime.
- Idle timeout.
- Connection leaks.
- Database connection limits.
- Number of application instances.

Use connection pooling where supported.

Do not increase the pool size blindly. Too many simultaneous connections can overload the database.

Ensure connections are returned to the pool after use.

Use sensible timeouts and monitor pool saturation.

## 12. Database Caching

Determine whether caching can reduce repeated database work.

Possible caching approaches include:

- Application-level caching.
- Query result caching where supported.
- In-memory caching.
- Redis.
- Distributed caching.
- Materialized views.

Before introducing caching, identify:

- Frequently accessed data.
- Data freshness requirements.
- Cache expiration policies.
- Cache invalidation rules.
- Memory requirements.
- Consistency requirements.
- Failure behavior when the cache is unavailable.

Define an appropriate time-to-live (TTL) where applicable.

Never assume cached data is always correct.

Protect cached information using appropriate authentication, authorization, and data isolation.

## 13. Database Scaling

Choose scaling techniques based on measured bottlenecks.

### Vertical scaling

Increase available resources such as:

- CPU.
- RAM.
- Storage performance.
- Network capacity.

### Read replicas

Consider read replicas when read workloads are high and the application can tolerate replication lag.

Understand that replicas may return stale data.

### Partitioning

Consider partitioning large tables when it improves data management, query performance, or maintenance operations.

Choose partition keys based on actual access patterns.

### Sharding

Consider sharding only when simpler scaling approaches are insufficient.

Evaluate:

- Shard key selection.
- Data distribution.
- Cross-shard queries.
- Transaction complexity.
- Rebalancing.
- Operational overhead.

Do not introduce distributed database complexity without a clear justification.

## 14. Bulk Operations and Batch Processing

For large data operations, evaluate batch processing.

Consider:

- Batch inserts.
- Batch updates.
- Bulk imports.
- Bulk exports.
- Pagination.
- Background processing.
- Transaction size.
- Retry behavior.

Avoid loading extremely large datasets into application memory unnecessarily.

Choose batch sizes based on measurement.

Ensure failed batches can be retried safely without creating duplicate or inconsistent records.

## 15. Database Resource Optimization

Monitor database resource consumption.

Evaluate:

- CPU usage.
- Memory pressure.
- Disk I/O.
- Storage capacity.
- Network latency.
- Temporary storage.
- Database cache behavior.
- Connection utilization.

Use configuration settings appropriate to the selected database and deployment environment.

Never copy configuration values from another database installation without understanding the workload, hardware, and database version.

## 16. Monitoring and Observability

Ensure important database performance indicators can be monitored.

Monitor:

- Slow queries.
- Query execution times.
- Throughput.
- Active connections.
- Idle connections.
- Connection pool saturation.
- Lock waits.
- Deadlocks.
- CPU and memory.
- Disk utilization.
- Replication lag.
- Cache hit ratio.
- Storage growth.

Use suitable monitoring tools and dashboards.

Examples include:

- Prometheus.
- Grafana.
- Database-native monitoring.
- Cloud database monitoring services.
- Application performance monitoring tools.

Avoid logging passwords, credentials, access tokens, or sensitive query parameters.

## 17. Performance and Load Testing

Validate database performance under realistic workloads.

Test:

- Normal usage.
- Peak usage.
- High concurrency.
- Large datasets.
- Read-heavy workloads.
- Write-heavy workloads.
- Mixed workloads.
- Long-running operations.
- Recovery after temporary overload.

Possible tools include:

- pgbench.
- sysbench.
- Apache JMeter.
- k6.
- Gatling.
- Database-native benchmarking utilities.

Use representative test data.

Do not use production customer information in performance tests unless explicitly authorized and appropriately protected.

Separate load testing from production systems unless a controlled production test has been approved.

Measure results against the established baseline.

## 18. Cloud and Managed Database Performance

When using managed database services, examine:

- Instance size.
- Storage type.
- Connection limits.
- Network latency.
- Read replica availability.
- Backup configuration.
- Automatic scaling.
- Monitoring capabilities.
- Regional placement.
- Service quotas.
- Pricing implications.

Do not assume that a managed database automatically optimizes application queries.

Ensure that the application and database are deployed with appropriate network proximity.

## 19. Safe Performance Optimization Workflow

Follow this workflow for database performance tasks.

### Phase 1: Inspect

- Identify the database technology and version.
- Understand the existing schema.
- Review important queries.
- Examine current indexes.
- Inspect application database access patterns.

### Phase 2: Measure

- Establish performance baselines.
- Identify slow queries.
- Measure resource utilization.
- Reproduce the problem safely.

### Phase 3: Diagnose

- Analyze execution plans.
- Examine index usage.
- Investigate locks and transactions.
- Identify inefficient queries.
- Identify connection or resource bottlenecks.

### Phase 4: Plan

- Rank problems by impact.
- Identify possible optimizations.
- Assess correctness and security risks.
- Estimate implementation complexity.
- Define measurable success criteria.

### Phase 5: Implement

- Make targeted changes.
- Preserve existing functionality.
- Use safe migrations.
- Avoid unnecessary configuration changes.
- Document important trade-offs.

### Phase 6: Test

- Run relevant functional tests.
- Compare query results.
- Benchmark performance.
- Test concurrency.
- Check for regressions.

### Phase 7: Validate

- Compare results with the original baseline.
- Confirm that expected improvements occurred.
- Check database integrity.
- Review resource consumption.
- Confirm that application behavior remains correct.

### Phase 8: Report

Provide a concise report describing:

- The original performance problem.
- The root cause.
- Changes made.
- Tests performed.
- Before-and-after measurements.
- Remaining limitations.
- Recommended next steps.

## 20. Prohibited Practices

Never:

- Optimize without measuring the original problem.
- Add indexes without examining query patterns.
- Remove constraints casually.
- Disable database security for performance.
- Expose sensitive data in monitoring systems.
- Run uncontrolled benchmarks against production.
- Change transaction isolation without understanding the consequences.
- Introduce caching without invalidation rules.
- Increase connection limits without resource analysis.
- Introduce sharding unnecessarily.
- Claim performance improvements without measurements.
- Ignore data integrity when optimizing queries.

## 21. Definition of Done

A database performance task is complete when:

- The performance problem has been investigated.
- A measurable baseline exists where practical.
- The root cause has been identified or remaining uncertainty documented.
- Optimizations have been implemented safely.
- Functional behavior is preserved.
- Relevant tests have passed.
- Performance has been measured after the changes.
- Security and data integrity remain intact.
- Important trade-offs are documented.
- Remaining performance limitations are reported.

## 22. Final Engineering Rule

Always optimize the actual workload rather than an imagined workload.

A good database optimization must improve measurable performance while preserving correctness, security, maintainability, and reliability.