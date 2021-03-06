# Orion

## Documentation
Visit [kpmp.github.io/dlu](http://kpmp.io.github.io/dlu)

## Local Setup
On your local machine

- Open your terminal of choice.
- `cd {kpmp_directory}`
- `mkdir data`
- `git clone git@github.com:KPMP/orion-data.git`
- `git clone git@github.com:KPMP/orion-web.git`
- `git clone git@github.com:KPMP/orion-docker.git`
- `git clone git@github.com:KPMP/zipWorker.git`
- `cd zipWorker`
- `./gradlew build`
- `chmod 777 build/libs/*`
- `cd ../heavens-docker/orion`
- `cp .env.example .env`
- Modify .env values to match your machine
- `docker-compose -f docker-compose.dev.yml up -d`
- Go to orion-web and install and build the react project
  - `cd ../orion-web`
  - `npm install`
  - `npm run build`
- Direct your browser to localhost

## NOTES

### RUNNING WITH SHIBBOLETH (SHIB)
On a machine that runs with shibboleth (such as dev, qa, and prod), you will need to start the dataLakeProxyServer docker first because it houses the dataLake network that orion will connect to.

First build zipWorker:
- `cd ~/zipWorker`
- `./gradlew build`
- `chmod 777 build/libs/*`

Then start the dataLakeProxyServer:
 - `cd ~/heavens-docker/dataLakeProxyServer`
 - `docker-compose up -d`

Lastly start orion:
 - `cd ~/heavens-docker/orion`
 - `docker-compose -f docker-compose.shib.yml up -d`

### RUNNING WITHOUT SHIBBOLETH (DEV)
On a machine that runs without shibboleth and does not need proxying (such as local development), skip standing up the dataLakeProxyServer and launch orion directly.  Specify the dev file.

First build zipWorker:
- `cd ~/zipWorker`
- `./gradlew build`
- `chmod 777 build/libs/*`

The, start orion:
 - `cd ~/heavens-docker/orion`
 - `docker-compose -f docker-compose.dev.yml up -d`

