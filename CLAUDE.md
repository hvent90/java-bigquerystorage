# CLAUDE.md - BigQuery Storage Java Client

This repository contains the Google Cloud BigQuery Storage Client Library for Java, providing idiomatic Java access to the BigQuery Storage API for high-throughput read and write operations.

## Tech Stack

- **Language**: Java 8+ (supports Java 8, 11, 17, 21)
- **Framework**: Google Cloud Client Libraries for Java / gRPC
- **Runtime**: Java Virtual Machine (JVM)
- **Build Tool**: Apache Maven 3.x
- **Testing**: JUnit 4.13.2, Mockito
- **Package Manager**: Maven Central
- **Transport**: gRPC over HTTP/2
- **Protocol**: Protocol Buffers (protobuf)
- **Code Generation**: Google API Generator (GAPIC) 2.61.0
- **Dependencies**: 
  - `com.google.cloud:google-cloud-shared-dependencies` (BOM)
  - `com.google.cloud:libraries-bom` for version management
  - gRPC libraries for transport
  - Protocol Buffer libraries for serialization

## Project Structure

- **`google-cloud-bigquerystorage/`**: Main client library source code
  - `src/main/java/`: Core implementation classes
    - `com.google.cloud.bigquery.storage.v1/`: Primary v1 API client
    - `com.google.cloud.bigquery.storage.v1beta*/`: Beta API versions
    - `com.google.cloud.bigquery.storage.util/`: Utility classes
  - `src/test/java/`: Unit and integration tests
  - `src/main/resources/META-INF/native-image/`: GraalVM native image configurations
- **`proto-google-cloud-bigquerystorage-v*/`**: Protocol buffer definitions and generated Java classes
- **`grpc-google-cloud-bigquerystorage-v*/`**: Generated gRPC stub classes
- **`samples/`**: Code samples and usage examples
  - `snippets/`: Example applications demonstrating API usage
  - `install-without-bom/`: Sample showing dependency management without BOM
- **`.github/`**: GitHub workflows, templates, and automation
- **`.kokoro/`**: Google's internal CI/CD build scripts

## Commands

- **Development**: `mvn clean verify` (build and test)
- **Build**: `mvn clean install -DskipTests=true -Dclirr.skip=true -Denforcer.skip=true -Dmaven.javadoc.skip=true`
- **Test**: `mvn test -B -ntp -Dclirr.skip=true -Denforcer.skip=true`
- **Integration Tests**: `mvn verify -Penable-integration-tests` (requires `GOOGLE_APPLICATION_CREDENTIALS`)
- **Lint**: `mvn com.spotify.fmt:fmt-maven-plugin:check`
- **Format**: `mvn com.spotify.fmt:fmt-maven-plugin:format`
- **Javadoc**: `mvn javadoc:javadoc javadoc:test-javadoc`
- **Install Dependencies**: `mvn install -B -V -ntp`
- **API Compatibility Check**: `mvn clirr:check`
- **Sample Tests**: `mvn verify -Penable-samples` (from `samples/` directory)

## Code Style

- **Formatting**: Uses `google-java-format` via `com.spotify.fmt:fmt-maven-plugin`
- **Linting**: Enforced through Maven build plugins and CI/CD
- **License Headers**: Required Apache 2.0 license headers on all Java files (validated via `license-checks.xml`)
- **Import Style**: Standard Java import organization, grouped by package
- **Naming Conventions**:
  - Classes: PascalCase (e.g., `JsonStreamWriter`, `BigQueryReadClient`)
  - Methods: camelCase (e.g., `createReadSession`, `appendRows`)  
  - Constants: UPPER_SNAKE_CASE (e.g., `CLIENT_ID`)
  - Packages: lowercase with dots (e.g., `com.google.cloud.bigquery.storage.v1`)
- **File Organization**: 
  - Main source: `src/main/java/com/google/cloud/bigquery/storage/`
  - Test source: `src/test/java/com/google/cloud/bigquery/storage/`
  - Resources: `src/main/resources/` and `src/test/resources/`

## Workflow

- **Development**: 
  - Local setup requires Java 8+ and Maven 3.x
  - Use `mvn clean verify` for full build and test cycle
  - Integration tests require GCP service account credentials
  - Code formatting enforced via `google-java-format`

- **Testing**: 
  - Unit tests: JUnit 4 with Mockito for mocking
  - Integration tests: Real GCP BigQuery Storage API calls (requires credentials)
  - Coverage: Tracked via Codecov integration
  - Multiple Java versions tested: 8, 11, 17, 21

- **Code Review**: 
  - All changes require GitHub pull request review
  - Automated CI/CD checks must pass (lint, test, build)
  - Pull request template enforces issue linkage and documentation updates
  - Google CLA required for external contributors

- **CI/CD Pipeline**:
  - **GitHub Actions**: Multi-Java version testing, linting, javadoc generation
  - **Kokoro**: Google's internal build system for additional testing
  - **Automated Jobs**: `test`, `lint`, `javadoc`, `clirr`, `integration`, `samples`
  - **Quality Gates**: All tests must pass, code coverage maintained, API compatibility verified

- **Release Process**: 
  - **Automated**: Uses release-please bot for version management
  - **Versioning**: Semantic versioning (e.g., `3.16.4-SNAPSHOT`)
  - **Distribution**: Published to Maven Central
  - **Backport Support**: Multiple active version branches (`2.x.x`, `3.x.x`)
  - **Dependency Management**: Renovate bot for dependency updates

- **Contribution**: 
  - Open GitHub issue before implementing changes
  - Follow Google's Open Source Community Guidelines  
  - Code samples must follow [samples format guide](https://github.com/GoogleCloudPlatform/java-docs-samples/blob/main/SAMPLE_FORMAT.md)
  - Changes require tests, documentation, and backward compatibility consideration

## Architecture & Performance

- **Client Design**: Built on Google API Extensions (GAX) for consistent client experience
- **Transport**: gRPC for high-performance, streaming operations
- **Retry Logic**: Configurable retry settings with exponential backoff
- **Flow Control**: Built-in flow control for streaming operations
- **Schema Evolution**: Automatic schema update support in JsonStreamWriter
- **Multi-Version**: Supports multiple API versions (v1, v1alpha, v1beta, v1beta1, v1beta2)
- **Native Image**: GraalVM native image support via reflection configuration
- **Observability**: OpenTelemetry metrics support for monitoring and telemetry
- **Connection Management**: Connection pooling and lifecycle management for streaming writes

## Security

- **Authentication**: Google Application Default Credentials (ADC)
- **Authorization**: IAM-based access control
- **Encryption**: TLS for transport layer security
- **Credential Management**: Secure handling via Google Auth libraries
- **Dependency Scanning**: Automated dependency vulnerability checks
- **License Compliance**: Apache 2.0 license with header validation