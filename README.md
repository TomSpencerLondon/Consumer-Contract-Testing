


We run the consumer contract tests with:
```bash
mvn clean test
```
This error shows if we change our API:
```bash
.   ____          _            __ _ _
/\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
\\/  ___)| |_)| | | | | || (_| |  ) ) ) )
'  |____| .__|_| |_|_| |_\__, | / / / /
=========|_|==============|___/=/_/_/_/
:: Spring Boot ::                (v2.5.2)

2023-04-05 12:47:44.563  INFO 378321 --- [           main] com.saggu.cdc.ProviderApplicationTests   : Starting ProviderApplicationTests using Java 17.0.6 on tom-ubuntu with PID 378321 (started by tom in /home/tom/Projects/consumer-driven-contract/service-provider)
2023-04-05 12:47:44.564  INFO 378321 --- [           main] com.saggu.cdc.ProviderApplicationTests   : No active profile set, falling back to default profiles: default
2023-04-05 12:47:45.586  INFO 378321 --- [           main] com.saggu.cdc.ProviderApplicationTests   : Started ProviderApplicationTests in 1.058 seconds (JVM running for 7.296)
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 1.027 s - in com.saggu.cdc.ProviderApplicationTests
[INFO]
[INFO] Results:
[INFO]
[ERROR] Errors:
[ERROR]   ContractVerifierTest.validate_order_for_client1:35 » IllegalState Parsed JSON ...
[INFO]
[ERROR] Tests run: 2, Failures: 0, Errors: 1, Skipped: 0
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  14.392 s
[INFO] Finished at: 2023-04-05T12:47:46+01:00
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:2.22.2:test (default-test) on project service-provider: There are test failures.
[ERROR]
[ERROR] Please refer to /home/tom/Projects/consumer-driven-contract/service-provider/target/surefire-reports for the individual test results.
[ERROR] Please refer to dump files (if any exist) [date].dump, [date]-jvmRun[N].dump and [date].dumpstream.
[ERROR] -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MojoFailureException


```
