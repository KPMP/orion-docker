# KPMP - Orion Docker Onboarding

- Install docker for your OS and register if needed.
- Launch Docker
- Go to Advanced tab and change your memory to 4GB (Apply & restart)
- Open your terminal of choice.
- `cd {kpmp_directory}`
- `mkdir data`
- `git clone git@github.com:KPMP/orion-data.git`
- `git clone git@github.com:KPMP/orion-web.git`
- `git clone git@github.com:KPMP/orion-docker.git`
- `cd orion-docker`
- `touch .env`
- Add following items to newly created .env file.
  - `ENV_SPRING_BOOT_APPDIR={kpmp_directory}/orion-data`
  - `ENV_REACT_APPDIR={kpmp_directory}/orion-web`
  - `ENV_MYSQL_IMPORT_DIR={kpmp_directory}/orion-data/migrations`
  - `ENV_DOCKER_ENVIRONMENT=dev`
  - `ENV_DATALAKE_FILE_DIR={kpmp_directory}/data`
  - `ENV_APACHE_TOMCAT_PORT=3030`
  - `ENV_MYSQL_PORT=3306`
  - `ENV_MYSQL_ROOT_PASSWORD=`
  - `ENV_MYSQL_DATABASE=`
  - `ENV_REACT_DEV_SERVER_PORT=3000`
  - `ENV_APP_HOSTNAME="localhost"`
  - `ENV_APP_PORT=80`
- `docker-compose up -d`
- Copy the sql scripts from orion-data into the mysql container (you need to do them one at a time)
  - `docker cp ../orion-data/migrations/{name of sql script} mysql:.`
- Shell into the mysql container
  - `docker exec -it mysql bash`
- Apply the sql scripts to the orion schema
  - `mysql -uroot -p<password> orion < {script.sql}`
- Exit the mysql container
  - `exit`
- Restart the spring container
  - `docker-compose up -d --no-deps spring`
- Go to orion-web and install and build the react project
  - `cd ../orion-web`
  - `npm install`
  - `npm run build`
- Direct your browser to localhost
