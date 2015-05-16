Reflections Maven plugin
------------------------

#####This project is DISCONTINUED

It is MUCH MUCH easier (and sane) to integrate Reflections into your Maven build using gmaven-plugin.
That is, using a simple Groovy script to instantiate Reflections as you need, without the hassle of using (and writing) a Maven plugin...

For example:

```xml
<plugin>
    <groupId>org.codehaus.gmaven</groupId>
    <artifactId>gmaven-plugin</artifactId>
    <version>1.5</version>
    <dependencies>
        <dependency>
            <groupId>org.reflections</groupId>
            <artifactId>reflections</artifactId>
            <version>0.9.10</version>
        </dependency>
    </dependencies>
    <executions>
        <execution>
            <phase>generate-resources</phase>
            <goals>
                <goal>execute</goal>
            </goals>
            <configuration>
                <source>
                    new org.reflections.Reflections("f.q.n")
                        .save("${project.build.outputDirectory}/META-INF/reflections/${project.artifactId}-reflections.xml")
                </source>
            </configuration>
        </execution>
    </executions>
</plugin>
```

Later on, when your project is bootstrapping you can let Reflections collect all those resources and re-create that metadata for you, 
making it available at runtime without re-scanning the classpath:

```java
Reflections reflections =
        isProduction() ? Reflections.collect() : new Reflections("your.package.here");
```
