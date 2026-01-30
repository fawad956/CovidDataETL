# CovidDataETL

A SQL Server Integration Services (SSIS) project for extracting, transforming, and loading COVID-19 data into a business intelligence workflow.

## Overview

CovidDataETL is an enterprise data pipeline designed to process COVID-19 pandemic data from multiple sources, including global daily statistics and country-wise metrics. The project integrates data from World Health Organization (WHO) sources and transforms it into a structured SQL Server database for analysis and reporting.

## Project Structure

```
CovidDataETL/
├── Package.dtsx              # Main SSIS package with ETL logic
├── Project.params             # Project-level parameters
├── CovidDataETL.dtproj        # SSIS project file
├── Data/                      # Source data files
│   ├── country_wise_latest.csv
│   ├── WHO-COVID-19-global-daily-data.csv
│   └── WHO-COVID-19-global-data.csv
├── bin/
│   └── Development/
│       └── CovidDataETL.ispac # Compiled project archive
└── obj/
    └── Development/           # Build artifacts
```

## Data Sources

The project processes COVID-19 data from the following sources:

- **country_wise_latest.csv**: Latest confirmed cases, deaths, recoveries, and active cases by country
- **WHO-COVID-19-global-daily-data.csv**: Daily global COVID-19 statistics
- **WHO-COVID-19-global-data.csv**: Cumulative global COVID-19 data

### Data Fields

The ETL pipeline extracts and processes the following key metrics:

- Country/Region
- Confirmed Cases
- Deaths
- Recovered
- Active Cases
- New Cases
- New Deaths
- WHO Region

## Technology Stack

- **SQL Server Integration Services (SSIS)**: Data integration platform
- **SQL Server**: Target database (BI_Workflow_Covid)
- **ADO.NET**: Database connectivity
- **Local SQL Server**: (localdb)\MSSQLLocalDB instance
- **Visual Studio**: SSIS project development environment

## Getting Started

### Prerequisites

- SQL Server 2019 or later with SSIS
- SQL Server Data Tools (SSDT) for Visual Studio
- Local SQL Server instance or (localdb)\MSSQLLocalDB configured
- Source CSV files in the Data directory

### Setup Instructions

1. **Clone the Repository**
   ```bash
   git clone https://github.com/yourusername/CovidDataETL.git
   cd CovidDataETL
   ```

2. **Open the Project**
   - Open `CovidDataETL.slnx` in Visual Studio
   - Load the SSIS project file `CovidDataETL.dtproj`

3. **Configure Database Connection**
   - Update the connection manager `(localdb)\MSSQLLocalDB.BI_Workflow_Covid` if needed
   - Ensure the target database `BI_Workflow_Covid` exists

4. **Run the Package**
   - In Visual Studio, right-click `Package.dtsx`
   - Select "Execute Package"
   - Monitor the execution results

## Package Details

### Connection Managers

- **SQL Server Connection**: Targets the `BI_Workflow_Covid` database on local SQL Server instance
- **Flat File Connection**: Reads CSV data from the Data directory

### Data Flow Tasks

The main package performs the following operations:

1. **Extract**: Reads COVID-19 data from CSV files
2. **Transform**: Cleanses and validates data, performs data type conversions
3. **Load**: Inserts processed data into SQL Server tables

## Configuration

### Project Parameters

Configuration parameters can be managed through `Project.params`:

- Data source file paths
- Database connection strings
- Execution settings

### Environment Variables

The project uses the following key variables:

- Source file path: `C:\Users\fawad\Github\BI Workflow for Covid Data\`
- Database: `BI_Workflow_Covid`
- Server: `(localdb)\MSSQLLocalDB`

## Building and Deployment

### Build the Project

```bash
# In Visual Studio
Build > Build Solution
```

This creates the compiled package (`CovidDataETL.ispac`) in the `bin/Development/` directory.

### Deployment

The ISPAC file can be deployed to:

- Local SSIS Catalog
- SQL Server Integration Services server
- File system for scheduled execution

## Troubleshooting

### Common Issues

- **File Not Found**: Verify CSV files exist in the Data directory with correct paths
- **Database Connection Failed**: Check that SQL Server instance is running and credentials are correct
- **Data Type Errors**: Review the flat file connection manager column definitions

### Logging

SSIS execution logs can be found in:

- Visual Studio Output window during debugging
- SQL Server Integration Services Catalog (if deployed)
- Windows Event Viewer (Application logs)

## Performance Considerations

- Large CSV files are processed with buffering
- Data type conversions are optimized during the transform phase
- Index usage on destination tables recommended for faster inserts

## Development Notes

**Last Updated**: January 2026  
**SSIS Version**: Visual Studio 2022 with SSIS 17.0  
**Database**: SQL Server (localdb)

## Future Enhancements

- [ ] Add incremental load capability
- [ ] Implement data quality checks and validation rules
- [ ] Add error logging and notifications
- [ ] Support for additional WHO data sources
- [ ] Create scheduled job for automated daily runs
- [ ] Build related SSRS reports for data visualization


## Support

For issues, questions, or suggestions, please open an issue in the GitHub repository.

## Acknowledgments

- World Health Organization (WHO) for providing COVID-19 data
- SQL Server community for SSIS documentation and best practices

---

**Last Maintained**: January 2026
