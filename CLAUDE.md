# Google Cloud BigQuery Storage Java Client

This repository contains the Java client library for Google Cloud BigQuery Storage API - a high-throughput API for reading and writing data stored in BigQuery.

## Tech Stack

- **Language**: Java (versions 8, 11, 17, 21 supported)
- **Framework**: Google API Extensions for Java (GAX), gRPC
- **Runtime**: JVM (Java Virtual Machine)
- **Build Tool**: Apache Maven 3.x
- **Testing**: JUnit 4, Mockito for unit tests, integration tests with actual BigQuery
- **Package Manager**: Maven (pom.xml)
- **Protocol**: Protocol Buffers (protobuf) for API definitions
- **Transport**: gRPC for communication with BigQuery Storage API
- **Observability**: OpenTelemetry metrics support
- **Code Generation**: Google API Generator (GAPIC) for client library generation

## Project Structure

- **`google-cloud-bigquerystorage/`**: Main client library with high-level API classes
  - `src/main/java/com/google/cloud/bigquery/storage/v1/`: Core client classes (BigQueryReadClient, BigQueryWriteClient, StreamWriter, etc.)
  - `src/test/java/`: Unit and integration tests
- **`proto-google-cloud-bigquerystorage-v1*/`**: Protocol buffer definitions and generated Java classes for different API versions (v1, v1alpha, v1beta, v1beta1, v1beta2)
- **`grpc-google-cloud-bigquerystorage-v1*/`**: gRPC stub classes for different API versions
- **`samples/`**: Code samples and example applications
  - `snippets/src/main/java/com/example/bigquerystorage/`: Sample applications demonstrating API usage
  - `install-without-bom/`, `snapshot/`: Different dependency management examples
- **`google-cloud-bigquerystorage-bom/`**: Bill of Materials (BOM) for dependency management
- **`.github/`**: GitHub Actions workflows and repository configuration
- **`.kokoro/`**: Google's internal CI/CD scripts

## Commands

- **Development**: `mvn compile` (compile source code)
- **Build**: `mvn clean verify` (build, package, and run all unit tests)
- **Test**: `mvn test` (run unit tests only)
- **Integration Tests**: `mvn -Penable-integration-tests clean verify` (requires GCP credentials)
- **Lint**: `mvn com.spotify.fmt:fmt-maven-plugin:check` (check code formatting)
- **Format**: `mvn com.spotify.fmt:fmt-maven-plugin:format` (auto-format code)
- **Install**: `mvn install -DskipTests=true` (install to local Maven repository)
- **Samples**: `mvn -P lint --quiet --batch-mode checkstyle:check` (in samples/snippets directory)
- **Javadoc**: `mvn javadoc:javadoc javadoc:test-javadoc` (generate documentation)

## Code Style

- **Formatting**: Google Java Format (google-java-format) with automated formatting via `fmt-maven-plugin`
- **Linting**: Checkstyle for code quality checks in samples
- **Type Checking**: Java static typing with Protocol Buffers for API contracts
- **Import Style**: Standard Java import conventions, organized with standard Java ordering
- **Naming Conventions**: 
  - Classes: PascalCase (e.g., `BigQueryReadClient`, `StreamWriter`)
  - Methods: camelCase (e.g., `createReadSession`, `appendRows`)
  - Constants: UPPER_SNAKE_CASE
  - Packages: lowercase with dots (e.g., `com.google.cloud.bigquery.storage.v1`)
- **File Organization**: 
  - Separate modules for different API versions and components
  - Test classes mirror source package structure with `Test` suffix
  - Proto definitions in separate modules from generated Java code

## Workflow

- **Development**: 
  - Java 8+ required (CI tests on Java 8, 11, 17, 21)
  - Maven 3.x for dependency management and builds
  - Protocol Buffer compiler for proto file generation
  - Google Application Credentials required for integration tests
- **Testing**: 
  - Unit tests run via `mvn test`
  - Integration tests require GCP project and service account
  - Separate test profiles for different test types
  - Coverage reporting via Codecov
- **Code Review**: 
  - All changes require pull request review
  - Automated CI checks include builds on multiple Java versions, linting, and tests
  - Contributor License Agreement (CLA) required
  - CODEOWNERS file defines review assignments
- **Deployment**: 
  - Automated releases via release-please GitHub Action
  - Publishes to Maven Central repository
  - Supports multiple release branches for different versions
  - Snapshot builds for development versions
- **Release Process**: 
  - Semantic versioning with conventional commits
  - Automated changelog generation
  - Branch-based releases with backport support
  - Maven coordinates: `com.google.cloud:google-cloud-bigquerystorage`
- **Contribution**: 
  - Fork and pull request workflow
  - Code must pass all CI checks (build, test, lint)
  - Follow Google Java Style Guide
  - Include tests for new functionality
  - Update documentation as needed

## Key Features

- **Multi-version API Support**: Supports v1 (stable), v1alpha, v1beta, v1beta1, and v1beta2 API versions
- **High Performance**: Optimized for high-throughput reading and writing of BigQuery data
- **Streaming Support**: Real-time data streaming with connection pooling and automatic retry
- **Arrow and Avro Support**: Multiple data format options (Protocol Buffers, Arrow, Avro)
- **Native Image Support**: GraalVM native image compatibility
- **OpenTelemetry Integration**: Built-in observability and metrics collection
- **Connection Management**: Automatic connection pooling and lifecycle management
- **Authentication**: Google Cloud authentication with service accounts and user credentials

## Architecture

This is a multi-module Maven project that provides:
- Generated client libraries from Protocol Buffer definitions
- Hand-written convenience layers for common operations
- Separate modules for different API versions to support migration
- Bill of Materials (BOM) for simplified dependency management
- Comprehensive sample applications demonstrating usage patterns

The library follows Google Cloud Java client library conventions and integrates with the broader Google Cloud ecosystem.