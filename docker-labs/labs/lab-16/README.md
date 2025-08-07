# Lab 16: Docker Compose for Node.js + PostgreSQL App
-  Clone source code and Dockerfile from https://github.com/Ibrahim-Adel15/docker6.git
-  Write a docker compose.yml file that define the following:
   1. App as a service for node.js application
      -  Builds the image from the provided Dockerfile in the cloned directory
      -  Expose port 3000
      -  Depends on the db service to ensure PostgreSQL is ready before the app starts
      -  Use mynet network
   2. DB as a service for PostgreSQL Database
      -  Uses the image: postgres:15 alpine
      -  Runs on port 5432
      -  Uses the following environment variables:
         -  o POSTGRES_USER: postgres
         -  o POSTGRES_PASSWORD : postgres
         -  o POSTGRES_DB: postgres
      -  Mounts a volume postgres_data for data persistence (/var/lib/postgresql/data)
      -  Use mynet network
   3. postgres_data as a volume
   4. mynet as a network
---

## **1️⃣ Clone the Source Code**
Clone the provided Node.js application and Dockerfile:

```
git clone https://github.com/IbrahimAdel15/docker6.git
```
## 2️⃣ Create docker-compose.yaml file
```
version: "3.9"

services:
  app:
    build: .
    container_name: node_app
    ports:
      - "3000:3000"
    depends_on:
      - db
    networks:
      - mynet

  db:
    image: postgres:15-alpine
    container_name: postgres_db
    ports:
      - "5432:5432"
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: postgres
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - mynet

volumes:
  postgres_data:

networks:
  mynet:
```
## 3️⃣ Run the Services
Build and start the containers:
```
docker compose up -d
```
## 4️⃣ Verify Containers Are Running
```
docker ps
```
Expected output:

```
node_app      → Node.js application on port 3000
postgres_db   → PostgreSQL database on port 5432
```
## 5️⃣ Test the Node.js App
Access the app in a browser or via curl:
```
curl http://localhost:3000
```
Expected output:

```
PostgreSQL Connection Test App
```
## 6️⃣ Access the PostgreSQL Database
Enter the PostgreSQL interactive shell:
```
docker exec -it postgres_db psql -U postgres -d postgres
```
Inside PostgreSQL:
```
\l        -- list databases
```
## 7️⃣ Create a Test Table
```
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50)
);

INSERT INTO users (name) VALUES ('Ahmed');

SELECT * FROM users;
```
Example output:
```
 id |  name
----+--------
  1 | Ahmed
(1 row)
```
Exit:
```
\q
```
## 8️⃣ Stop and Remove Containers
Stop containers (keep database data):
```
docker compose down
```
Stop and remove containers and database volume:
```
docker compose down -v
```
