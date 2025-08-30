# CLAUDE.md - Google BigQuery Storage Client for Java

## Overview
This is the Google BigQuery Storage Client Library for Java, providing direct, high-throughput read and write access to Google BigQuery tables through gRPC APIs. The library supports streaming reads, batch writes, schema-aware data ingestion, and OpenTelemetry metrics collection.

# Tech Stack
- **Language**: Java 8+ (supports Java 8, 11, 17, 21)
- **Framework**: Google Cloud Client Libraries with gRPC transport
- **Runtime**: JVM (Java Virtual Machine)
- **Build Tool**: Apache Maven 3.x
- **Testing**: JUnit 4.13.2 with Truth assertions and Mockito
- **Package Manager**: Maven Central with Google Cloud BOM
- **Database**: Google BigQuery via BigQuery Storage API
- **Key Dependencies**:
  - gRPC (grpc-api, grpc-stub, grpc-protobuf)
  - Protocol Buffers (protobuf-java)
  - Google Auth Library (google-auth-library-credentials)
  - Guava, Gson for utilities
  - OpenTelemetry for observability
  - Apache Arrow and Avro for data formats

# Project Structure
- **`google-cloud-bigquerystorage/`**: Main client library module
  - `src/main/java/com/google/cloud/bigquery/storage/`: Core client implementation
    - `v1/`: Primary API version with read/write clients
    - `v1alpha/`, `v1beta/`, `v1beta1/`, `v1beta2/`: Beta API versions
    - `util/`: Shared utilities and error handling
- **`proto-google-cloud-bigquerystorage-*/`**: Protocol buffer definitions for different API versions
- **`grpc-google-cloud-bigquerystorage-*/`**: Generated gRPC client stubs
- **`samples/`**: Code examples and integration tests
  - `snippets/`: Complete working examples for different use cases
  - `install-without-bom/`, `snapshot/`: Different dependency configurations
- **`.kokoro/`**: Google's internal CI/CD build scripts
- **`.github/workflows/`**: GitHub Actions CI/CD workflows

# Commands
- **Development**: `mvn clean verify` - Build and run all unit tests
- **Build**: `mvn clean install -DskipTests=true` - Compile and package without tests
- **Test**: `mvn test` - Run unit test suite
- **Integration Tests**: `mvn -Penable-integration-tests clean verify` (requires GOOGLE_APPLICATION_CREDENTIALS)
- **Lint**: `mvn com.spotify.fmt:fmt-maven-plugin:check` - Check code formatting
- **Format**: `mvn com.spotify.fmt:fmt-maven-plugin:format` - Auto-format code
- **Install**: `mvn install` - Install dependencies and build project
- **Javadoc**: `mvn javadoc:javadoc javadoc:test-javadoc` - Generate documentation
- **Samples**: `mvn -Penable-samples clean verify` - Run sample applications
- **Native Image**: `mvn -PcustomNative test` - Test with GraalVM native image
- **Version Check**: `mvn clirr:check` - Check API compatibility

# Code Style
- **Formatting**: Google Java Format (google-java-format) - enforced via fmt-maven-plugin
- **Linting**: Built-in Maven compiler with strict compilation settings
- **Type Checking**: Static analysis via Protocol Buffer validation and GAX annotations
- **Import Style**: Standard Java import organization, grouped by package hierarchy
- **Naming Conventions**: 
  - Classes: PascalCase (e.g., `JsonStreamWriter`, `BigQueryReadClient`)
  - Methods: camelCase (e.g., `createReadSession`, `appendRows`)
  - Constants: UPPER_SNAKE_CASE (e.g., `CLIENT_ID`)
  - Packages: Lowercase with dots (e.g., `com.google.cloud.bigquery.storage.v1`)
- **File Organization**: 
  - Version-specific packages (v1, v1alpha, v1beta, etc.)
  - Separate modules for proto definitions and gRPC stubs
  - Utility classes in dedicated `util` package
- **License Headers**: Apache 2.0 license header required on all source files
- **API Documentation**: Comprehensive JavaDoc for all public APIs

# Workflow
- **Development**: 
  - Local setup requires Java 8+ and Maven 3.x
  - Clone repository and run `mvn clean verify` for full build
  - Integration tests require GCP credentials via `GOOGLE_APPLICATION_CREDENTIALS`
- **Testing**: 
  - Unit tests via JUnit with Truth assertions
  - Integration tests against live BigQuery service
  - Mock-based testing for gRPC services
  - Native image testing with GraalVM support
  - Cross-platform testing (Linux, macOS, Windows)
- **Code Review**: 
  - All changes require GitHub Pull Request approval
  - Automated checks: CI builds, formatting, linting, javadoc generation
  - Google CLA (Contributor License Agreement) required
  - Community guidelines follow Google Open Source standards
- **CI/CD Pipeline**:
  - GitHub Actions for continuous integration
  - Multiple Java versions tested (8, 11, 17, 21)
  - Kokoro (Google's internal CI) for additional testing
  - Automated dependency updates via Renovate
  - Auto-release for dependency-only updates
- **Release Process**: 
  - Semantic versioning (major.minor.patch)
  - Release-please automation for version management
  - Staged releases through Sonatype Nexus to Maven Central
  - Snapshot versions for development builds
  - BOM (Bill of Materials) for dependency coordination
- **Contribution**: 
  - Fork and create feature branch
  - Follow Google Java Format styling
  - Include unit tests and integration tests where applicable
  - Update documentation and samples as needed
  - Submit PR with descriptive title and body

## Key Features
- **High-throughput streaming reads** from BigQuery tables
- **Batch and streaming writes** to BigQuery tables  
- **Schema-aware data ingestion** with automatic schema updates
- **Multiple data formats**: Protocol Buffers, JSON, Apache Arrow, Avro
- **OpenTelemetry integration** for metrics and observability
- **Connection pooling** and automatic retry logic
- **Native image support** with GraalVM
- **Comprehensive error handling** and timeout management

## Security Considerations
- Service account authentication via Google Auth Library
- TLS encryption for all gRPC communications  
- IAM-based authorization for BigQuery resources
- Credential management through environment variables
- No hardcoded secrets in source code or configuration files

## Performance Optimizations
- Connection pooling for reduced latency
- Batch request processing for improved throughput
- Configurable flow control settings
- Automatic request retry with exponential backoff
- Memory-efficient streaming for large datasets
- Arrow format support for columnar data processing