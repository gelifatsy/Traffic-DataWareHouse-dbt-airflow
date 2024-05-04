# pNEUMA Data Warehouse

This is a data warehouse project built for the pNEUMA open dataset of naturalistic trajectories of half a million vehicles collected by a swarm of drones in a congested downtown area of Athens, Greece.

## Table of Contents
- [Data](#data)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
  - [Airflow](#airflow)
  - [dbt](#dbt)
  - [Redash](#redash)
- [Architecture](#architecture)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

## Data
The data is initially a video feed of drones tracking different vehicles on the road. This was then converted into a trajectory-describing format. In the dataset, the vehicles are described with 4 columns, and the trajectories are described with 6 repeating columns that change with approximately a 4-second time interval.

For each `.csv` file:

1. Each row represents the data of a single vehicle.
2. The first 10 columns in the first row include the column names: `track_id`, `type`, `traveled_d`, `avg_speed`, `lat`, `lon`, `speed`, `lon_acc`, `lat_acc`, `time`.
3. The first 4 columns include information about the trajectory, such as the unique `track_id`, the type of vehicle, the distance traveled in meters, and the average speed of the vehicle in km/h.
4. The last 6 columns are then repeated every 6 columns based on the time frequency. For example, column 5 contains the latitude of the vehicle at time column 10, and column 11 contains the latitude of the vehicle at time column 16.
5. The speed is in km/h, longitudinal and lateral acceleration are in m/sec^2, and the time is in seconds.

## Prerequisites
- Docker
- Docker Compose

## Installation
1. Navigate to the project folder.
2. Build an Airflow image:
   ```bash
   docker build . --tag apache_dbt/airflow:2.3.3
   ```
3. Run the Docker Compose setup:
   ```bash
   docker-compose up
   ```

## Usage

### Airflow
1. Open the Airflow web UI at `http://localhost:8080/`.
2. Activate and trigger the `load_dag` and `dbt_dag` DAGs.

### dbt
The dbt models and transformations are defined in the `dbt/` directory. You can interact with dbt through the Airflow DAGs or by running dbt commands directly in the Airflow container.

### Redash
1. Open the Redash dashboard at `http://localhost:5000/`.
2. Create new data sources, queries, and dashboards to explore the pNEUMA dataset.

## Architecture
The data warehouse architecture consists of the following components:

1. **Data Source**: The pNEUMA dataset, stored as CSV files.
2. **Ingestion**: Airflow DAGs are used to ingest the data from the CSV files into a Postgres database.
3. **Transformation**: dbt is used to define and execute the data transformations, creating a star schema data model.
4. **Visualization**: Redash is used to create interactive dashboards and reports based on the transformed data.

## Roadmap
- Implement incremental loading of data using Airflow sensors and dbt incremental models.
- Add monitoring and alerting for the data pipeline.
- Explore advanced analytics and machine learning techniques on the pNEUMA dataset.
- Integrate the data warehouse with a cloud-based data platform for scalability and cost-effectiveness.

## Contributing
Contributions are welcome! If you find any issues or have ideas for improvements, please create a new issue or submit a pull request.

## License
This project is licensed under the [MIT License](LICENSE).