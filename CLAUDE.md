# Google Cloud BigQuery Storage Java Client

This repository contains the Java idiomatic client library for [Google Cloud BigQuery Storage](https://cloud.google.com/bigquery/docs/reference/storage/). BigQuery Storage provides direct, high-throughput read and write access to existing BigQuery tables with automatic liquid sharding and fine-grained control over data access patterns.

## Tech Stack

- **Language**: Java 8+ (supports Java 8, 11, 17, 21)
- **Framework**: Google API Client Library (GAX), gRPC
- **Runtime**: JVM (Java Virtual Machine)
- **Build Tool**: Maven 3.6+
- **Testing**: JUnit 4, Google Truth, Mockito
- **Package Manager**: Maven Central
- **Database**: Google BigQuery (via BigQuery Storage API)
- **Additional Libraries**: 
  - Protocol Buffers 3.25.4
  - Apache Arrow (for columnar data)
  - Apache Avro (for serialization)
  - OpenTelemetry (for observability)
  - Google Cloud Core libraries
  - Gson (for JSON processing)

## Project Structure

- **`google-cloud-bigquerystorage/`**: Main client library implementation
  - `src/main/java/`: Core BigQuery Storage client code
  - `src/test/java/`: Unit tests
  - `src/main/resources/`: Native image configurations
- **`proto-google-cloud-bigquerystorage-v*/`**: Generated Protocol Buffer classes for different API versions
  - `v1/`: Stable version protocol definitions
  - `v1beta/`, `v1beta1/`, `v1beta2/`: Beta version protocol definitions  
  - `v1alpha/`: Alpha version protocol definitions
- **`grpc-google-cloud-bigquerystorage-v*/`**: Generated gRPC client stubs
- **`samples/`**: Code examples and integration tests
  - `snippets/`: Sample applications demonstrating API usage
  - `snapshot/`: Snapshot version samples
  - `install-without-bom/`: Example without BOM dependency management
- **`.github/workflows/`**: CI/CD pipeline configurations
- **`.kokoro/`**: Google internal build system configurations
- **`google-cloud-bigquerystorage-bom/`**: Bill of Materials for dependency management

## Commands

- **Install Dependencies**: `mvn install -B -V -ntp -DskipTests=true -Dclirr.skip=true -Denforcer.skip=true -Dmaven.javadoc.skip=true -Dgcloud.download.skip=true -T 1C`
- **Build**: `mvn clean verify`
- **Test**: `mvn test -B -ntp -Dclirr.skip=true -Denforcer.skip=true`
- **Integration Tests**: `mvn -B -Penable-integration-tests -DtrimStackTrace=false -Dclirr.skip=true -Denforcer.skip=true -Dit.test=!ITBigQueryWrite*RetryTest -Dsurefire.failIfNoSpecifiedTests=false -Dfailsafe.failIfNoSpecifiedTests=false -fae verify`
- **Lint**: `mvn com.spotify.fmt:fmt-maven-plugin:check`
- **Format Code**: `mvn com.spotify.fmt:fmt-maven-plugin:format`
- **Generate Javadoc**: `mvn javadoc:javadoc javadoc:test-javadoc`
- **Native Image Testing**: `mvn -B -PcustomNative test`
- **Dependency Check**: `mvn dependency:analyze`
- **Run Samples**: Navigate to `samples/snippets/` and run `mvn exec:java -Dexec.mainClass="com.example.bigquerystorage.CLASSNAME"`

## Code Style

- **Formatting**: Google Java Format (via `com.spotify.fmt:fmt-maven-plugin`)
- **Linting**: Automated via Maven plugins and CI pipeline
- **Type Checking**: Standard Java compilation with strict compiler warnings
- **Import Style**: Google Java Style Guide conventions
  - Wildcard imports avoided
  - Imports organized alphabetically
  - Static imports separated and grouped
- **Naming Conventions**: 
  - Classes: PascalCase (e.g., `JsonStreamWriter`, `BigQueryReadClient`)
  - Methods: camelCase (e.g., `append()`, `createReadSession()`)
  - Constants: SCREAMING_SNAKE_CASE (e.g., `CLIENT_ID`)
  - Packages: lowercase with dots (e.g., `com.google.cloud.bigquery.storage.v1`)
- **File Organization**: 
  - One public class per file
  - Package-private classes in same file as main class when appropriate
  - Test classes named with `Test` suffix for unit tests, `IT` suffix for integration tests

## Workflow

- **Development**: 
  - Clone repository and ensure Java 8+ and Maven 3.6+ are installed
  - Set `GOOGLE_APPLICATION_CREDENTIALS` environment variable for authentication
  - Run `mvn install` to build all modules
  - Use Maven profiles for specific JDK versions (`java17`, `arrow-config`, `customNative`)

- **Testing**: 
  - Unit tests: `mvn test` (JUnit 4 framework)
  - Integration tests: Require Google Cloud Project access with valid service account
  - Multiple Java version testing (8, 11, 17, 21) via CI matrix
  - Native image testing with GraalVM support
  - Code coverage tracking via Maven Surefire

- **Code Review**: 
  - All contributions require GitHub Pull Request review
  - Automated checks: CI build, linting, tests, dependency analysis
  - Manual review by Google Cloud team members (`@googleapis/api-bigquery`)
  - CLA (Contributor License Agreement) required for external contributions

- **Deployment**: 
  - Multi-module Maven project with parent POM
  - Automated releases via `release-please[bot]`
  - Maven Central deployment for public distribution
  - Semantic versioning (e.g., 3.16.x)
  - Separate versioning for stable (v1) and beta (v1beta, v1alpha) APIs

- **Release Process**: 
  - Version management through `versions.txt` file
  - Automated release PRs created by release-please
  - Auto-approval workflow for release PRs
  - Hermetic library generation for consistency
  - Multiple API version support (v1, v1beta1, v1beta2, v1alpha, v1beta)

- **Contribution**: 
  - Follow Google Open Source Community Guidelines
  - Run `mvn com.spotify.fmt:fmt-maven-plugin:format` before committing
  - Include appropriate tests for new functionality
  - Update documentation and samples as needed
  - Ensure compatibility across supported Java versions

## Architecture & Design Patterns

- **Multi-module Maven Architecture**: Separate modules for different API versions and protocol definitions
- **Generated Code Pattern**: Protocol Buffer and gRPC code generation from service definitions
- **Builder Pattern**: Extensive use in client configuration (e.g., `JsonStreamWriter.Builder`)
- **Async Programming**: ApiFuture-based asynchronous operations
- **Stream Processing**: Support for both read and write streaming operations
- **Schema Evolution**: Built-in schema update support for BigQuery table changes
- **Connection Pooling**: Managed gRPC connections with automatic retry and circuit breaker patterns

## Security & Best Practices

- **Authentication**: Google Cloud authentication via service accounts or default credentials
- **Encryption**: All data transmission encrypted via gRPC over TLS
- **Dependency Management**: Regular dependency updates via Renovate bot
- **Vulnerability Scanning**: Automated security checks in CI pipeline
- **Native Image Support**: GraalVM native image compatibility with reflection configurations
- **Resource Management**: Proper resource cleanup with AutoCloseable implementations

## Observability

- **OpenTelemetry Integration**: Built-in metrics and tracing support
- **Metrics Available**: 
  - `active_connection_count`: Active gRPC connections
  - `append_requests_acked`: Successful append operations
  - `network_response_latency`: Request/response timing
  - `inflight_queue_length`: Pending operation queue depth
- **Logging**: Standard Java logging with configurable levels
- **Error Handling**: Comprehensive exception hierarchy with specific error types