# Postgresql and pgAdmin installation with Docker

This is working example of installing postgresql and pgAdmin. You can use this configuration or create own configuration based on this one.

## Installing

1. Open terminal and clone repo anywhere at your home folder:

   ```shell
   git clone https://github.com/vivazzi/docker_pg_admin.git
   cd docker_pg_admin
   ```

2. Pull docker images: postgres, pgadmin:

   ```
   docker pull postgres
   docker pull dpage/pgadmin4
   ```

3. (optionally) `.env` consists of default variables for database connection. You can copy `.env` to new file, for example, `.env.dev` to apply your custom variables.

4. Run containers:
    
   ```shell
   # With default .env environment:
   docker compose up
   
   # Or with custom environment, for example, .env.dev:
   docker compose --env-file ./.env.dev up
   ```

# Connection to the db server

1. Get `IPAddress` of your postgresql container (this is required to connect to the server):
   
   ```shell
   $ docker ps
   
   CONTAINER ID   IMAGE            COMMAND                  CREATED              STATUS                          PORTS                                            NAMES
   771a12c63380   dpage/pgadmin4   "/entrypoint.sh"         About a minute ago   Up About a minute (unhealthy)   443/tcp, 0.0.0.0:5555->80/tcp, :::5555->80/tcp   docker_pg_admin-pgadmin-1
   5c20922bf03f   postgres         "docker-entrypoint.s…"   About a minute ago   Up About a minute               0.0.0.0:6543->5432/tcp, :::6543->5432/tcp        docker_pg_admin-postgres-1
   ```
   
   ```shell
   docker inspect docker_pg_admin-postgres-1 | grep IPAddress
   ```

2. Run `localhost:5555` in the browser and input email and password defined in `PGADMIN_DEFAULT_EMAIL` and `PGADMIN_DEFAULT_PASSWORD`.

3. Register new server with credentials:

   ```
   Host: <IPAddress>
   Port: 5432
   Maintenance database: postgres
   Username: <POSTGRES_USER>
   Password: <POSTGRES_PASSWORD>
   ```