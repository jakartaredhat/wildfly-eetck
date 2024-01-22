# wildfly-eetck
Example runner for WildFly and the updated Arquillian/Junit5 EE TCK tests

## Preparing to run the tests
In order to run these tests, the WildFly Arquillian container and the Jakarta EE TCK Arquillian/Junit5 tests must be built.
There are two repositories to clone and build:

Build the WildFly Arquillian container:
git clone https://github.com/starksm64/wildfly-arquillian.git
cd wildfly-arquillian
git checkout appclient
mvn install

Build the Jakarta EE TCK Arquillian/Junit5 tests:
git clone https://github.com/jakartaredhat/jakartaee-tck.git
cd jakartaee-tck
git checkout ejb-arq-test
mvn install

## Running the tests from the command line
From within the wildfly-eetck directory, run the following command:
mvn test


The current status of the 3 test classes is:
```bash
(base) starksm@Scotts-Mac-Studio wildfly-eetck % mvn test
[INFO] Scanning for projects...
...
[INFO] --- maven-surefire-plugin:3.1.2:test (default-test) @ wildfly-tck-runner ---
[INFO] Tests are skipped.
[INFO] 
[INFO] --- maven-surefire-plugin:3.1.2:test (appclient-tests-tck) @ wildfly-tck-runner ---
[INFO] Using auto detected provider org.apache.maven.surefire.junitplatform.JUnitPlatformProvider
[INFO] 
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.sun.ts.tests.ejb30.bb.session.stateless.basic.ClientTest
[INFO] Tests run: 7, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 60.56 s -- in com.sun.ts.tests.ejb30.bb.session.stateless.basic.ClientTest
[INFO] Running com.sun.ts.tests.ejb30.bb.session.stateless.annotation.appexception.annotated.ClientTest
[ERROR] Tests run: 20, Failures: 0, Errors: 7, Skipped: 0, Time elapsed: 163.8 s <<< FAILURE! -- in com.sun.ts.tests.ejb30.bb.session.stateless.annotation.appexception.annotated.ClientTest
[ERROR] com.sun.ts.tests.ejb30.bb.session.stateless.annotation.appexception.annotated.ClientTest.checkedRollbackAppExceptionTest -- Time elapsed: 8.320 s <<< ERROR!
java.lang.Exception: Test case throws exception: Got expected application exception,expected tx status code 1(STATUS_MARKED_ROLLBACK), but actual 0(STATUS_ACTIVE)
        at org.jboss.as.arquillian.container.protocol.appclient.AppClientMethodExecutor.invoke(AppClientMethodExecutor.java:86)

[ERROR] com.sun.ts.tests.ejb30.bb.session.stateless.annotation.appexception.annotated.ClientTest.uncheckedRollbackAppExceptionTest -- Time elapsed: 8.192 s <<< ERROR!
java.lang.Exception: Test case throws exception: Got unexpected exception:
        at org.jboss.as.arquillian.container.protocol.appclient.AppClientMethodExecutor.invoke(AppClientMethodExecutor.java:86)
 
[ERROR] com.sun.ts.tests.ejb30.bb.session.stateless.annotation.appexception.annotated.ClientTest.uncheckedAppExceptionTest2 -- Time elapsed: 8.225 s <<< ERROR!
java.lang.Exception: Test case throws exception: Got unexpected exception:
        at org.jboss.as.arquillian.container.protocol.appclient.AppClientMethodExecutor.invoke(AppClientMethodExecutor.java:86)
 
[ERROR] com.sun.ts.tests.ejb30.bb.session.stateless.annotation.appexception.annotated.ClientTest.uncheckedAppExceptionTestLocal -- Time elapsed: 8.231 s <<< ERROR!
java.lang.Exception: Test case throws exception: Got unexpected exception:
        at org.jboss.as.arquillian.container.protocol.appclient.AppClientMethodExecutor.invoke(AppClientMethodExecutor.java:86)

[ERROR] com.sun.ts.tests.ejb30.bb.session.stateless.annotation.appexception.annotated.ClientTest.uncheckedRollbackAppExceptionTestLocal -- Time elapsed: 8.211 s <<< ERROR!
java.lang.Exception: Test case throws exception: Got unexpected exception:
        at org.jboss.as.arquillian.container.protocol.appclient.AppClientMethodExecutor.invoke(AppClientMethodExecutor.java:86)

[ERROR] com.sun.ts.tests.ejb30.bb.session.stateless.annotation.appexception.annotated.ClientTest.uncheckedAppExceptionTest -- Time elapsed: 8.141 s <<< ERROR!
java.lang.Exception: Test case throws exception: com.sun.ts.tests.ejb30.common.appexception.UncheckedAppException
        at org.jboss.as.arquillian.container.protocol.appclient.AppClientMethodExecutor.invoke(AppClientMethodExecutor.java:86)

[ERROR] com.sun.ts.tests.ejb30.bb.session.stateless.annotation.appexception.annotated.ClientTest.checkedRollbackAppExceptionTestLocal -- Time elapsed: 8.257 s <<< ERROR!
java.lang.Exception: Test case throws exception: Got expected application exception,expected tx status code 1(STATUS_MARKED_ROLLBACK), but actual 0(STATUS_ACTIVE)
        at org.jboss.as.arquillian.container.protocol.appclient.AppClientMethodExecutor.invoke(AppClientMethodExecutor.java:86)
 

[INFO] Running com.sun.ts.tests.ejb30.bb.session.stateless.annotation.enventry.ClientTest
[INFO] Tests run: 18, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 147.1 s -- in com.sun.ts.tests.ejb30.bb.session.stateless.annotation.enventry.ClientTest
[INFO] 
[INFO] Results:
[INFO] 
[ERROR] Errors: 
[ERROR]   ClientTest.checkedRollbackAppExceptionTest »  Test case throws exception: Got expected application exception,expected tx status code 1(STATUS_MARKED_ROLLBACK), but actual 0(STATUS_ACTIVE)
[ERROR]   ClientTest.checkedRollbackAppExceptionTestLocal »  Test case throws exception: Got expected application exception,expected tx status code 1(STATUS_MARKED_ROLLBACK), but actual 0(STATUS_ACTIVE)
[ERROR]   ClientTest.uncheckedAppExceptionTest »  Test case throws exception: com.sun.ts.tests.ejb30.common.appexception.UncheckedAppException
[ERROR]   ClientTest.uncheckedAppExceptionTest2 »  Test case throws exception: Got unexpected exception:
[ERROR]   ClientTest.uncheckedAppExceptionTestLocal »  Test case throws exception: Got unexpected exception:
[ERROR]   ClientTest.uncheckedRollbackAppExceptionTest »  Test case throws exception: Got unexpected exception:
[ERROR]   ClientTest.uncheckedRollbackAppExceptionTestLocal »  Test case throws exception: Got unexpected exception:
[INFO] 
[ERROR] Tests run: 45, Failures: 0, Errors: 7, Skipped: 0
[INFO] 
...
```

The failures in the com.sun.ts.tests.ejb30.bb.session.stateless.annotation.appexception.annotated.ClientTest
appear to be due to either missing exception mappings or some other transaction/exception configuration
that is not being set correctly.

## Running the tests from within Intellij
The project has Junit run configurations for the 3 test classes, and the tests can be run from within Intellij.
.
![Sample com.sun.ts.tests.ejb30.bb.session.stateless.basic.ClientTest](images/basic-ClientTest.png)
