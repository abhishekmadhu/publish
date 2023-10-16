---
type: note
tags:
  - permanent
  - zettelkasten
  - programming
share: "true"
---
#permanent


Easy to run [[Postgres|Postgres]] in [[Docker|Docker]] - summarized from [[How to Run PostgreSQL and pgAdmin Using Docker  by Mahbub Zaman  Towards Data Science|How to Run PostgreSQL and pgAdmin Using Docker  by Mahbub Zaman  Towards Data Science]]

Use the following [[Docker Compose|Docker Compose]] 
```yml
version: '3.8'
services:
  db:
    container_name: pg_container
    image: postgres
    restart: always
    environment:
      POSTGRES_USER: root
      POSTGRES_PASSWORD: root
      POSTGRES_DB: test_db
    ports:
      - "5432:5432"
  pgadmin:
    container_name: pgadmin4_container
    image: dpage/pgadmin4
    restart: always
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@admin.com
      PGADMIN_DEFAULT_PASSWORD: root
    ports:
      - "5050:80"
```

Store it in a folder, and just run `docker compose up` from that folder. 

Then, when both the services are up and running...
1. Open up [[pgAdmin|pgAdmin]] in a browser at `localhost:5050`
2. Log in to [[pgAdmin|pgAdmin]] using the username and password mentioned above 
3. To connect to [[Postgres|Postgres]] from [[pgAdmin|pgAdmin]], use the host `pg_container` (the name of the container that we defined in the [[Docker Compose|Docker Compose]] file) - 
	1. The network works that way
4. List the docker containers with `docker ps`, and grab the container id for the `postgres` container. 
5. Get the IP address of the `postgres` container using `docker inspect <id> | grep IPAddress`
6. Take the IP Address and use it to create connection from [[pgAdmin|pgAdmin]]