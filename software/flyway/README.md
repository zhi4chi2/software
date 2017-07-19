# Overview
https://flywaydb.org/documentation/migration/


Within a single migration run, repeatable migrations are always applied last, after all pending versioned migrations have been executed. Repeatable migrations are applied in the order of their description.


Within a single migration, all statements are run within a single transaction.


# Versioned migrations
https://flywaydb.org/documentation/migration/versioned


## Usages
## Versions
versioned migration must have a unique version and a description


version example
- 1
- 001
- 5.2
- 5_2 (5.2 at runtime) - Underscores are replaced by dots at runtime


# Repeatable migrations
## Usages
- (Re-)creating views/procedures/functions/packages/...
- Bulk reference data reinserts


# Sql-based migrations
## Typical usage
## Location and discovery
New sql migrations are discovered automatically through classpath and file system scanning at runtime.
This scanning is recursive. All migrations in directories below the specified ones are also picked up.


## Naming
file name consists of
- prefix
- version
- separator - 默认 __
- description - Underscores or spaces separate the words
- suffix


## Placeholder replacement


# Java-based migrations
## Typical usage
- BLOB & CLOB changes
- Advanced bulk data changes (Recalculations, advanced format changes, ...)


## Location and discovery
New java migrations are discovered automatically through classpath scanning at runtime. The scanning is recursive. Java migrations in subpackages of the specified ones are also picked up.


## Naming
必须实现 JdbcMigration 接口。


## Checksums and Validation
FIXME


## Spring support (Optional)
实现 SpringJdbcMigration 接口


FIXME


# Configuration
注意使用不同运行方式(command line, java, maven...)时的配置项的默认值可能是不一样的。


# 术语
- metadata table - 即 schema_version 表，是 flyway 创建并维护的。
- migrations - 即用 SQL/java 写的调整数据库的文件。可以是 versioned or repeatable
  - versioned migrations have a unique version and are applied exactly once.
  - repeatable migrations do not have a version. Instead they are (re-)applied every time their checksum changes. 这种 migrations 应该在开头有 drop 语句或者 CREATE OR REPLACE 。
- pending versioned migrations - 某次执行时，与数据库比对，还没执行将要执行的 migration
- migration state
  - resolved/pending - have been detected by Flyway's filesystem and classpath scanner.
  - applied - executed against the database
  - success
  - failed - migration fails and the database doesn't supports DDL transactions, the migration is marked as failed in the metadata table, indicating manual database cleanup may be required.
  - outdated - repeatable migrations whose checksum has changed since they are last applied


# Basic Practice
- 当使用 java repeatable migration 时，应该实现 MigrationChecksumProvider 接口，并且当需要重新执行(repeat)时，修改 getChecksum() 的返回值。否则 flyway 不知道该 java 类有没有更改过，因此不会 repeat 执行。而 flyway 对 sql migration 可以自动计算 checksum


# Reference
- https://flywaydb.org/
- https://github.com/flyway/flyway
