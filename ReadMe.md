This repository holds configuration for the on-premise version of the Planner Engine developed for the Arrowhead Copilot Suite.


## Requirements

The application consists of docker images, so you need [docker](https://www.docker.com/) to run it.

## Application architechture:

The application consists of three docker images:
* **frontend**: an Angular application which handles user interaction
* **planner-service**: This image holds the main planner engine, which is responsible for constructing and executing the plans and function calls required for solving the request or problem.
* **config-service** a supplementary service, which is responsible for managing the available plugins for the planner service, and provide information.

## Configuration

#### To properly run the application, first fill in the missing values in the *.env* file:
* **Parameters for the frontend application:**
    * **FRONTEND_PORT** - The port number where the application will be accessible. (Example: 4200)

    * **FRONTEND_PLANNER_URL** - The URL or IP address where the planner service is hosted. Required for the frontend to access the planner (by default it is the same computer where the frontend is hosted)

    * **FRONTEND_CONFIG_SERVICE_URL** - The URL or IP address where the configuration service is hosted. Required for the frontend to access the config service (by default it is the same computer where the frontend is hosted)

* Monitoring credentials <br> Running the application requires connecting to the administrator monitoring services, which is implemented using Langfuse. Ask the administrator for credentials:
    * **LANGFUSE_HOST** - URL of the Langfuse logging service.
    * **LANGFUSE_PK** - Public key for authenticating with Langfuse.
    * **LANGFUSE_SK** - Secret key for authenticating with Langfuse.

* **LLM Credentials** <br> The credentials for the LLM API used by the planner engine.<br> ***This on-premise deployment currently only support Azure OpenAI deplyoment***

    * **LLM_ENDPOINT** - The API endpoint for accessing the Azure OpenAI service.
    * **LLM_APIKEY** -API key used for authenticating requests to the LLM service.
    * **LLM_MODELNAME** - name of the OpenAI model to use (e.g., *gpt-4o*).
    * **LLM_APIVERSION** - Specifies the API version for the LLM service. (e.g. *2024-02-15-preview*)

* **MongoDB Credentials**
    * **MONGO_USERNAME** - Admin username for the MongoDB instance. (arbitrary, default: mongoadmin)

    * **MONGODB_PASSWORD** - Amin password for the MongoDB instance (aribtrary)

    * **MONGODB_DATA_DIR** - Directory path (relative to Docker Compose file) where MongoDB data will be stored. (Example: *./mongodb/*)

* **Internal Service Ports**

    * **PLANNER_PORT** - Port on which the planner engine service is exposed (any free port, default: 8002)

    * **CONFIG_SERVICE_PORT** - Port on which the config service is exposed (any free port, default: 8004)

 ## Running the application:

For running the application, use `docker compose` with the given compose file.
 
For example, for runnning from the repository directory:
```
docker compose -f docker-compose-onprem.yml up -d --pull always
```

To stop the application, run:
```
docker compose -f docker-compose-onprem.yml down
```

**The application can be accessed from the web browser on the port set in the *.env* file.**
