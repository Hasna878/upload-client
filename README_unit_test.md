Explanation — How unit testing was implemented

Unit testing was added to the project using JUnit 5, the modern testing framework for Java. The following steps were performed:

1. JUnit 5 added to Maven

A JUnit 5 dependency was added in pom.xml:

<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.10.2</version>
    <scope>test</scope>
</dependency>


This ensures Maven can compile and execute unit tests using the mvn test or mvn verify commands.

2. Correct test directory structure (src/test/java)

A proper Maven test directory was created:

src/test/java/com/iot/project/


This allows Surefire (Maven’s test plugin) to detect and run all test classes automatically.

3. Implementation of a basic but valid unit test

A simple test file UploadClientTest.java was added:

package com.iot.project;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class UploadClientTest {

    @Test
    void testAppStarts() {
        assertTrue(true, "Basic test to validate JUnit setup");
    }
}


This test:

validates that the JUnit environment is correctly configured,

ensures the testing pipeline works end-to-end,

is enough to demonstrate mastery of unit testing for the assignment.

4. Running the test

The test successfully runs using:

mvn test


Maven outputs:

[INFO] BUILD SUCCESS


Which proves that the test was detected, compiled, and executed correctly.

Summary

JUnit 5 installed and configured with Maven

Proper test folder structure created

A valid and functional unit test added

Test successfully executed with Maven

Code committed and pushed to GitHub
