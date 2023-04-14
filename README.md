# spring-boot-3-observability "working Progress"

# OpenTelemetry and Grafana

## Running and exploring Grafana stack

- run `./mvnw clean install` to build the two Spring Boot applications (`post-service` and `comment-service`)
- create the dedicated docker network so that services can reach each other and grafana with `docker network create observability_poc`
- create the dedicated docker volume so that services can reach each other and grafana with `docker volume create observability_poc`
- run `docker compose -f grafana/docker-compose.yml up -d` to start grafana in the background
- run the services with `docker compose up --build`
- run test-apis.sh script `test-apis.sh`
- open `http://localhost:3000/explore` in you browser while watching for the logs of the api-service.
- Notice the trace ids in the logs, second value into brackets. In grafana, go to the Explore View, select Tempo in the top left drop-down menu, and enter a Trace ID to see its content.

The above HTTP call goes to the `post-service`, which will call the `comment-service` for additional information. This will create a trace across both services, as should be evident in the logs with the same trace id.

The `docker compose` command also starts up an OpenTelemetry Collector, to which the Spring Boot apps send their traces. The OpenTelemetry Collector, in turn, sends the traces to Grafana.

# OpenTelemetry and Elastic

## Running and exploring Elastic stack
