# CLAUDE.md

Generated for `hvent90/java-bigquerystorage.git`

This project is the Google BigQuery Storage Client for Java, providing idiomatic Java access to the BigQuery Storage API for high-throughput read/write operations.

## Tech Stack

- **Language**: Java 8+ (supports Java 8, 11, 17, 21)
- **Framework**: Google Cloud Client Libraries, gRPC
- **Runtime**: JVM
- **Build Tool**: Apache Maven
- **Testing**: JUnit 4, Mockito, Google Truth (testing framework)
- **Package Manager**: Maven
- **Protocol**: gRPC, Protocol Buffers (protobuf)
- **Transport**: Google API Extensions (GAX), HTTP/2 via gRPC
- **Dependencies**: Google Cloud Shared Dependencies, Guava, Apache Commons

## Project Structure

- `google-cloud-bigquerystorage/`: Main client library source code
  - `src/main/java/com/google/cloud/bigquery/storage/`: Core client implementation
    - `v1/`: Current stable API version (BigQuery Read/Write clients)
    - `v1beta*/`: Beta API versions for different features
    - `util/`: Utility classes for error handling and time conversion
- `proto-google-cloud-bigquerystorage-v*/`: Generated Protocol Buffer classes
- `grpc-google-cloud-bigquerystorage-v*/`: Generated gRPC stub classes  
- `samples/`: Sample code and usage examples
  - `snippets/`: Runnable code examples
  - `install-without-bom/`: Installation example without BOM
- `google-cloud-bigquerystorage-bom/`: Bill of Materials for dependency management
- `.kokoro/`: Continuous integration scripts and configuration
- `.github/`: GitHub Actions workflows and repository configuration

## Commands

- **Install**: `mvn install -B -V -ntp -DskipTests=true -Dclirr.skip=true -Denforcer.skip=true -Dmaven.javadoc.skip=true`
- **Build**: `mvn clean verify`
- **Test**: `mvn test -B -ntp -Dclirr.skip=true -Denforcer.skip=true`
- **Lint**: `mvn com.spotify.fmt:fmt-maven-plugin:check`
- **Integration Tests**: `mvn -B -Penable-integration-tests verify` (requires GOOGLE_APPLICATION_CREDENTIALS)
- **Javadoc**: `mvn javadoc:javadoc javadoc:test-javadoc`
- **Format**: `mvn com.spotify.fmt:fmt-maven-plugin:format`
- **Compatibility Check**: `mvn clirr:check`

## Code Style

- **Formatting**: Google Java Format via `com.spotify.fmt:fmt-maven-plugin`
- **Linting**: Built-in Maven enforcer and custom quality checks
- **License Headers**: Apache License 2.0 headers required on all Java files (defined in `java.header`)
- **Import Style**: Standard Java import conventions, grouped by package hierarchy
- **Naming Conventions**: 
  - Classes: PascalCase (e.g., `BigQueryReadClient`)
  - Methods: camelCase (e.g., `createReadSession`)
  - Constants: UPPER_SNAKE_CASE
  - Packages: lowercase with dots (e.g., `com.google.cloud.bigquery.storage`)
- **File Organization**: Organized by API version and feature area under `com/google/cloud/bigquery/storage/`

## Workflow

- **Development**: 
  - Java 8+ required for development
  - Maven 3.6+ recommended
  - Use `mvn install` to build without running tests
  - Integration tests require Google Cloud service account credentials
- **Testing**: 
  - Unit tests: `mvn test`
  - Integration tests: `mvn verify -Penable-integration-tests` 
  - Requires `GOOGLE_APPLICATION_CREDENTIALS` environment variable for integration tests
- **Code Review**: 
  - All changes require pull request review
  - PR template includes checklist for tests, linting, and documentation
  - Must link to GitHub issue for bugs/features
- **CI/CD**: 
  - GitHub Actions for continuous integration
  - Tests on Java 8, 11, 17, 21 on Ubuntu and Windows
  - Automated dependency updates via Renovate
  - Release automation via release-please bot
- **Release Process**: 
  - Semantic versioning (x.y.z format)
  - Automated releases via release-please GitHub Action
  - SNAPSHOT versions for development
  - Published to Maven Central
- **Contribution**: 
  - Contributor License Agreement required
  - Follow Google Open Source Community Guidelines
  - Create issue before submitting code changes
  - Ensure tests pass and code coverage doesn't decrease