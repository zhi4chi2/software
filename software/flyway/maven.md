# First Steps
https://flywaydb.org/getstarted/firststeps/maven


pom.xml
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>org.example.demo</groupId>
  <artifactId>demo-flyway</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>jar</packaging>

  <name>demo-flyway</name>

  <build>
    <plugins>
      <plugin>
        <groupId>org.flywaydb</groupId>
        <artifactId>flyway-maven-plugin</artifactId>
        <version>4.2.0</version>
        <configuration>
          <url>jdbc:postgresql://localhost:5432/test</url>
          <user>postgres</user>
          <password>postgres</password>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>9.4.1212</version>
          </dependency>
        </dependencies>
      </plugin>
    </plugins>
  </build>
</project>
```


src/main/resources/db/migration/V1__Create_person_table.sql
```sql
create table PERSON (
    ID int not null,
    NAME varchar(100) not null
);
```


执行 `mvn flyway:migrate` 输出
```
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building demo-flyway 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO]
[INFO] --- flyway-maven-plugin:4.2.0:migrate (default-cli) @ demo-flyway ---
[INFO] Flyway 4.2.0 by Boxfuse
[INFO] Database: jdbc:postgresql://localhost:5432/test (PostgreSQL 9.1)
[INFO] Successfully validated 1 migration (execution time 00:00.011s)
[INFO] Creating Metadata table: "public"."schema_version"
[INFO] DB: ALTER TABLE / ADD PRIMARY KEY 将要为表 "schema_version" 创建隐含索引 "schema_version_pk"
[INFO] Current version of schema "public": << Empty Schema >>
[INFO] Migrating schema "public" to version 1 - Create person table
[INFO] Successfully applied 1 migration to schema "public" (execution time 00:00.357s).
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.291 s
[INFO] Finished at: 2017-06-23T10:34:00+08:00
[INFO] Final Memory: 7M/114M
[INFO] ------------------------------------------------------------------------
```


注意初始时数据库要是空的，不能有任何表，否则报异常 org.flywaydb.core.api.FlywayException: Found non-empty schema(s) "public" without metadata table! Use baseline() or set baselineOnMigrate to true to initialize the metadata table.


添加 src/main/resources/db/migration/V2__Add_people.sql
```sql
insert into PERSON (ID, NAME) values (1, 'Axel');
insert into PERSON (ID, NAME) values (2, 'Mr. Foo');
insert into PERSON (ID, NAME) values (3, 'Ms. Bar');
```


再次执行 `mvn flyway:migrate` 输出
```
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building demo-flyway 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO]
[INFO] --- flyway-maven-plugin:4.2.0:migrate (default-cli) @ demo-flyway ---
[INFO] Flyway 4.2.0 by Boxfuse
[INFO] Database: jdbc:postgresql://localhost:5432/test (PostgreSQL 9.1)
[INFO] Successfully validated 2 migrations (execution time 00:00.017s)
[INFO] Current version of schema "public": 1
[INFO] Migrating schema "public" to version 2 - Add people
[INFO] Successfully applied 1 migration to schema "public" (execution time 00:00.031s).
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 0.960 s
[INFO] Finished at: 2017-06-23T10:36:17+08:00
[INFO] Final Memory: 7M/114M
[INFO] ------------------------------------------------------------------------
```


# Overview
https://flywaydb.org/documentation/maven/


## Goals
FIXME


## Configuration
### Directly in the configuration of the plugin
Due to a long standing Maven bug it is not possible to configure empty values this way. You must use one of the other configurations ways instead. 


### Through Maven properties
FIXME


### Through an external config file
FIXME


### Through System properties
FIXME


### Overriding order
从高到低
- System properties
- External config file
- Maven properties
- Plugin configuration


## Authentication
FIXME


# Migrate
## Default Phase
pre-integration-test


## Usage
## Configuration
部分
- table - 默认 schema_version
- locations - 默认 filesystem:src/main/resources/db/migration
- sqlMigrationPrefix - 默认 V
- repeatableSqlMigrationPrefix - 默认 R
- sqlMigrationSeparator - 默认 __
- sqlMigrationSuffix - 默认 .sql
- encoding - 默认 UTF-8
- placeholderPrefix - 默认 ${
- placeholderSuffix - 默认 }
- target - 默认 latest version ，可以指定为某个版本，或者设为 current 然后通过 MigrationVersion.CURRENT placeholder 指定目标版本


## Sample configuration
## Exposed properties
## Sample output
执行 `mvn compile flyway:migrate`


# Clean
https://flywaydb.org/documentation/maven/clean

