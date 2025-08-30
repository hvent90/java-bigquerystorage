# Google BigQuery Storage Client for Java

This repository contains the Java client library for Google Cloud BigQuery Storage, providing direct high-throughput access to BigQuery data with parallel processing capabilities and fine-grained control over data retrieval.

## Tech Stack

- **Language**: Java 8+ (supports Java 8, 11, 17, 21)
- **Framework**: Google API Extensions (GAX) for Java
- **Runtime**: JVM 8+ with compilation on Java 17
- **Build Tool**: Apache Maven 3.x
- **Testing**: JUnit 4.13.2
- **Package Manager**: Maven with BOM-based dependency management
- **Transport**: gRPC for communication with BigQuery Storage API
- **Protocol**: Protocol Buffers for data serialization
- **Dependencies**: Google Cloud shared dependencies, gRPC, protobuf
- **Observability**: OpenTelemetry metrics support

## Project Structure

- `google-cloud-bigquerystorage/`: Main client library with API implementations
- `proto-google-cloud-bigquerystorage-*/`: Protocol buffer definitions for different API versions (v1, v1alpha, v1beta, v1beta1, v1beta2)
- `grpc-google-cloud-bigquerystorage-*/`: Generated gRPC stub classes for API versions
- `google-cloud-bigquerystorage-bom/`: Bill of Materials for version management
- `samples/`: Code samples and integration tests
- `samples/snippets/`: Example usage code and integration tests
- `.kokoro/`: Google internal CI/CD build configuration
- `.github/workflows/`: GitHub Actions CI/CD workflows

## Commands

- **Development**: `mvn clean verify` (builds, tests, and packages)
- **Build**: `mvn install -DskipTests=true -Dclirr.skip=true -Denforcer.skip=true -Dmaven.javadoc.skip=true`
- **Test**: `mvn test -B -ntp -Dclirr.skip=true -Denforcer.skip=true`
- **Integration Tests**: `mvn -Penable-integration-tests clean verify`
- **Lint**: `mvn com.spotify.fmt:fmt-maven-plugin:check`
- **Format**: `mvn com.spotify.fmt:fmt-maven-plugin:format`
- **Javadoc**: `mvn javadoc:javadoc javadoc:test-javadoc`
- **API Compatibility**: `mvn clirr:check`
- **Samples**: `mvn -Penable-samples verify` (in samples directory)

## Code Style

- **Formatting**: Google Java Format via `com.spotify.fmt:fmt-maven-plugin`
- **Linting**: Checkstyle with Google style configuration
- **API Compatibility**: CLIRR Maven plugin for binary compatibility checking
- **License Headers**: Apache 2.0 license headers enforced on all Java files
- **Import Style**: Specific imports preferred over wildcard imports (except in test files)
- **Naming Conventions**: Standard Java camelCase for variables/methods, PascalCase for classes
- **File Organization**: Package structure follows Google Cloud client library conventions

## Workflow

- **Development**: 
  - Local development requires Java 8+ and Maven
  - Use `mvn clean verify` for full build and test cycle
  - Integration tests require GCP service account credentials via `GOOGLE_APPLICATION_CREDENTIALS`

- **Testing**: 
  - Unit tests run on Java 8, 11, 17, 21 via GitHub Actions
  - Integration tests available with `-Penable-integration-tests` profile
  - Sample integration tests in separate Maven modules
  - Windows compatibility testing included in CI

- **Code Review**: 
  - All changes require GitHub pull request review
  - Contributor License Agreement (CLA) required
  - Automated CI checks for formatting, linting, tests, and compatibility

- **Release Process**: 
  - Automated releases via release-please bot
  - Semantic versioning with automated changelog generation
  - Maven Central deployment for stable releases
  - Snapshot releases for development versions

- **Deployment**: 
  - Artifacts published to Maven Central
  - Multi-version support (v1, v1alpha, v1beta, v1beta1, v1beta2)
  - BOM artifacts for dependency management
  - GraalVM native image support configurations included

- **Contribution**: 
  - Fork and create pull requests from feature branches
  - Follow Google Java style guide and formatting
  - Include tests for new functionality
  - Update documentation and samples as needed