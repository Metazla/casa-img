## ⚠️ Repository Archived

This project is being archived because I no longer have time to maintain it. It is a fork of the original project [worph/casa-img](https://github.com/worph/casa-img), which is more up-to-date and has Docker images published (unfortunately, I forgot to use the fork button, so it's not marked as a fork).

### Other notable repositories working on this:
- [dockur/casa](https://github.com/dockur/casa) (with docker image published)
- [Mazuna/casa-img-revived](https://github.com/Mazuna/casa-img-revived)

Thanks to everyone who contributed to this project!


# CasaIMG Project

Welcome to the CasaIMG project! This project aims to deliver CasaOS (https://github.com/IceWhaleTech/CasaOS) as a docker container.

## Prerequisites
- Docker must be installed on the host (works on Windows and Linux host).
- at least 150MB of RAM

## Getting Started

The image is not yet published on DockerHub, so you have to build it yourself on your machine.

### Step 1: Clone the Repository and Build the Image
```bash
git clone --recurse-submodules https://github.com/Metazla/casa-img
cd casa-img
docker build -t casaimg .
```

### Step 2: Run the Container from the Image (See Below)

### Step 3: Access the Web Interface
Open [http://localhost:8080](http://localhost:8080) in your browser to access the web interface.


## Running the Container

### Example: Running from Docker Command Line

The image is not yet published on DockerHub, so you have to build it yourself on your machine:


To run the container, use the following command:

```bash
docker run -d \
    -p 8080:8080 \
    -e REF_NET=meta \  # optional, the network to attach the container created by CasaIMG
    -e REF_PORT=80 \  # optional, the published port for the WEB-UI of a new container installation
    -e REF_DOMAIN=nas.localhost \  # optional, the published hostname for the WEB-UI of a new container installation
    -e DATA_ROOT=/c/DATA \  # mandatory, path where the data are located (Windows /c/path/DATA or Linux /path/DATA)
    -v C:\DATA:/DATA \  # mandatory, where persistent data and app volume will be stored
    -v /var/run/docker.sock:/var/run/docker.sock \  # mandatory, allows CasaIMG to control the docker host
    --name casaimg casaimg
```

### Example: Docker Compose

Create a `docker-compose.yml` file with the following content:

```yaml
services:
  casaimg:
    image: casaimg:latest
    ports:
      - "8080:8080"
    environment:
      REF_NET: meta  # optional
      REF_PORT: 80  # optional
      REF_DOMAIN: nas.localhost  # optional
      DATA_ROOT: /c/DATA  # mandatory, path where the data are located (Windows /c/DATA or Linux /path/DATA)
    volumes:
      - C:\DATA:/DATA  # mandatory, where persistent data and app volume will be stored
      - /var/run/docker.sock:/var/run/docker.sock  # mandatory, allows CasaIMG to control the docker host
```

To start the service with Docker Compose, run:

```bash
docker-compose up -d
```
