# CLAUDE.md - Google Cloud BigQuery Storage Java Client

This is a comprehensive guide for the Google Cloud BigQuery Storage Java client library repository.

## Tech Stack

- **Language**: Java 8+ (builds with Java 17, supports runtime Java 8-21)
- **Framework**: Google Cloud Client Libraries framework with gRPC
- **Runtime**: JVM (Java Virtual Machine)
- **Build Tool**: Maven 3.x
- **Testing**: JUnit 4.13.2, Mockito for unit tests, integration tests with Google Cloud
- **Package Manager**: Apache Maven
- **Transport**: gRPC for BigQuery Storage API communication
- **Protocols**: Protocol Buffers (protobuf) 3.25.4
- **Key Dependencies**:
  - `com.google.cloud:google-cloud-shared-dependencies` (shared Google Cloud dependencies)
  - `io.grpc:grpc-*` (gRPC libraries)
  - `com.google.protobuf:protobuf-java`
  - `com.google.gson:gson` (JSON handling)
  - `org.json:json` (JSON processing)

## Project Structure

- **`google-cloud-bigquerystorage/`**: Main client library source code
- **`proto-google-cloud-bigquerystorage-v*/`**: Protocol buffer definitions for different API versions (v1, v1alpha, v1beta, v1beta1, v1beta2)
- **`grpc-google-cloud-bigquerystorage-v*/`**: Generated gRPC client stubs for each API version
- **`samples/`**: Code samples and snippets demonstrating library usage
- **`google-cloud-bigquerystorage-bom/`**: Bill of Materials for dependency management
- **`.github/workflows/`**: CI/CD pipeline configurations
- **`.kokoro/`**: Google's internal build system configuration

### Key Source Directories

- **`src/main/java/com/google/cloud/bigquery/storage/`**: Primary source code
  - **`v1/`**: Production-ready v1 API client implementation
  - **`v1beta*/`**: Beta API versions
  - **`util/`**: Utility classes and helpers
- **`src/test/java/`**: Unit and integration test files
- **`src/main/resources/META-INF/`**: Native image configurations for GraalVM

## Commands

- **Development**: `mvn clean verify` (clean, compile, test, package)
- **Build**: `mvn clean install -DskipTests=true` (fast build without tests)
- **Test**: `mvn test` (unit tests), `mvn -Penable-integration-tests verify` (with integration tests)
- **Lint**: `mvn com.spotify.fmt:fmt-maven-plugin:check` (code formatting check)
- **Format**: `mvn com.spotify.fmt:fmt-maven-plugin:format` (auto-format code)
- **Install**: `mvn install` (install dependencies and build artifacts)
- **Integration Tests**: `export GOOGLE_APPLICATION_CREDENTIALS=/path/to/service-account.json && mvn -Penable-integration-tests clean verify`
- **Javadoc**: `mvn javadoc:javadoc javadoc:test-javadoc`
- **Clirr Check**: `mvn clirr:check` (API compatibility check)
- **Samples**: `mvn -Penable-samples verify` (in samples/ directory)

## Code Style

- **Formatting**: Google Java Format via `com.spotify.fmt:fmt-maven-plugin`
- **Linting**: Checkstyle with Google Java style guide (samples use `mvn checkstyle:check`)
- **Type Checking**: Standard Java compiler with strict compilation settings
- **Import Style**: 
  - Standard Java imports first
  - Google Cloud and API imports grouped
  - Third-party imports
  - Static imports last
- **Naming Conventions**:
  - Classes: PascalCase (e.g., `JsonStreamWriter`, `BigQueryReadClient`)
  - Methods: camelCase (e.g., `createReadSession`, `appendRows`)
  - Constants: UPPER_SNAKE_CASE (e.g., `CLIENT_ID`)
  - Packages: lowercase with dots (e.g., `com.google.cloud.bigquery.storage.v1`)
- **File Organization**:
  - License header on all source files (Apache 2.0)
  - Package declaration
  - Imports (grouped and sorted)
  - Class/interface declaration with Javadoc

## Workflow

### Development

1. **Local Setup**: 
   - Java 8+ installed
   - Maven 3.x installed
   - Optional: Google Cloud credentials for integration tests
   - Run `mvn clean verify` to validate setup

2. **Environment Requirements**:
   - Primary development on Java 17
   - Testing across Java 8, 11, 17, and 21
   - Windows, Linux, and macOS support

### Testing

- **Unit Tests**: `mvn test` (no external dependencies)
- **Integration Tests**: Require Google Cloud project and service account
- **Sample Tests**: Separate test suite in `samples/` directory
- **Coverage**: Codecov integration for coverage reporting
- **Continuous Testing**: GitHub Actions runs tests on multiple Java versions

### Code Review

- **Process**: All changes require pull request review
- **Approval**: Maintainer approval required
- **Automation**: 
  - Automated formatting and lint checks
  - Automated dependency updates via Renovate
  - API compatibility checks via Clirr

### Deployment

- **Release Process**: Automated via release-please GitHub Action
- **Versioning**: Semantic versioning (x.y.z format)
- **Artifacts**: Published to Maven Central
- **Environments**: 
  - Development: Snapshot builds
  - Production: Release builds to Maven Central

### Contribution

1. **Setup**: Fork repository, create feature branch
2. **Development**: Follow Google Java style guide, write tests
3. **Formatting**: Run `mvn com.spotify.fmt:fmt-maven-plugin:format`
4. **Testing**: Ensure `mvn clean verify` passes
5. **Pull Request**: Submit PR with clear description
6. **Review**: Await maintainer review and approval

### Release Process

- **Versioning**: Automated semantic versioning
- **Release Automation**: GitHub Actions handles release process
- **Distribution**: Artifacts published to Maven Central
- **Documentation**: Javadocs published to cloud.google.com
- **Dependency Management**: BOM (Bill of Materials) for version coordination

### Architecture Notes

- **Multi-module Maven project**: Separate modules for different API versions and concerns
- **gRPC-based**: Uses gRPC for efficient communication with BigQuery Storage API
- **Schema Evolution**: Supports automatic schema updates for BigQuery table changes
- **Stream Writing**: Optimized for high-throughput data ingestion
- **Native Image**: GraalVM native image support with reflection configurations
- **Telemetry**: OpenTelemetry integration for metrics and observability

### Security Considerations

- **Authentication**: Uses Google Cloud authentication (service accounts, ADC)
- **Credentials**: Never commit credentials, use environment variables
- **Dependencies**: Regular automated dependency updates via Renovate
- **Vulnerability Scanning**: Automated security scanning in CI/CD pipeline
- **License Compliance**: Apache 2.0 license, CLA required for contributions