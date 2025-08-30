# BigQuery Storage Client for Java

This is the Java client library for Google Cloud BigQuery Storage API. It provides direct, high-throughput read and write access to BigQuery tables with support for multiple data formats including Avro, Arrow, and Protocol Buffers.

## Tech Stack

- **Language**: Java (requires Java 8+, supports Java 11, 17, 21)
- **Framework**: Google Cloud Client Libraries for Java, gRPC-based API
- **Runtime**: JVM (Java 8+)
- **Build Tool**: Apache Maven with multi-module structure
- **Testing**: JUnit 4.13.2, Mockito 3.12.4, Google Truth 1.4.4
- **Package Manager**: Maven with Google Cloud shared dependencies BOM
- **Database**: Google BigQuery (cloud-native data warehouse)
- **Transport**: gRPC for high-performance communication
- **Observability**: OpenTelemetry support for metrics and tracing
- **Serialization**: Protocol Buffers, Apache Avro 1.11.4, Apache Arrow

## Project Structure

- `google-cloud-bigquerystorage/`: Main client library module containing core functionality
- `proto-google-cloud-bigquerystorage-v*/`: Protocol buffer definitions for different API versions
- `grpc-google-cloud-bigquerystorage-v*/`: Generated gRPC client code for different API versions
- `google-cloud-bigquerystorage-bom/`: Bill of Materials for dependency management
- `samples/`: Code samples and integration examples
  - `samples/snippets/`: Complete examples demonstrating library usage
  - `samples/install-without-bom/`: Standalone installation example
  - `samples/snapshot/`: Development snapshot samples
- `.github/`: GitHub workflows, issue templates, and repository configuration
- `.kokoro/`: Google's internal CI/CD build scripts and configurations

## Commands

- **Development**: `mvn install -DskipTests=true -Dclirr.skip=true -Denforcer.skip=true -Dmaven.javadoc.skip=true`
- **Build**: `mvn clean verify` (includes unit tests and verification)
- **Test**: `mvn test -B -ntp -Dclirr.skip=true -Denforcer.skip=true`
- **Lint**: `mvn com.spotify.fmt:fmt-maven-plugin:check`
- **Format**: `mvn com.spotify.fmt:fmt-maven-plugin:format`
- **Install**: `mvn install -B -V -ntp` (with dependencies)
- **Integration Tests**: `mvn -Penable-integration-tests clean verify` (requires GOOGLE_APPLICATION_CREDENTIALS)
- **Javadoc**: `mvn javadoc:javadoc javadoc:test-javadoc`
- **Compatibility Check**: `mvn -Denforcer.skip=true clirr:check`
- **Samples**: `mvn -Penable-samples verify` (in samples directory)
- **GraalVM Native**: `mvn -PcustomNative test` (native image testing)

## Code Style

- **Formatting**: Google Java Format via `com.spotify.fmt:fmt-maven-plugin`
- **Linting**: Google Java Format enforces consistent formatting across the codebase
- **License Headers**: Apache 2.0 license headers required on all Java files (enforced by Checkstyle)
- **Import Style**: Standard Java import organization following Google's conventions
- **Naming Conventions**: 
  - Classes: PascalCase (e.g., `BigQueryReadClient`)
  - Methods: camelCase (e.g., `createReadSession`)
  - Constants: UPPER_SNAKE_CASE (e.g., `DEFAULT_TIMEOUT`)
  - Packages: lowercase with dots (e.g., `com.google.cloud.bigquery.storage.v1`)
- **File Organization**: Multi-module Maven structure with versioned API packages
- **Type Checking**: Standard Java compiler type checking with Maven compiler plugin
- **AutoValue**: Used for immutable value classes (enabled via `EnableAutoValue.txt`)

## Workflow

- **Development**: 
  - Local setup requires Java 8+ and Maven
  - Run `mvn install` to build and install dependencies locally
  - Use `mvn com.spotify.fmt:fmt-maven-plugin:format` before committing
  - Integration tests require Google Cloud credentials via `GOOGLE_APPLICATION_CREDENTIALS`

- **Testing**: 
  - Unit tests: `mvn test` (no external dependencies required)
  - Integration tests: Require GCP service account and active project
  - Native image tests available with GraalVM profile
  - Cross-platform testing on Linux, macOS, and Windows via GitHub Actions
  - Multi-version Java testing (8, 11, 17, 21)

- **Code Review**: 
  - All changes require GitHub pull request review
  - Automated checks include: unit tests, integration tests, linting, Javadoc generation
  - Compatibility checking via CLIRR to prevent breaking changes
  - Code coverage tracking with Codecov
  - Google's internal build system (Kokoro) provides additional validation

- **Deployment**: 
  - Automated release process using release-please for semantic versioning
  - Artifacts deployed to Maven Central Repository
  - Snapshots published for development versions
  - Multi-module releases with synchronized versioning across all modules

- **Release Process**: 
  - Semantic versioning following `major.minor.patch` format
  - Release automation via `release-please[bot]`
  - Automated dependency updates via Renovate
  - Support for multiple API versions (v1, v1alpha, v1beta, v1beta1, v1beta2)

- **Contribution**: 
  - Requires signed Google Contributor License Agreement (CLA)
  - Follow Google's Open Source Community Guidelines
  - Sample code must follow Google Cloud samples formatting guidelines
  - PRs must include appropriate tests and documentation updates

## Security Considerations

- Apache 2.0 licensed open source project
- Requires Google Cloud authentication via service accounts
- Supports multiple authentication methods through google-auth-library
- License header validation enforced via Checkstyle configuration
- Dependency vulnerability scanning via Renovate and GitHub Dependabot

## Architecture Patterns

- **Multi-module Maven Structure**: Separates concerns across API versions and functionality
- **gRPC Streaming**: High-performance bidirectional streaming for large data transfers
- **Connection Pooling**: Efficient connection management via `ConnectionWorkerPool`
- **Retry Logic**: Built-in exponential backoff and retry mechanisms
- **Schema Evolution**: Support for multiple data formats and schema versions
- **Native Image Support**: GraalVM compatibility for reduced startup times and memory usage