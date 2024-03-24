# Runing Airflow in Docker

---

# docker-compose.yaml

To deploy Airflow in Docker, you should fetch `docker-compose.yaml`.

```
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.0.2/docker-compose.yaml'
```

# Initializing Env

Before starting Airflow for the first time, prepare env, i.e. create the necessary files, directories and initialize the database.
Add a .env file

```
mkdir ./dags ./logs ./plugins
```

```
echo -e "AIRFLOW_UID=$(id -u)" > .env
```

On all operating systems (macOS, Win), run database migrations and create the first user account. Run the following command:

```
docker-compose up airflow-init
```

After initialization is complete, you should see a message like this:

```
airflow-init-1 exited with code 0
```

The account created has the login `airflow` and the password `airflow`.

# Running Airflow

Now you can start all services:

```
docker compose up
```

# Running the CLI commands

To run `airflow info`, run the following command:

```
docker compose run airflow-worker airflow info
```

On MacOS, you can make your work easier and download a optional wrapper scripts that will allow you to run commands with a simpler command:

```
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.8.3/airflow.sh'
chmod +x airflow.sh
```

Now you can run the command:

```
./airflow.sh info
```

You can also use `bash` as parameter to enter interactive bash shell in the container or python to enter python container.

```
./airflow.sh bash
```

```
./airflow.sh python
```

# Cleaning up

To stop and delete containers, delete volumes with database data, download images, run:

```
docker compose down --volumes --rmi all
```
