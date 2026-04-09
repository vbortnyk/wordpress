# Wordpress

This project provides a containerized setup for running a WordPress website using Docker and Docker Compose.

It includes a preconfigured environment with WordPress and MariaDB, managed via a `docker-compose.yml` file and environment variables defined in a `.env` file.

The purpose of this project is to simplify local WordPress development and setup, provide persistent storage for both website files and the database using Docker volumes, demonstrate how to run a full web application stack using containerization.

This setup allows you to quickly start, stop, and recreate the entire WordPress environment without manual installation of dependencies on the host system.

## Table of contents
- [Requirements](#requirements)
- [Quick start](#quick-start)
- [Data persistance](#data-persistance)
- [Networking](#-and-networking)


### Requirements
 - Docker installed on your system
 - Docker Compose (usually included with Docker Desktop)
 - Basic knowledge of running commands in a terminal
 - A system that supports Docker (Linux, macOS, or Windows)
 - Internet connection to pull required images:
    - WordPress
    - MariaDB

### Quick start
Clone the repository:
```bash
$ git clone git@github.com:vbortnyk/wordpress.git
$ cd <your-repo-folder>
```
The `.env-template` file contains all required environment variables. Rename it to `.env` and adjust the values according to your local setup.
```bash
$ mv .env-template .env
```
Set values to environment variables:
```bash
WORDPRESS_IMAGE=
MARIADB_IMAGE=
```
Reommended images: 
 - Wordpress: `wordpress:6.4-apache`
 - MriaDB: `mariadb:latest`


Adjust values like database name, user, and password.
```bash
MARIADB_DATABASE= #Create a database with this name automatically when the container starts
MARIADB_USER= #This user is created automatically when the container starts
MARIADB_PASSWORD= #Used together with `MARIADB_USER` to access the database
MARIADB_ROOT_PASSWORD= #Sets the password for the root (admin) user of MariaDB
```

Start the stack using Docker Compose:
```bash
$ docker compose up -d
```
Open your browser and access WordPress:
```bash
<host-ip>:8080
```
Follow the WordPress installation wizard and connect it to the database (MariaDB).


### Data Persistence
The database (MariaDB) stores its data in a Docker volume mounted to: `/var/lib/mysql`

The WordPress files (WordPress) are stored in a volume mounted to: `/var/www/html`

Additionally, the services are configures with the restart policy `unless-stopped`

This configuration ensures that containers automatically restart after as system reboot or Docker restart, unless they are manually stopped.

### Networking
All services run on a shared network created by Docker Compose.

Containers communicate using service names as hostnames