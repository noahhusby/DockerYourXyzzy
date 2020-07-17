# Docker Your Xyzzy

Get your Xyzzy on: `docker pull emcniece/dockeryourxyzzy`

- Github: [emcniece/DockerYourXyzzy](https://github.com/emcniece/DockerYourXyzzy)
- Docker Hub: [emcniece/dockeryourxyzzy](https://hub.docker.com/r/emcniece/dockeryourxyzzy/)


# Supported tags and respective `Dockerfile` links:

- `latest`, `3` ([Dockerfile](./Dockerfile))
- `latest`, `run`, `2`, `2-run` ([Dockerfile](https://github.com/emcniece/DockerYourXyzzy/blob/83bfeebe9c3a7619dd4409c02b92fa8b88dd298a/Dockerfile))
- `base`, `2-base` ([Dockerfile](https://github.com/emcniece/DockerYourXyzzy/blob/83bfeebe9c3a7619dd4409c02b92fa8b88dd298a/Dockerfile))
- `dev`, `2-dev` ([Dockerfile](https://github.com/emcniece/DockerYourXyzzy/blob/83bfeebe9c3a7619dd4409c02b92fa8b88dd298a/Dockerfile))


# What is Docker Your Xyzzy?

This is a containerized build of the [Pretend You're Xyzzy](https://github.com/ajanata/PretendYoureXyzzy) Cards Against Humanity clone.

> ⚠ Version 3 (April 2020) is a vastly simplified Docker image, may break if upgrading from version 2. It no longer features multi-step builds.


# Usage

The PYX project can be used in Docker format for development, outputting the built files, or running in production.


## Run with Docker-Compose (fastest)

An example stack of PYX with a Postgres database and an [Ngrok](https://ngrok.com/) tunnel can be found in [docker-compose.yml](./docker-compose.yml):

```sh
# Run PYX/Postgres stack
docker-compose up -d --build
```

Once the containers are running, you can:

- Visit http://localhost:8080/game.jsp to play locally
- Visit http://localhost:4040/status to find your Ngrok URL
- Visit https://#####.ngrok.io to share publicly

## Run Standalone Container

Keep the container up with SQLite and `war:exploded jetty:run`:

```sh
docker run -d \
  -p 8080:8080 \
  --name pyx-dev \
  emcniece/dockeryourxyzzy:latest

# Visit http://localhost:8080 in your browser
# Or, start a bash session within the container:
docker exec -it pyx-dev bash
```

## Run With Overrides

Settings in `build.properties` can be modified by passing them in the container CMD:

```sh
docker run -d \
  -p 8080:8080 \
  emcniece/dockeryourxyzzy:latest \
  mvn clean package war:war \
    -Dhttps.protocols=TLSv1.2 \
    -Dmaven.buildNumber.doCheck=false \
    -Dmaven.buildNumber.doUpdate=false \
    -Dmaven.hibernate.url=jdbc:postgresql://postgres/pyx
```
