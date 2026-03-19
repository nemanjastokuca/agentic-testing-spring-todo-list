# Repository Guidelines

## Project Structure & Module Organization
`src/main/java/com/nttdata/ta/todo` contains the Spring Boot application code: MVC and REST controllers, the `TodoItem` JPA entity, `TodoItemRepository`, and the `TodoListViewModel`. Server-rendered UI templates live in `src/main/resources/templates` (`base.html`, `index.html`). Runtime configuration is in `src/main/resources/application.properties` and targets MySQL; test overrides live in `src/test/resources/application.properties` and use in-memory H2. Root-level build and CI files are `pom.xml`, `mvnw`, and `Jenkinsfile`. Maven outputs go to `target/`.

## Build, Test, and Development Commands
Use Java 11 for local development.

- `./mvnw clean package`: compile, run tests, and build the WAR in `target/`.
- `./mvnw test`: run the Spring Boot test suite against the H2 test database.
- `./mvnw spring-boot:run`: start the app locally using the main MySQL-backed properties.
- `java -jar target/todo-0.0.1-SNAPSHOT.war`: run the packaged application after a successful build.

Before running locally, update `src/main/resources/application.properties` with valid MySQL connection details.

## Coding Style & Naming Conventions
Keep code in the `com.nttdata.ta.todo` package unless you are deliberately introducing a new package boundary. Follow the existing Java and Thymeleaf style: 4-space indentation, `PascalCase` class names, `camelCase` fields and methods, and clear endpoint names such as `addItem` or `updateItem`. Keep controllers focused on request handling, keep persistence logic in the repository layer, and avoid unrelated formatting-only edits. No formatter or lint configuration is checked in, so consistency with nearby code matters.

## Testing Guidelines
Tests use JUnit 5 through `spring-boot-starter-test`. Add new tests under `src/test/java/com/nttdata/ta/todo`, and name them with the `*Tests` suffix. For controller or persistence changes, prefer Spring Boot integration tests that rely on the H2 settings in `src/test/resources/application.properties`. At minimum, run `./mvnw test` before opening a PR.

## Commit & Pull Request Guidelines
Recent commit subjects are short, imperative, and scoped, for example `Add Jenkinsfile for ci build` and `Use H2 DB for test`. Follow that pattern: one clear action per commit title, no trailing punctuation, and separate unrelated changes. PRs should include a brief summary, test evidence, any MySQL/config changes, linked issues when available, and screenshots for Thymeleaf UI updates.
