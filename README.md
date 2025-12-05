Static Code Analysis Setup (Checkstyle)

For the upload-client module of my AWS Java project, I configured Checkstyle as a static code analysis tool. Checkstyle analyses the Java source code without executing it and reports style and formatting issues.

I created a configuration file at:

config/checkstyle/checkstyle.xml

This file defines the rules used by Checkstyle, for example:

maximum line length of 120 characters,

4-space indentation,

mandatory braces for control structures (if, for, while, …),

whitespace and formatting conventions.

Checkstyle is integrated into the Maven build using the maven-checkstyle-plugin in pom.xml. The plugin is declared inside the <build><plugins> section and references the custom configuration file:

<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-checkstyle-plugin</artifactId>
    <version>3.3.1</version>
    <configuration>
        <configLocation>config/checkstyle/checkstyle.xml</configLocation>
        <failsOnError>true</failsOnError>
        <linkXRef>false</linkXRef>
    </configuration>
    <executions>
        <execution>
            <id>checkstyle-validation</id>
            <phase>verify</phase>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
</plugin>

How to run the analysis

Prerequisites:

Java (JDK 17)

Maven installed and available on the command line

From the upload-client directory, the static analysis can be executed with:

mvn verify


During the verify phase, Maven automatically invokes Checkstyle using the specified configuration file. If no violations are found, the build ends with BUILD SUCCESS. If there are style violations, Maven reports them in the console and the build fails, which enforces code quality rules.

You can adjust the wording a bit if you want, but this already fits the requirement:

“Proof: link to configuration and explanation of how to install and run analysis.”
