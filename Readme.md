# Sample Web Application with Docker Compose

This project sets up a classic web application using Docker Compose, consisting of three essential containers: a server, a client, and a database.

## Prerequisites

- [Docker](https://www.docker.com/get-started)

## Usage

1. Clone this repository
``` bash
    git clone https://github.com/caidam/web-app-with-docker-compose.git
    cd web-app-with-docker-compose
```

2. Build and start the containers using Docker Compose:

```bash
    sudo docker compose -f docker-compose.yml up --build
```

alternatively, you can start the project in development mode using the below command:

```bash
    sudo docker compose -f docker-compose.dev.yml up --build
```

3. Access the application
- Server: Open your web browser and go to http://localhost:5050.
- Client: Access the client application through http://localhost:8080.
- Database: The database container is running internally and is managed by the application.


## Project Structure

- `server/`: Contains the server-side code and configuration.
- `client/`: Contains the client-side code and configuration.
- `docker-compose.yml` and `docker-compose.dev.yml` : Define the Docker Compose configuration for the application depending on the chosen mode.

## Volumes and data persistency

In this project, volumes for data persistency are defined in the Docker Compose files. The volumes ensure that data is preserved between container restarts.

```yaml
services:
    server:
        build: ./server
        ports:
            - 5050:5000
        volumes:
            - ./server/src/:/app/src
    client:
        build: ./client
        ports:
          - 8080:80
        volumes:
            - ./client/src/:/app/src

    mongodb:
        image: mongo
        volumes:
            - ./data:/data/db
```

In general :
```yaml
...
    volumes:
      - /path/on/host:/path/in/container
...
```

Replace `/path/on/host` with the desired path on the host machine and `/path/in/container` with the corresponding path inside the container.



