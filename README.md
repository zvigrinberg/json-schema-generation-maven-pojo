# json-schema-generation-maven-pojo

## Goal

 To Create Pojos from Json Schemas.

 ## Procedure

 1. Create sample maven project
```shell
mvn archetype:generate -DgroupId=org.zgrinber.example -DartifactId=jsonschema-demo
```

2. Add `json2schemapojo maven plugin to pom.xml:
```xml
 <build>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
            <groupId>org.jsonschema2pojo</groupId>
            <artifactId>jsonschema2pojo-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <sourceDirectory>${basedir}/src/main/resources/schema/sbom-1.4.schema.json</sourceDirectory>
                <targetPackage>org.zgrinber.example</targetPackage>
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
    </pluginManagement>
  </build>
```
3. Add the following two dependencies to pom.xml
```xml
  <dependencies>
    <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
      <version>2.4</version>
    </dependency>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.5.4</version>
    </dependency>
  </dependencies>
``` 
 4. Add the following properties to pom.xml
```xml
 <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>20</maven.compiler.source>
    <maven.compiler.target>20</maven.compiler.target>
  </properties>
```

5. Add to maven-compiler-plugin the following configuration, so it will be like  that:
```xml
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
          <configuration>
            <source>20</source>
            <target>20</target>
          </configuration>
        </plugin>
```
6. Build the java POJOs out of the json schema, using the plugin and its goal `generate`
```shell
 mvn jsonschema2pojo:generate
```
