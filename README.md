# Unit Testing & Logging — Spring Boot Project

This project demonstrates:
- **JUnit 5** unit tests for a service class.
- **Mockito** mocks for the repository, so unit tests do not need a database.
- **SLF4J + Logback** logging for important service events.
- **Maven Surefire** test reports.
- **JaCoCo** code coverage reports.
- A runnable REST API backed by an in-memory H2 database.

## Requirements
- JDK 17 or newer
- Maven 3.6.3 or newer
- Eclipse IDE (optional)

## Run from a terminal
1. Extract the ZIP.
2. Open a terminal in the `unit-testing-logging` folder (the folder containing `pom.xml`).
3. Run tests and create reports:

   ```bash
   mvn clean verify
   ```

4. Start the application:

   ```bash
   mvn spring-boot:run
   ```

The API starts at `http://localhost:8080`.

## Test and coverage reports
After `mvn clean verify`:
- JUnit/Surefire report: `target/surefire-reports/`
- JaCoCo HTML coverage report: `target/site/jacoco/index.html`
- XML coverage report: `target/site/jacoco/jacoco.xml`

Open `target/site/jacoco/index.html` in a browser to view coverage. Reports are generated on your machine when Maven runs; they are not pre-generated in this source ZIP.

## Sample API requests
Create an employee:

```bash
curl -X POST http://localhost:8080/api/employees \
  -H "Content-Type: application/json" \
  -d "{\"name\":\"Asha Kumar\",\"email\":\"asha@example.com\",\"department\":\"Engineering\"}"
```

List employees:

```bash
curl http://localhost:8080/api/employees
```

Get one employee (replace `1` with the returned ID):

```bash
curl http://localhost:8080/api/employees/1
```

Update an employee:

```bash
curl -X PUT http://localhost:8080/api/employees/1 \
  -H "Content-Type: application/json" \
  -d "{\"name\":\"Asha Kumar\",\"email\":\"asha@example.com\",\"department\":\"Platform\"}"
```

Delete an employee:

```bash
curl -X DELETE http://localhost:8080/api/employees/1
```

## Run in Eclipse
1. Install/configure JDK 17 and Maven in Eclipse.
2. Select **File → Import → Maven → Existing Maven Projects**.
3. Browse to the extracted project folder and select its `pom.xml`.
4. Right-click the project → **Maven → Update Project**.
5. To test: right-click the project → **Run As → Maven build...**, enter `clean verify`, and click **Run**.
6. To start: right-click the main class `UnitTestingLoggingApplication.java` → **Run As → Spring Boot App** (or run `spring-boot:run` as a Maven build).

## Logging
Logback configuration is in `src/main/resources/logback-spring.xml`. Logs are written to the console and `logs/application.log`. The repository is intentionally mocked in service unit tests, keeping the tests fast and isolated.

## Notes
- The H2 database is in-memory; data resets when the application restarts.
- If port 8080 is already in use, set `server.port=8081` in `src/main/resources/application.properties`, then use port 8081 in the URLs.
