# hello-docker-app

```
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=hello-docker-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
```

> edited pom.xml==>

```
<plugin>
          <artifactId>maven-jar-plugin</artifactId>
          <version>3.0.2</version>
                <configuration>
        <archive>
          <manifest>
            <addClasspath>true</addClasspath>
            <classpathPrefix>lib/</classpathPrefix>
            <mainClass>com.mycompany.app.App</mainClass>
          </manifest>
        </archive>
      </configuration>
</plugin>
```
