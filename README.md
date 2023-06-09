### Spring contract testing
https://cloud.spring.io/spring-cloud-contract/2.1.x/multi/multi__spring_cloud_contract_verifier_introduction.html

https://www.youtube.com/watch?v=9cpXaEr3C5o

Jasvinder S Saggu:
https://saggu.medium.com/consumer-driven-contracts-using-spring-cloud-contract-f5bce1d01b8a

He also writes about the SAGA distributed transactions pattern:
https://saggu.medium.com/saga-distributed-transactions-pattern-using-apache-camel-microservices-design-pattern-9625131dbaa2

This is the swagger ui:
![image](https://user-images.githubusercontent.com/27693622/230075087-004e21ea-1d07-4f86-b1fb-a5e381c0ecab.png)

but it doesn't test what we have promised to applications that consume our service.

We run the provider contract tests with:
```bash
mvn clean test
```

The groovy script creates this test for us:
```java
public class ContractVerifierTest extends CdcBaseClass {

	@Test
	public void validate_order_for_client1() throws Exception {
		// given:
			MockMvcRequestSpecification request = given();


		// when:
			ResponseOptions response = given().spec(request)
					.get("/orders/1");

		// then:
			assertThat(response.statusCode()).isEqualTo(200);
			assertThat(response.header("Content-Type")).matches("application/json.*");

		// and:
			DocumentContext parsedJson = JsonPath.parse(response.getBody().asString());
			assertThatJson(parsedJson).field("['orderId']").isEqualTo("1");
			assertThatJson(parsedJson).field("['itemName']").isEqualTo("Sony TV");
			assertThatJson(parsedJson).field("['price']").isEqualTo(500.0);
			assertThatJson(parsedJson).field("['units']").isEqualTo(1);
	}

}

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
