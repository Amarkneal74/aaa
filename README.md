# NY OCM Practitioner List Job - Workflow Flowchart

```mermaid
flowchart TD
    A[Application Start] --> B[Spring Boot Initialization]
    B --> C[Job Execution]
    
    C --> D[Clean Output Directory]
    D --> E{Cleanup OK?}
    
    E -->|Yes| F[Read Practitioner Data]
    E -->|No| G[Job Failed]
    
    F --> H[Export to CSV]
    H --> I[Job Completed]
    
    G --> J[Send Error Email]
    J --> K[End]
    I --> K
    
    style A fill:#e1f5fe
    style I fill:#c8e6c9
    style G fill:#ffcdd2
    style J fill:#ffcdd2
```

## Component Overview

- **BatchApplication**: Main Spring Boot application with CommandLineRunner
- **JobConfig**: Defines the Spring Batch job with two sequential steps
- **CleanDirTasklet**: Cleans output directory before processing
- **SqlFileReader**: Reads practitioner data from Oracle database using SQL file
- **CsvWriter**: Writes processed data to CSV format
- **DataSourceConfig**: Configures Oracle database connection
- **Error Handling**: Email notifications for failures via GeneralErrorEmailStrategy

## Data Flow

1. Application starts and initializes Spring context
2. Job executes two sequential steps:
   - **Clean Step**: Removes old output files
   - **Export Step**: Reads from database and writes to CSV
3. Data is processed in chunks of 1000 records
4. Final CSV contains practitioner information for public consumption
