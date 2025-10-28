# Java Project Template with Static Analysis and CI/CD

This repository provides a Java Maven project template for creating Java projects with built-in static analysis tools,
code quality checks, dependency management, and CI/CD integration. It is designed to serve as a starting point for new
Java projects, ensuring consistency and quality from the outset.

## Features

* **Maven Project Structure:** Configured for Java 21 with a standard project layout.
* **Code Formatting:** Uses [Spotless](https://github.com/diffplug/spotless)
  with [Palantir Java Format](https://github.com/palantir/palantir-java-format) for consistent code style.
* **Static Analysis:** Integrates [Error Prone](https://errorprone.info/)
  and [NullAway](https://github.com/uber/NullAway) for catching bugs and enforcing null safety.
* **Dependency Management:** Employs
  the [Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/) to enforce rules like banning
  duplicate dependencies and requiring Java 21.
* **CI/CD:** Includes a GitHub Actions workflow for automated builds and Dependabot for dependency updates.
* **IDE Settings:** Pre-configured code style settings for IntelliJ IDEA.
* **Maven Wrapper:** Ensures consistent builds across different environments with Maven 3.9.9 (wrapper version 3.3.2).
* **Consistent Line Endings:** Enforced via `.gitattributes` for cross-platform compatibility.

## How to Use

To start a new project using this template, follow these steps:

* **Clone the Repository:**
  ```bash
  git clone https://github.com/Asapin/statically-analyzed-java.git
  cd your-repo
  ```
* **Update pom.xml:**
    * Modify the `groupId`, `artifactId`, and `version` to match your project.
    * Example:
      ```xml
      <groupId>io.company</groupId>
      <artifactId>app</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      ```
* **Rename Package Structure** (if necessary):
    * Update the package names in the source files (e.g., `src/main/java/io/company`) to align with your project's
      structure.
* **Start Developing:**
    * Use the included Maven wrapper to build and run your project:
      ```bash
      ./mvnw clean verify
      ```
    * The Maven wrapper ensures you don’t need to install Maven locally, using version 3.9.9 as specified.

## Configuration Details

### Maven Plugins

* **Spotless Maven Plugin:**
    * Formats Java code using Palantir Java Format with the PALANTIR style.
    * Features:
        * Removes unused imports.
        * Formats annotations and Javadoc.
        * Trims trailing whitespace and ensures files end with a newline.
        * Enforces a specific import order (`#, java, org, com, <others>`).
        * Uses 4-space indentation and UNIX line endings (`\n`).
    * Also formats YAML files in `.github/` (e.g., `dependabot.yml`, `build.yml`) with 2-space indentation.
* **Maven Enforcer Plugin:**
    * Enforces rules such as:
        * Banning duplicate POM dependency versions and dynamic versions.
        * Excluding vulnerable dependencies (e.g., Log4j versions < 2.17.0).
        * Ensuring dependency convergence.
        * Requiring `Java 21`.
    * Fails the build if any rule is violated.
* **Maven Compiler Plugin:**
    * Compiles with Java 21.
    * Integrates Error Prone and NullAway for static analysis.
        * **Error Prone:**
            * Detects common programming bugs during compilation.
            * Configured to fail the build on warnings to ensure high-quality code.
        * **NullAway:**
            * Provides comprehensive nullness analysis during compilation.
            * Prevents potential `NullPointerException`s by requiring proper null annotations.
    * Configured to fail on warnings to maintain code quality.
    * Uses JSpecify annotations for null safety within the `io.company` package.

### Dependencies

* **JSpecify:**
    * Provides annotations for null safety, used in conjunction with NullAway.

### Code Style

* **Import Order:** Groups imports as: `java`, `javax`, `org`, `com`, `others` and `static imports`, with blank lines between
  groups.
* Indentation: Uses 4 spaces for Java code, 2 spaces for YAML.
* Line Endings: Ensures UNIX-style line endings (`\n`) for all files.

### YAML Formatting

* Spotless formats YAML files in the `.github/` directory, ensuring consistent 2-space indentation and UNIX line
  endings.

### CI/CD Setup

#### GitHub Actions

* **Workflow File:** `.github/workflows/build.yml`
* **Triggers:**
    * Pushes to the `main` branch.
    * Pull requests.
* **Jobs:**
    * Runs on `ubuntu-latest` with Java 21 (Temurin distribution).
    * Steps:
        * Maximizes disk space for the build environment.
        * Sets up Java 21.
        * Checks out the code.
        * Grants execution permissions to the Maven wrapper.
        * Builds the project with `./mvnw clean verify -T 2.0C --batch-mode`.
        * Extracts the `artifactId` and `version` from the POM.
        * Uploads the resulting `.jar` file as an artifact (e.g., `app-0.0.1-SNAPSHOT.jar`).

#### Dependabot

* **Configuration File:** `.github/dependabot.yml`
* **Updates:**
    * Checks daily for updates to:
        * Maven dependencies (in `/`).
        * GitHub Actions configurations (in `/`).

### IDE Settings

The template includes IntelliJ IDEA settings for consistent code style:

* **External Dependencies:**
    * Configured to use Palantir Java Format (see `.idea/externalDependencies.xml`).
* **Code Style:**
    * Import layout matches the Spotless configuration (see `.idea/codeStyles/Project.xml`).
    * Applied automatically when opening the project in IntelliJ IDEA.

These settings are stored in the `.idea/` directory.

### Build Configurations

The following build configurations are pre-set and can be used in your IDE:

* **[Clean] With tests:**
  ```bash
  clean verify -T 1.0C
  ```
* **[Clean] Without tests:**
  ```bash
  clean verify -T 1.0C -Dmaven.test.skip=true
  ```
* **[Incremental] With tests:**
  ```bash
  verify -T 1.0C
  ```
* **[Incremental] Without tests:**
  ```bash
  verify -T 1.0C -Dmaven.test.skip=true
  ```
* **[Spotless] Fix code style:**
  ```bash
  spotless:apply
  ```

These commands use `-T 1.0C` for parallel builds with one thread per CPU core.

### Additional Notes

* **.gitattributes:**
    * Ensures all text files use UNIX-style line endings (`\n`) with `* text eol=lf`, promoting cross-platform
      consistency.

## Contributing

Contributions are welcome! Feel free to open issues or submit pull requests to improve this template or add more
features.
