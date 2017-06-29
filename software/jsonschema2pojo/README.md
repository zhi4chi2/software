# Maven plugin
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

  <artifactId>demo-jsonschema2pojo</artifactId>
  <packaging>jar</packaging>

  <name>demo-jsonschema2pojo</name>

  <dependencies>
    <dependency>
      <groupId>org.apache.commons</groupId>
      <artifactId>commons-lang3</artifactId>
      <version>3.6</version>
    </dependency>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.7.0</version>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.jsonschema2pojo</groupId>
        <artifactId>jsonschema2pojo-maven-plugin</artifactId>
        <version>0.4.37</version>
        <configuration>
          <sourceDirectory>${basedir}/src/main/resources/json</sourceDirectory>
          <targetPackage>org.example.demo.jsonschema2pojo</targetPackage>
          <sourceType>json</sourceType>
          <useBigDecimals>true</useBigDecimals>
          <useCommonsLang3>true</useCommonsLang3>
          <annotationStyle>none</annotationStyle>
          <includeAdditionalProperties>false</includeAdditionalProperties>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>generate</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```


src/main/resources/json/info.js
```javascript
{
  "a" : "aa",
  "b" : 1.1,
  "c" : false
}
```


则将生成 target/java-gen/org/example/demo/jsonschema2pojo/Info.java
```java

package org.example.demo.jsonschema2pojo;

import java.math.BigDecimal;
import org.apache.commons.lang3.builder.EqualsBuilder;
import org.apache.commons.lang3.builder.HashCodeBuilder;
import org.apache.commons.lang3.builder.ToStringBuilder;

public class Info {

    private String a;
    private BigDecimal b;
    private Boolean c;

    public String getA() {
        return a;
    }

    public void setA(String a) {
        this.a = a;
    }

    public BigDecimal getB() {
        return b;
    }

    public void setB(BigDecimal b) {
        this.b = b;
    }

    public Boolean getC() {
        return c;
    }

    public void setC(Boolean c) {
        this.c = c;
    }

    @Override
    public String toString() {
        return ToStringBuilder.reflectionToString(this);
    }

    @Override
    public int hashCode() {
        return new HashCodeBuilder().append(a).append(b).append(c).toHashCode();
    }

    @Override
    public boolean equals(Object other) {
        if (other == this) {
            return true;
        }
        if ((other instanceof Info) == false) {
            return false;
        }
        Info rhs = ((Info) other);
        return new EqualsBuilder().append(a, rhs.a).append(b, rhs.b).append(c, rhs.c).isEquals();
    }

}
```


# Reference
- http://www.jsonschema2pojo.org/
- https://github.com/joelittlejohn/jsonschema2pojo
- https://github.com/joelittlejohn/jsonschema2pojo/wiki/Getting-Started
- https://github.com/joelittlejohn/jsonschema2pojo/wiki/Reference - JSON Schema Reference
- https://joelittlejohn.github.io/jsonschema2pojo/site/0.4.37/generate-mojo.html - maven plugin 的文档
- http://json2java.azurewebsites.net/ - FIXME 另外一种类似的工具

