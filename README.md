data-warehouse-dbt-airflow-postgres-redash

A data-warehouse built for the pNEUMA open dataset of naturalistic trajectories of half a million vehicles collected by a swarm of drones in a congested downtown area of Athens, Greece.

Data
The data is initially a video feed of drones tracking different vehicles on the road. Then this was turned into a trajectory describing format. In our data the vehicles are described with 4 columns, and the trajectories are described with 6 repeating columns that change with approximately 4 second time interval.

For each .csv file the following apply:

Each row represents the data of a single vehicle
The first 10 columns in the 1st row include the columns’ names (track_id; type; traveled_d; avg_speed; lat; lon; speed; lon_acc; lat_acc; time)
The first 4 columns include information about the trajectory like the unique trackID, the type of vehicle, the distance traveled in meters and the average speed of the vehicle in km/h
The last 6 columns are then repeated every 6 columns based on the time frequency. For example, column_5 contains the latitude of the vehicle at time column_10, and column_11 contains the latitude of the vehicle at time column_16.
Speed is in km/h, Longitudinal and Lateral Acceleration in m/sec2 and time in second

Getting Started
Prerequisites
Make sure you have docker installed on local machine.

Docker
Docker Compose

Getting Started
Prerequisites
Make sure you have docker installed on local machine.

Docker
Docker Compose
Installation

Navigate to the folder

Build an airflow image
docker build . --tag apache_dbt/airflow:2.3.3
Run
docker-compose up

Open Airflow web browser
Navigate to `http://localhost:8080/` on the browser

activate and trigger load_dag
activate and trigger dbt_dag

Access redash dashboard
Navigate to `http://localhost:5000/` on the browser
