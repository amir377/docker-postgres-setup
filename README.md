
# Docker Postgres Setup

This repository provides an easy-to-use solution for deploying a Postgres database inside a Docker container. It includes a user-friendly PowerShell script (`install.ps1`) and a Bash script (`install.sh`) to automate the process of setting up a Postgres container with customizable parameters.

## Features

1. **Environment File Generation**: Automatically generates a `.env` file with user-defined parameters such as container name, network name, port, and database credentials.
2. **Docker Network Management**: Creates a Docker network if it doesn’t already exist.
3. **Docker Compose Configuration**: Dynamically generates a `docker-compose.yaml` file from a `docker-compose.example.yaml` template.
4. **Build and Run**: Executes `docker-compose up -d --build` to build and start the Postgres container.
5. **Container Status Check**: Checks the container status post-deployment.
6. **Error Handling**: Automatically displays logs if the container fails to start.
7. **Interactive Access**: Automatically connects to the container shell if it starts successfully.

## Prerequisites

- Docker must be installed and running on your system.
- Docker Compose must be installed.
- **Linux Only**: Ensure `dos2unix` is installed to handle line ending conversions if needed.
  ```bash
  sudo apt install dos2unix
  ```
- Git must be installed and available in your system's PATH.
  ```bash
  sudo apt install git       # For Debian/Ubuntu
  sudo yum install git       # For CentOS/RHEL
  brew install git           # For macOS
  ```
- Windows PowerShell (Admin) or a Bash-compatible terminal for script execution.

## Installation Steps

### One Command Install and Clone

#### Windows

Open PowerShell as Administrator and run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass; git clone https://github.com/amir377/docker-postgres-setup; cd docker-postgres-setup; ./install.ps1
```

#### Linux/Mac

Run the following command in your terminal:
```bash
git clone https://github.com/amir377/docker-postgres-setup && cd docker-postgres-setup && dos2unix install.sh && chmod +x install.sh && ./install.sh
```

## Manual Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/amir377/docker-postgres-setup.git
   cd docker-postgres-setup
   ```

2. Place your `docker-compose.example.yaml` file in the root directory (if not already provided).

3. Run the appropriate installation script:
   - For Windows: `install.ps1`
   - For Linux/Mac: `install.sh`

4. Follow the prompts to customize your setup:
   - Container name
   - Network name
   - Postgres port
   - Database name
   - Postgres user credentials
   - Allowed host

## File Descriptions

### `install.ps1`

Automates the entire setup process for Windows, including:

- Generating `.env` and `docker-compose.yaml` files.
- Ensuring Docker and Docker Compose are installed.
- Creating the specified Docker network.
- Building and starting the Postgres container.
- Providing access to the container shell or logs based on status.

### `install.sh`

Automates the setup process for Linux/Mac, including:

- Generating `.env` and `docker-compose.yaml` files.
- Ensuring Docker and Docker Compose are installed.
- Creating the specified Docker network.
- Building and starting the Postgres container.
- Providing access to the container shell or logs based on status.

### `.env`

Holds configuration values for the Postgres container. Example:

```env
CONTAINER_NAME=postgres
NETWORK_NAME=general
POSTGRES_PORT=5432
ALLOW_HOST=0.0.0.0
POSTGRES_DATABASE=general
POSTGRES_USER=admin
POSTGRES_PASSWORD=adminpassword
```

### `docker-compose.example.yaml`

A template file for the `docker-compose.yaml` file. Placeholders are dynamically replaced with values from the `.env` file.

### `docker-compose.yaml`

Generated file used to deploy the Postgres container with Docker Compose.

## Usage

### Accessing the Postgres Database

- Host: The `ALLOW_HOST` value specified during setup (default: `127.0.0.1`)
- Port: The `POSTGRES_PORT` value specified during setup (default: `5432`)
- Username: The `POSTGRES_USER` value specified during setup
- Password: The `POSTGRES_PASSWORD` value specified during setup

### Viewing Logs

If the container fails to start, the script will display logs automatically:

```bash
docker logs <container-name>
```

### Accessing the Container Shell

If the container starts successfully, the script will connect to the container shell automatically:

```bash
docker exec -it <container-name> bash
```

## Notes

- Ensure Docker is running before executing the script.
- If you encounter permission issues, run PowerShell or Bash as Administrator.
- Update the `docker-compose.example.yaml` file to suit your specific requirements.

## License

This project is licensed under the MIT License. See the LICENSE file for details.

---

Feel free to customize the script or template files to fit your specific use case!
