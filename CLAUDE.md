# BigQuery Storage Java Client

This repository contains the Google Cloud BigQuery Storage client library for Java. The library provides idiomatic Java client for BigQuery Storage API, enabling high-throughput read and write access to BigQuery tables with support for multiple data formats including Arrow, Avro, and Protocol Buffers.

## Tech Stack

- **Language**: Java 8+ (supports Java 8, 11, 17, and newer versions)
- **Framework**: Google Cloud Java Client Libraries (GAPIC), Google API Extensions (GAX)
- **Runtime**: JVM 
- **Build Tool**: Apache Maven 3.x
- **Testing**: JUnit 4.x, Google Truth, Mockito
- **Package Manager**: Maven Central
- **Transport**: gRPC
- **Data Formats**: Protocol Buffers, Apache Arrow, Apache Avro
- **Observability**: OpenTelemetry integration
- **Code Generation**: Protocol Buffer Compiler (protoc), GAPIC Generator

## Project Structure

- `google-cloud-bigquerystorage/`: Main client library with high-level APIs
- `grpc-google-cloud-bigquerystorage-*/`: Generated gRPC stub libraries for different API versions
- `proto-google-cloud-bigquerystorage-*/`: Generated Protocol Buffer classes for different API versions
- `google-cloud-bigquerystorage-bom/`: Bill of Materials for dependency management
- `samples/`: Code samples and examples
- `.kokoro/`: Kokoro CI/CD configuration files
- `src/main/java/`: Main source code organized by API version (v1, v1alpha, v1beta, etc.)
- `src/test/java/`: Unit and integration tests
- `src/test/proto/`: Test Protocol Buffer definitions

## Commands

- **Install Dependencies**: `mvn clean install`
- **Build**: `mvn clean compile` 
- **Test**: `mvn clean test` (unit tests only)
- **Integration Tests**: `mvn -Penable-integration-tests clean verify` (requires GOOGLE_APPLICATION_CREDENTIALS)
- **Build + Test**: `mvn clean verify`
- **Format Code**: `mvn com.spotify.fmt:fmt-maven-plugin:format`
- **Build with Samples**: `mvn -Pinclude-samples clean verify`
- **Native Image Test**: `mvn -PcustomNative test` (GraalVM native image testing)

## Code Style

- **Formatting**: google-java-format (automatic formatting via Maven plugin)
- **Linting**: Checkstyle with custom rules for license header validation
- **Type Checking**: Static analysis via Maven compiler plugin with enhanced error reporting
- **Import Style**: Google Java Style Guide conventions (static imports grouped separately)
- **Naming Conventions**: 
  - Classes: PascalCase
  - Methods/variables: camelCase  
  - Constants: UPPER_SNAKE_CASE
  - Packages: lowercase with dots
- **File Organization**: Organized by API version and functionality, with clear separation between client code, generated code, and tests

## Workflow

- **Development**: 
  - Local development with Maven
  - Java 8+ required for building and running
  - Protocol Buffer compilation integrated into build process
  - Auto-generation of gRPC and proto classes from .proto files

- **Testing**: 
  - Unit tests with JUnit 4 and Google Truth assertions
  - Mock services for gRPC testing using MockGrpcService
  - Integration tests require GCP service account credentials
  - Separate test configurations for different Java versions (8, 11, 17)
  - GraalVM native image testing support

- **Code Review**: 
  - All submissions require review via GitHub pull requests
  - Contributor License Agreement (CLA) required
  - Automated formatting and style checks
  - License header validation on all Java files

- **CI/CD**: 
  - Google Kokoro CI system with multi-platform testing
  - Continuous integration on Java 8, 11 across Linux, macOS, Windows
  - Presubmit checks include: compilation, unit tests, integration tests, dependency analysis, license checks
  - Nightly builds with extended test suites
  - GraalVM native image compatibility testing

- **Release Process**: 
  - Semantic versioning (major.minor.patch)
  - Automated release pipeline via Kokoro
  - Maven Central deployment
  - Bill of Materials (BOM) management for version coordination

- **Dependency Management**: 
  - Renovate bot for automated dependency updates
  - Google Cloud Shared Dependencies BOM for version alignment
  - Semantic commit messages for dependency updates
  - Separate profiles for different Google Cloud service versions

- **Contribution**: 
  - Fork and pull request workflow
  - Code samples must follow Google's Java sample formatting guide
  - Integration tests require GCP project with BigQuery Storage API enabled
  - All code must include Apache 2.0 license headers