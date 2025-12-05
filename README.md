Static Code Analysis Setup (Checkstyle)

This project uses Checkstyle as a static code analysis tool. Checkstyle examines the Java source code without executing it and reports formatting issues, style violations, and potential problems.
The goal is to enforce consistent coding standards and improve code readability and maintainability.

📁 Checkstyle Configuration

A custom Checkstyle rule file is provided at:

config/checkstyle/checkstyle.xml


This file defines the style rules applied to the project, including:

Maximum line length: 120 characters

Indentation rules: 4 spaces

Mandatory braces for control structures (if, for, while, etc.)

Enforced whitespace and formatting conventions

These rules are applied automatically during the Maven build process.

🔧 Maven Integration

Checkstyle is integrated through the maven-checkstyle-plugin inside the project's pom.xml.
The plugin executes Checkstyle during the verify phase of the Maven lifecycle.

Extract from pom.xml
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


With this configuration:

The build fails if Checkstyle detects violations

The output clearly displays any issues in the terminal

Running Checkstyle becomes fully automated

▶️ Running Static Code Analysis
Prerequisites

Java 17 (JDK 17)

Apache Maven installed (mvn available in terminal)

Command

From the root of the upload-client module, run:

mvn verify

What Happens

During the verify phase:

Maven compiles the project

Maven triggers the Checkstyle plugin

The plugin reads your configuration file

Style checks run on all Java source files

If the project passes all style rules:

BUILD SUCCESS
You have 0 Checkstyle violations.


If violations are found:

BUILD FAILURE
[ERROR] ... details of the rule violations ...


This ensures consistent code standards throughout the project.
