# Google Cloud BigQuery Storage Client for Java

This project provides a Java client library for Google BigQuery Storage API, offering high-throughput read and write access to BigQuery tables.

## Tech Stack

- **Language**: Java 8+ (supports Java 8, 11, 17, 21)
- **Framework**: Google API Client Libraries for Java (GAPIC)
- **Runtime**: JVM (Java Virtual Machine)
- **Build Tool**: Maven 3.x
- **Testing**: JUnit 4.13.2
- **Package Manager**: Maven
- **Transport**: gRPC (Google Remote Procedure Call)
- **Serialization**: Protocol Buffers (protobuf 3.25.4)
- **Dependencies**: 
  - Google Cloud Shared Dependencies
  - Google Auth Library
  - OpenTelemetry (optional for metrics)

## Project Structure

- `google-cloud-bigquerystorage/`: Main client library module containing core functionality
- `grpc-google-cloud-bigquerystorage-v*/`: gRPC stub modules for different API versions (v1, v1alpha, v1beta, v1beta1, v1beta2)
- `proto-google-cloud-bigquerystorage-v*/`: Protocol buffer definitions and generated classes for API versions
- `samples/`: Code samples and example usage
  - `samples/snippets/src/main/java/`: Main sample code
  - `samples/snippets/src/test/java/`: Integration tests for samples
- `google-cloud-bigquerystorage-bom/`: Bill of Materials for dependency management
- `.github/`: GitHub workflows, issue templates, and repository configuration
- `.kokoro/`: Google internal CI/CD configuration scripts

## Commands

- **Development**: `mvn clean verify` (build, test, and package)
- **Build**: `mvn compile` or `mvn install -DskipTests=true`
- **Test**: `mvn test` (unit tests) or `mvn -Penable-integration-tests verify` (with integration tests)
- **Lint**: `mvn com.spotify.fmt:fmt-maven-plugin:check` (check formatting) or `mvn com.spotify.fmt:fmt-maven-plugin:format` (auto-format)
- **Install Dependencies**: `mvn install`
- **Integration Tests**: `export GOOGLE_APPLICATION_CREDENTIALS=/path/to/service-account.json && mvn -Penable-integration-tests clean verify`
- **Javadoc**: `mvn javadoc:javadoc javadoc:test-javadoc`
- **Code Quality**: `mvn clirr:check` (API compatibility check)

## Code Style

- **Formatting**: Google Java Format via `com.spotify.fmt:fmt-maven-plugin`
- **Linting**: Enforced via Maven build with Google Java style guide
- **Type Checking**: Static analysis through Maven compiler plugin and dependency analysis
- **Import Style**: Standard Java import ordering, static imports allowed
- **Naming Conventions**:
  - Classes: PascalCase (e.g., `BigQueryReadClient`)
  - Methods: camelCase (e.g., `createReadSession`)
  - Constants: UPPER_SNAKE_CASE
  - Packages: lowercase with dots (e.g., `com.google.cloud.bigquery.storage.v1`)
- **File Organization**: 
  - API versions separated into distinct packages (v1, v1alpha, v1beta, etc.)
  - Generated code kept separate from handwritten code
  - Test files mirror source structure with `Test` suffix

## Workflow

- **Development**: 
  - Local setup requires Java 8+ and Maven
  - Run `mvn clean verify` for full build and test cycle
  - Format code with `mvn com.spotify.fmt:fmt-maven-plugin:format`

- **Testing**: 
  - Unit tests: `mvn test`
  - Integration tests require GCP service account credentials
  - Separate test profiles for different environments
  - Test coverage reported via codecov

- **Code Review**:
  - All changes require GitHub pull requests
  - Automated CI/CD runs on multiple Java versions (8, 11, 17, 21)
  - Lint, test, and compatibility checks must pass
  - Manual review required before merge

- **Deployment**:
  - Automated releases via release-please bot
  - Multi-stage CI pipeline with Kokoro (Google's CI system)
  - Maven Central deployment for releases
  - Separate testing on Windows, macOS, and Linux
  - GraalVM native image support testing

- **Release Process**:
  - Semantic versioning (MAJOR.MINOR.PATCH)
  - Automated dependency updates via Renovate
  - Release notes generated automatically
  - SNAPSHOT versions for development builds

- **Contribution**:
  - Contributor License Agreement (CLA) required
  - Follow Google's Open Source Community Guidelines
  - Open issue before submitting code changes
  - Include appropriate tests and documentation
  - Maintain code coverage levels

## Architecture Notes

- **Multi-version Support**: Maintains backward compatibility with multiple API versions (v1, v1alpha, v1beta, etc.)
- **gRPC Transport**: Uses HTTP/2-based gRPC for efficient communication with BigQuery Storage API
- **Streaming Support**: Implements bidirectional streaming for high-throughput data operations
- **Connection Management**: Includes connection pooling and retry logic for reliability
- **Telemetry Integration**: Optional OpenTelemetry support for observability

## Security Considerations

- Service account authentication via `GOOGLE_APPLICATION_CREDENTIALS`
- OAuth 2.0 scopes for API authorization
- TLS encryption for all gRPC communications
- Secure credential handling practices enforced

## Performance Optimizations

- Protocol buffer serialization for efficient data transfer
- Connection pooling for reduced latency
- Configurable batch sizes for bulk operations
- Arrow format support for columnar data processing
- Parallel processing capabilities for large datasets