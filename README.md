# CityBikes Data Pipeline

This project implements a data pipeline for collecting and analyzing bike-sharing system data using the CityBikes API. The pipeline includes data extraction, loading, transformation, and analysis capabilities.

## Project Structure

```
.
├── citybikes-pipeline.py    # Main pipeline implementation
├── dbt_project.yml         # DBT project configuration
└── packages.yml            # DBT package dependencies
```

## Components

### Main Pipeline (`citybikes-pipeline.py`)

The main pipeline script handles:

- Data extraction from the CityBikes API
- Station coverage analysis
- Data loading into PostgreSQL
- Integration with dbt for transformations

Key features:
- Environment-based configuration (development, staging, production)
- Configurable city selection via environment variables
- Comprehensive station coverage analysis including:
  - Station density calculations
  - Coverage gap identification
  - Location recommendations
- Error handling and logging

### DBT Configuration (`dbt_project.yml`)

The dbt project configuration defines:
- Project name: `citybikes_dbt`
- Version: 1.0.0
- Model materialization strategies:
  - Default: tables
  - Staging: views
  - Analytics: tables

## Setup

1. Set up environment variables:
   ```bash
   ENVIRONMENT=production  # or 'development' or 'staging'
   CITY_NAME=Chicago      # or any other supported city
   ```

2. Install required Python packages:
   ```bash
   pip install dlt requests pandas numpy geopy python-dotenv
   ```

3. Configure dbt:
   - Ensure dbt profiles are set up in `.dbt` directory
   - Run `dbt deps` to install dependencies

## Data Model

The pipeline creates three main tables:
1. `network_info`: Basic information about the bike-sharing network
2. `station_data`: Detailed station information including location and availability
3. `coverage_analysis`: Analytics on station coverage and recommendations

## Usage

Run the pipeline:
```bash
python citybikes-pipeline.py
```

The pipeline will:
1. Extract data from CityBikes API
2. Load data into PostgreSQL
3. Perform coverage analysis
4. Execute dbt transformations

## Error Handling

The pipeline includes comprehensive error handling for:
- API connection issues
- Data validation
- Database operations
- DBT transformation errors

## Development

- Use `ENVIRONMENT=development` for testing
- Dev mode enables additional logging and data validation
- Staging environment available for pre-production testing

## Dependencies

- Python 3.x
- dbt
- PostgreSQL
- Required Python packages listed in requirements.txt (not shown)
- External APIs:
  - CityBikes API (http://api.citybik.es/v2/)
  - Nominatim Geocoding Service

## Note

Ensure proper configuration of PostgreSQL credentials and connection details in your dbt profiles before running the pipeline.
