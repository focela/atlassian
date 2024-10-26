
# Jira Docker Container

This repository provides a Docker setup for running Jira with MySQL as the database backend. It includes two main services: `jira` and `jira_db` (MySQL).

## 📂 Project Structure

- **Dockerfile**: Defines the environment for Jira with the required configurations and dependencies.
- **.github/workflows/docker-publish.yml**: GitHub Action workflow for building and pushing Docker images.
- **LICENSE**: Licensing information.
- **README.md**: Project documentation.

## 🚀 Getting Started

### Prerequisites

- Docker
- Docker Compose

## 📝 Example compose.yaml

Here's a sample `compose.yaml` configuration:

```yaml
services:
  jira_db:
    container_name: jira_db
    restart: always
    image: mysql:8.0
    environment:
      - MYSQL_USER=${JIRA_DB_USER:-jira}
      - MYSQL_DATABASE=${JIRA_DB_NAME:-jira_db_name}
      - MYSQL_PASSWORD=${JIRA_DB_PASSWORD:-jira_password}
      - MYSQL_ROOT_PASSWORD=${JIRA_DB_ROOT_PASSWORD:-jira_root_password}
    command: ['mysqld', '--character-set-server=utf8mb4', '--collation-server=utf8mb4_bin']
    volumes:
      - jira_db_data:/var/lib/mysql
    networks:
      - focela_network
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost"]
      interval: 30s
      timeout: 10s
      retries: 5

  jira:
    container_name: jira
    restart: always
    image: focela/jira:${JIRA_VERSION:-9.12.14}
    environment:
      - ATL_PROXY_NAME=${JIRA_ATL_PROXY_NAME:-localhost}
      - ATL_PROXY_PORT=${JIRA_ATL_PROXY_PORT:-443}
      - ATL_TOMCAT_PORT=${JIRA_ATL_TOMCAT_PORT:-8080}
      - ATL_TOMCAT_SCHEME=${JIRA_ATL_TOMCAT_SCHEME:-https}
      - ATL_TOMCAT_SECURE=${JIRA_ATL_TOMCAT_SECURE:-true}
      - TZ=${JIRA_TZ:-Asia/Ho_Chi_Minh}
    ports:
      - ${JIRA_PORT:-8080}:8080
    volumes:
      - jira_data:/var/jira
    depends_on:
      - jira_db
    networks:
      - focela_network
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8080"]
      interval: 30s
      timeout: 10s
      retries: 5
      start_period: 30s

networks:
  focela_network:
    driver: bridge
    name: focela_network

volumes:
  jira_db_data:
  jira_data:
```

## 📦 Volumes

- `jira_db_data`: Stores MySQL data for Jira.
- `jira_data`: Stores Jira's application data.

## 🛠 Troubleshooting

Check the container logs if you encounter any issues:

```bash
docker-compose logs jira
docker-compose logs jira_db
```


### 🌐 Setup

1. Clone this repository:

   ```bash
   git clone https://github.com/focela/jira.git
   cd jira
   ```

2. Create a `.env` file in the root of your project and configure the following values based on your requirements.

### ⚙️ Environment Variables

These environment variables should be set in a `.env` file:

#### MySQL Database Configuration for `jira_db`
- `JIRA_DB_USER`: Username for the Jira database (default: `jira`).
- `JIRA_DB_NAME`: Database name for Jira (default: `jira_db_name`).
- `JIRA_DB_PASSWORD`: Password for the Jira database user.
- `JIRA_DB_ROOT_PASSWORD`: Root password for MySQL.

#### Jira Application Configuration
- `JIRA_VERSION`: The version of Jira to use (default: `9.12.14`).
- `JIRA_PORT`: The external port for accessing Jira (default: `8080`).

#### Jira Tomcat Configuration
- `JIRA_ATL_PROXY_NAME`: The proxy name for Jira (default: `localhost`).
- `JIRA_ATL_PROXY_PORT`: The proxy port (default: `443`).
- `JIRA_ATL_TOMCAT_PORT`: The Tomcat port for Jira (default: `8080`).
- `JIRA_ATL_TOMCAT_SCHEME`: The scheme to use for Tomcat (`http` or `https`, default: `https`).
- `JIRA_ATL_TOMCAT_SECURE`: Specifies if Tomcat is secured (default: `true`).

#### Jira Timezone Configuration
- `JIRA_TZ`: Timezone setting for Jira (default: `Asia/Ho_Chi_Minh`).

3. Start the services using Docker Compose:

   ```bash
   docker-compose up -d
   ```

4. Access Jira at `http://localhost:8080`.

## 📋 License

This software is for **internal use only** at Focela Technologies. Redistribution and sublicensing are prohibited.

---

> Made with ❤️ by Focela Technologies
