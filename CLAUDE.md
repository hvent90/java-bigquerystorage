# CLAUDE.md

This is the Google BigQuery Storage Client for Java, a Java idiomatic client for Google BigQuery Storage API that provides high-throughput read and write access to BigQuery tables with support for multiple data formats (Avro, Arrow, Protocol Buffers).

## Tech Stack

- **Language**: Java 8+ (tested on Java 8, 11, 17, 21)
- **Framework**: Google API Extensions for Java (GAX), Google Cloud Client Libraries
- **Runtime**: JVM
- **Build Tool**: Maven 3.x
- **Testing**: JUnit 4.13.2, integration tests with Google Cloud services
- **Package Manager**: Maven
- **Transport**: gRPC
- **Data Formats**: Protocol Buffers, Apache Avro, Apache Arrow, JSON
- **Code Generation**: Protocol Buffer compilation, GAX client generation

## Project Structure

- `google-cloud-bigquerystorage/`: Main client library module with core functionality
- `proto-google-cloud-bigquerystorage-v*/`: Protocol buffer definitions for different API versions (v1, v1alpha, v1beta, v1beta1, v1beta2)
- `grpc-google-cloud-bigquerystorage-v*/`: gRPC client stubs for different API versions
- `google-cloud-bigquerystorage-bom/`: Bill of Materials for dependency management
- `samples/`: Example code and usage demonstrations
- `src/main/java/com/google/cloud/bigquery/storage/`: Main source code organized by API version
- `src/test/java/`: Unit and integration tests
- `.kokoro/`: CI/CD configuration scripts and build automation
- `.github/workflows/`: GitHub Actions workflows for testing and releases

## Commands

- **Development**: `mvn clean compile` (compile project)
- **Build**: `mvn clean verify` (build, package, and run all unit tests)
- **Test**: `mvn test` (run unit tests only)
- **Integration Tests**: `export GOOGLE_APPLICATION_CREDENTIALS=/path/to/service/account.json && mvn -Penable-integration-tests clean verify`
- **Lint**: `mvn com.spotify.fmt:fmt-maven-plugin:check` (check code formatting)
- **Format**: `mvn com.spotify.fmt:fmt-maven-plugin:format` (auto-format code)
- **Install**: `mvn install` (install to local Maven repository)
- **Javadoc**: `mvn javadoc:javadoc javadoc:test-javadoc` (generate documentation)
- **Samples**: `mvn -Penable-samples clean verify` (build and test samples)

## Code Style

- **Formatting**: Google Java Format (google-java-format) - automatic formatting enforced
- **License Header**: Apache 2.0 license header required on all Java files (defined in java.header)
- **Linting**: Maven fmt plugin for code formatting validation
- **Package Structure**: Follows Google Cloud client library conventions with versioned packages
- **Naming Conventions**: 
  - Classes: PascalCase (e.g., `JsonStreamWriter`, `BigQueryReadClient`)
  - Methods: camelCase
  - Constants: UPPER_SNAKE_CASE
- **Import Style**: Organized imports with Google's standard ordering
- **File Organization**: 
  - Source code in `src/main/java/com/google/cloud/bigquery/storage/`
  - Tests mirror source structure in `src/test/java/`
  - Resources in `src/main/resources/` and `src/test/resources/`

## Workflow

- **Development**: 
  - Requires Java 8+ and Maven 3.x
  - Integration tests require Google Cloud Platform credentials
  - Multi-module Maven build with parent POM dependency management
- **Testing**: 
  - Unit tests run without external dependencies
  - Integration tests require GCP service account and billing-enabled project
  - CI tests on multiple Java versions (8, 11, 17, 21) and platforms (Linux, macOS, Windows)
- **Code Review**: 
  - All changes require GitHub pull request review
  - Contributor License Agreement (CLA) required
  - Automated checks for formatting, tests, and code coverage
  - Must link to GitHub issue for bug reports/feature requests
- **Release Process**: 
  - Automated releases via release-please bot
  - Semantic versioning with Maven version management
  - Published to Maven Central
  - Releases automatically create GitHub releases and update changelogs
- **Quality Gates**:
  - Code formatting must pass (Google Java Format)
  - All tests must pass including integration tests
  - Code coverage requirements enforced
  - CLIRR compatibility checks for API changes
- **Contribution**: 
  - Follow Google's Open Source Community Guidelines
  - Sample code must follow Google Cloud samples format
  - Changes require associated GitHub issue for tracking