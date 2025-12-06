Explanation – how logging was set up and used

Logging is implemented using the SLF4J API with Logback as the concrete logging backend.

Add logging dependencies in pom.xml

The following dependencies were added inside the <dependencies> section:

<!-- Logging: SLF4J API -->
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-api</artifactId>
    <version>1.7.36</version>
</dependency>

<!-- Logging: Logback implementation -->
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.4.14</version>
</dependency>


This provides a standard logging abstraction (SLF4J) and a concrete implementation (Logback) at runtime.

Logger declaration in UploadClient

In UploadClient.java, the SLF4J logger is declared as a static field:

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class UploadClient {

    private static final Logger logger = LoggerFactory.getLogger(UploadClient.class);

    // ...
}


This logger is then used throughout the class.

INFO and DEBUG logs (normal execution and diagnostic details)

At the start of the main method, logging is used to indicate that the application has started and to record the arguments:

public static void main(String[] args) {
    logger.info("Starting UploadClient application...");
    logger.debug("Program started with {} argument(s): {}", args.length, java.util.Arrays.toString(args));
    // ...
}


INFO indicates a normal, high-level event (application start).

DEBUG provides more detailed technical information (arguments) useful when debugging.

WARN log (suspicious but non-fatal situation)

A WARN log is used to report a potentially incorrect usage scenario that does not immediately stop the program:

if (args.length == 0) {
    logger.warn("No arguments were provided to UploadClient. Using default configuration.");
}


This warns that the program is running without explicit arguments and falls back to default behaviour.

ERROR log (unexpected failure)

The main execution is wrapped in a try/catch block, and any unexpected exception is logged at ERROR level:

try {
    // main execution logic (local for now: reading files, preparing data, etc.)
} catch (Exception e) {
    logger.error("Unexpected error during UploadClient execution: {}", e.getMessage(), e);
}


This ensures that critical failures are visible in the logs and include the full stack trace (e), which is essential for diagnosing runtime problems.
