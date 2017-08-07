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

  <parent>
    <groupId>org.example.demo</groupId>
    <artifactId>demo-parent</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <relativePath>../pom.xml</relativePath>
  </parent>

  <artifactId>demo-flyway</artifactId>
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

    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
    </dependency>
    <dependency>
      <groupId>ch.qos.logback</groupId>
      <artifactId>logback-classic</artifactId>
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


测试：
- 新建 test 数据库
- 执行 Test.java
- 查看数据库


## Programmatic Configuration (Android)
FIXME


## Spring Configuration
pom.xml
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>org.example.demo</groupId>
    <artifactId>demo-parent</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <relativePath>../pom.xml</relativePath>
  </parent>

  <artifactId>demo-flyway</artifactId>
  <packaging>jar</packaging>

  <name>demo-flyway</name>

  <dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-framework-bom</artifactId>
        <version>4.3.9.RELEASE</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>

      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <exclusions>
          <exclusion>
            <groupId>commons-logging</groupId>
            <artifactId>commons-logging</artifactId>
          </exclusion>
        </exclusions>
      </dependency>
    </dependencies>
  </dependencyManagement>

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

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-orm</artifactId>
    </dependency>
    <dependency>
      <groupId>org.hibernate</groupId>
      <artifactId>hibernate-core</artifactId>
      <version>5.2.10.Final</version>
    </dependency>
    <dependency>
      <groupId>org.hibernate</groupId>
      <artifactId>hibernate-entitymanager</artifactId>
      <version>5.2.10.Final</version>
    </dependency>
    <dependency>
      <groupId>commons-dbcp</groupId>
      <artifactId>commons-dbcp</artifactId>
      <version>1.4</version>
    </dependency>

    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
    </dependency>
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>jcl-over-slf4j</artifactId>
      <version>${slf4j.version}</version>
    </dependency>
    <dependency>
      <groupId>ch.qos.logback</groupId>
      <artifactId>logback-classic</artifactId>
    </dependency>
  </dependencies>
</project>
```


src/main/resources/spring/spring-service.xml
```xml
<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:p="http://www.springframework.org/schema/p" xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
  <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close" p:driverClassName="org.postgresql.Driver"
    p:url="jdbc:postgresql://localhost:5432/test" p:username="postgres" p:password="postgres" />

  <bean id="flyway" class="org.flywaydb.core.Flyway" init-method="migrate">
    <property name="dataSource" ref="dataSource" />
    <property name="locations">
      <list>
        <value>org/example/demo/flyway/db/migration</value>
      </list>
    </property>
  </bean>

  <bean id="sessionFactory" class="org.springframework.orm.hibernate5.LocalSessionFactoryBean" depends-on="flyway">
    <property name="dataSource" ref="dataSource" />
  </bean>
</beans>
```


```java
package org.example.demo.flyway.db.migration;

import org.flywaydb.core.api.migration.spring.SpringJdbcMigration;
import org.springframework.jdbc.core.JdbcTemplate;

public class V1__Create_Person_Table implements SpringJdbcMigration {
    public void migrate(JdbcTemplate jdbcTemplate) throws Exception {
        StringBuilder sql = new StringBuilder();
        sql.append(" create table PERSON (");
        sql.append("     ID int not null,");
        sql.append("     NAME varchar(100) not null");
        sql.append(" )");
        jdbcTemplate.execute(sql.toString());
    }
}
```


```java
package org.example.demo.flyway.db.migration;

import java.util.HashMap;
import java.util.Map;

import org.flywaydb.core.api.migration.MigrationChecksumProvider;
import org.flywaydb.core.api.migration.spring.SpringJdbcMigration;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.simple.SimpleJdbcInsert;

public class R__Init_Data implements SpringJdbcMigration, MigrationChecksumProvider {
    public Integer getChecksum() {
        return 1;
    }

    public void migrate(JdbcTemplate jdbcTemplate) throws Exception {
        jdbcTemplate.execute("delete from PERSON");

        SimpleJdbcInsert insert = new SimpleJdbcInsert(jdbcTemplate).withTableName("PERSON");

        Map<String, Object> args = new HashMap<String, Object>();
        args.put("ID", 1);
        args.put("NAME", "Axel");
        insert.execute(args);

        args.put("ID", 2);
        args.put("NAME", "Mr. Foo");
        insert.execute(args);

        args.put("ID", 3);
        args.put("NAME", "Ms. Bar");
        insert.execute(args);
    }
}
```


```java
package org.example.demo.flyway;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext applicationContext = new ClassPathXmlApplicationContext("spring/*.xml");
        applicationContext.close();
    }
}
```


注意：
- spring-service.xml 中 sessionFactory bean depends-on="flyway" 因为 flyway 可能创建新表，所以必须保证 flyway 先执行。
- R\_\_Init\_Data 实现 MigrationChecksumProvider ，并且在每次修改时都应该修改 getChecksum 的返回值，以通知 flyway 重新执行。
- V1\_\_Create\_Person\_Table 不需要实现 V1\_\_Create\_Person\_Table 是因为 versioned migrations 都不应该修改！
- 这里测试了 java migration ，当然也可以使用 sql migration


测试：
- 新建 test 数据库
- 执行 Test.java
- 查看数据库
