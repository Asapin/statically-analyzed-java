# Java Project Template with Static Analysis and CI/CD

This repository is a template designed for creating Java projects with built-in static analysis tools, code quality checks, dependency management, and a basic CI/CD setup. It is fully integrated with GitHub Actions and Dependabot to streamline your project's development and maintenance process.

## Features

This template provides the following features and pre-configurations:

### Core Setup
- **Java 21**: Utilizes the latest Long-Term Support (LTS) version of Java.
- **Maven Integration**: Handles dependency management and build automation.

### Tools for Code Quality and Static Analysis
1. **Spotless**:
   - Enforces consistent code formatting using `PALANTIR` style.
   - Automatically removes unused imports, trims trailing whitespaces, ensures files end with a newline, and formats annotations.
   - Supports configured import order and 4-space indentation.
   - Includes formatting rules for both Java and YAML files.

2. **Maven Enforcer Plugin**:
   - Prevents issues like duplicate or dynamic dependency versions.
   - Enforces dependency convergence to avoid version conflicts.
   - Ensures the required Java version (`Java 21`) is used for compilation.
   - Example of banned dependencies for improved security (e.g., bans older vulnerable Log4j versions).

3. **Error Prone**:
   - Detects common programming bugs during compilation.
   - Configured to fail the build on warnings to ensure high-quality code.

4. **NullAway**:
   - Provides comprehensive nullness analysis during compilation.
   - Prevents potential `NullPointerException`s by requiring proper null annotations.

5. **Jspecify**:
   - Leverages a standard set of nullability annotations for integration with tools like NullAway.

### CI/CD Workflow
- **GitHub Actions Workflow**:
  - Configures a basic build workflow (`build.yml`) for continuous integration, ensuring that the codebase always meets quality standards.
  
- **Dependabot Integration**:
  - Keeps your dependencies updated by providing automated pull requests for dependency upgrades.

### Repository Usability
- Designed to be used as a **GitHub Template Repository**, making it easy to initialize new projects with minimal setup effort.

## How to Use

Follow these steps to get started:

1. **Use the Template**:
   - Click the `Use this template` button on GitHub and create a new repository.

2. **Clone Your Repository**:
   ```bash
   git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
   cd YOUR_REPOSITORY
   ```

3. **Configure Your Project**:
    - Update `groupId`, `artifactId`, and `version` in the `pom.xml` with your project's details.
    - Customize the `NullAway:AnnotatedPackages` configuration in `pom.xml` to match your project's base package.

4. **Start Development**:
    - Add your code, and benefit from the built-in quality checks and CI/CD integration.

## Prerequisites

Make sure you have the following installed:
- **Java Development Kit (JDK) 21**
- Use the included Maven wrapper `mvnw`

## Build and Verification

To build the project and execute all quality checks, run:
```
bash ./mvnw clean verify -T 1.0C
``` 

This command will:
- Clean the project directory.
- Run code formatting and static analysis checks via Spotless.
- Enforce dependency and Java version rules using the Maven Enforcer Plugin.
- Compile and analyze code using Error Prone and NullAway.
- Generate and install project artifacts locally.

If there are any issues with code quality or static analysis, the build will fail, providing actionable feedback for resolution.

## Contributing

Contributions are welcome! Feel free to open issues or submit pull requests to improve this template or add more features.

---
**Start building robust and maintainable Java applications today!**
