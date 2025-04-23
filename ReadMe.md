This repository holds configuration for the on-premise version of the Planner Engine developed for the Arrowhead Copilot Suite.


## Requirements

The application consists of docker images, so you need [docker](https://www.docker.com/) to run it.

## Configuration

To run the application, first fill in the missing values in the *.env* file.

Then run the following (from the repository directory):
```
docker compose -f docker-compose-onprem.yml up -d --pull always
```

To stop the application, run:
```
docker compose -f docker-compose-onprem.yml down
```

The application can be accessed from the web browser on the port set in the *.env* file.