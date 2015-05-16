Reflections Maven plugin
------------------------

#####This project is DISCONTINUED

It is [MUCH](http://stackoverflow.com/questions/19813097/is-it-possible-to-use-reflections-maven-to-scan-for-classes-inside-jars-in-web-i) MUCH easier (and sane) to integrate Reflections into your Maven build using gmavenplus-plugin.
That is, using a simple Groovy script to instantiate Reflections as you need, without the hassle of using (and writing) a Maven plugin...

For example:

```xml
<plugin>
    <groupId>org.codehaus.gmavenplus</groupId>
    <artifactId>gmavenplus-plugin</artifactId>
    <version>1.5</version>
    <executions>
        <execution>
            <phase>generate-resources</phase>
            <goals>
                <goal>execute</goal>
            </goals>
            <configuration>
                <scripts>
                    <script><![CDATA[
                        new org.reflections.Reflections("f.q.n")
                            .save("${project.build.outputDirectory}/META-INF/reflections/${project.artifactId}-reflections.xml")
                    ]]></script>
                </scripts>
            </configuration>
        </execution>
    </executions>
    <dependencies>
        <dependency>
            <groupId>org.reflections</groupId>
            <artifactId>reflections</artifactId>
            <!-- use latest version of Reflections -->
            <version>0.9.10</version>
        </dependency>
        <dependency>
            <groupId>org.codehaus.groovy</groupId>
            <artifactId>groovy-all</artifactId>
            <!-- any version of Groovy \>= 1.5.0 should work here -->
            <version>2.4.3</version>
            <scope>runtime</scope>
        </dependency>
    </dependencies>
</plugin>
```

Later on, when your project is bootstrapping you can let Reflections collect all those resources and re-create that metadata for you, 
making it available at runtime without re-scanning the classpath:

```java
Reflections reflections =
        isProduction() ? Reflections.collect() : new Reflections("your.package.here");
```
