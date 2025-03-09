# Open WebUI and Pipelines - Docker Compose Setup

## Overview
This `docker-compose.yml` file sets up two services:
1. **Open WebUI** - A web-based user interface for managing AI pipelines.
2. **Pipelines** - A service for running AI-related pipelines.

Both services run in separate containers and communicate with each other. 

---

## Prerequisites
Ensure you have the following installed:
- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

---

## Services Explained

### 1. Open WebUI
- **Image:** `ghcr.io/open-webui/open-webui:latest`
- **Container Name:** `open-webui`
- **Restart Policy:** `unless-stopped`
- **Ports:**
  - Maps port `8080` in the container to `3000` on the host.
- **Volumes:**
  - Stores backend data in a named volume `open-webui`.

### 2. Pipelines
- **Image:** `ghcr.io/open-webui/pipelines:latest`
- **Container Name:** `pipelines`
- **Restart Policy:** `always`
- **Ports:**
  - Exposes port `9099` on both the container and the host.
- **Extra Hosts:**
  - Allows the container to communicate with the host system using `host.docker.internal`.
- **Environment Variables:**
  - `PIPELINES_DIR=/pipelines`: Sets the directory for storing pipeline files.
  - `PIPELINES_REQUIREMENTS_PATH=/pipelines`: Specifies the path for required dependencies.
- **Volumes:**
  - Mounts the `./pipelines` directory from the host to `/pipelines` inside the container.

---

## Running the Services
To start the services, use the following command:
```sh
docker-compose up -d
```
This will start both containers in detached mode.

To stop the services, run:
```sh
docker-compose down
```

---

## Accessing the Services
- Open WebUI: [http://localhost:3000](http://localhost:3000)
- Pipelines API: Accessible on port `9099`

---

## Persistent Data
- The Open WebUI stores its backend data in the named volume `open-webui`.
- The `pipelines` directory on the host system is mounted into the container to persist pipeline-related files.

---

## Troubleshooting
- Check logs using:
  ```sh
  docker-compose logs -f
  ```
- Restart a specific service:
  ```sh
  docker-compose restart <service_name>
  ```
- Remove containers and volumes (WARNING: This deletes all stored data):
  ```sh
  docker-compose down -v
  ```

---

## License
This project follows the licensing of Open WebUI and Pipelines repositories.

For more information, visit their GitHub repositories:
- Open WebUI: [GitHub](https://github.com/open-webui/open-webui)
- Pipelines: [GitHub](https://github.com/open-webui/pipelines)