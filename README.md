Reflections Maven plugin
------------------------

Use this maven configuration in your pom file:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.reflections</groupId>
            <artifactId>reflections-maven</artifactId>
            <version>the latest version...</version>
            <executions>
                <execution>
                    <goals>
                        <goal>reflections</goal>
                    </goals>
                    <phase>process-classes</phase>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

Later on, when your project is bootstrapping you can let Reflections collect all those resources and re-create that metadata for you, 
making it available at runtime without re-scanning the classpath:

```java
Reflections reflections =
        isProduction() ? Reflections.collect() : new Reflections("your.package.here");
```

*Check the [ReflectionsMojo](http://code.google.com/p/reflections/wiki/ReflectionsMojo) wiki page*
