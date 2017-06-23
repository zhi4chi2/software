# API
https://flywaydb.org/documentation/api/


## Download
## The Flyway Class
## Programmatic Configuration (Java)
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

  <dependencies>
    <dependency>
      <groupId>org.flywaydb</groupId>
      <artifactId>flyway-core</artifactId>
      <version>4.2.0</version>
    </dependency>
    <dependency>
      <groupId>org.postgresql</groupId>
      <artifactId>postgresql</artifactId>
      <version>9.4.1212</version>
    </dependency>
  </dependencies>
</project>
```


src/main/resources/db/migration/V1__Create_person_table.sql
```sql
create table PERSON (
    ID int not null,
    NAME varchar(100) not null
);
```


src/main/resources/db/migration/V2__Add_people.sql
```sql
insert into PERSON (ID, NAME) values (1, 'Axel');
insert into PERSON (ID, NAME) values (2, 'Mr. Foo');
insert into PERSON (ID, NAME) values (3, 'Ms. Bar');
```


```java
package org.example.demo.flyway;

import org.flywaydb.core.Flyway;

public class Test {
    public static void main(String[] args) {
        Flyway flyway = new Flyway();
        flyway.setDataSource("jdbc:postgresql://localhost:5432/test", "postgres", "postgres");
        flyway.migrate();
    }
}
```


## Programmatic Configuration (Android)
FIXME


## Spring Configuration
FIXME
