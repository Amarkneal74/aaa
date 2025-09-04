# NY OCM Practitioner List Job

This is a Java 21 Spring Boot batch application developed for New York State's Office of Cannabis Management (OCM) to export practitioner data from an Oracle database to CSV format for public consumption. The application implements a two-step batch processing workflow: first cleaning the output directory to remove existing files, then executing an SQL query to retrieve practitioner information (including names, addresses, specialties, counties, and contact details) from multiple database tables, processing the data in chunks of 1000 records, and writing the formatted results to CSV files. The system includes comprehensive error handling with email notifications, uses encrypted configuration properties for security, integrates with Google Cloud logging for monitoring, and generates detailed build metadata tracking for deployment and maintenance purposes.

## Features

- **Spring Boot Batch Processing**: Two-step job execution with cleanup and data export
- **Oracle Database Integration**: JDBC connectivity with optimized cursor-based reading
- **CSV Export**: Formatted practitioner data export with chunked processing (1000 records)
- **Error Handling**: Comprehensive exception handling with email notifications
- **Security**: Encrypted configuration properties using Jasypt
- **Monitoring**: Google Cloud logging integration with structured logging
- **Build Automation**: Gradle build with comprehensive metadata and version tracking

## Architecture

The application follows a layered architecture:
- **BatchApplication**: Main Spring Boot application entry point
- **JobConfig**: Spring Batch job configuration with sequential steps
- **Readers**: SQL file-based database readers with cursor pagination
- **Writers**: CSV writers for formatted output generation
- **Tasklets**: Directory cleanup and file management utilities
- **Configuration**: Database and job parameter configuration

## Data Processing

The application processes practitioner data with the following fields:
- County, City, Name
- Specialty, Address, State, ZIP
- Phone Number (formatted)

Only practitioners with public consent (`PUBLIC_LIST_CONSENT_IND = 'Y'`) are included in the export.

## Requirements

- Java 21+
- Oracle Database connectivity
- Spring Boot 4.0.0-M2
- Gradle build system

## Build & Deploy

```bash
./gradlew bootJar
```

This generates `practitioner_list_job.jar` with all dependencies included.
