
# `Containerization of Medusa_Backend by integrating PostgreSQL and Redis with Docker`

This project containerizes the Medusa backend with PostgreSQL as the database and Redis for caching. Docker and Docker Compose are used to orchestrate the services.

## `Process Overview:`

### `Medusa Backend Setup:`
```
The Medusa backend is built using Node.js and the Medusa framework, serving as the core e-commerce service.
```
### `PostgreSQL Integration:`
```
PostgreSQL is used as the main relational database to store product, customer, and order data for the Medusa backend.
```
### `Redis Integration:`
```
Redis is utilized as a caching layer to improve the performance of data retrieval and manage background tasks.
```
### `Docker and Docker Compose:`
```
Docker images are built for each service (Medusa, PostgreSQL, Redis).

Docker Compose handles the orchestration of these services, ensuring they run together smoothly.

```
## 🔗 Links

[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/sathish-gurka)


## Authors

- [@GurkaSathish](https://github.com/sathishyadav024)


## Pre-Requisites

- `Linux Server`
- `Docker`
- `docker-compose`
- `Git`
## `Install Medusa_Backend Project`

```
$ docker run --rm -v $(pwd):/app -w /app node:18 npx @medusajs/medusa-cli new medusa-backend
```
```
# cd medusa_backend
```

## `Create a Dockerfile`

```
$ mkdir Dockerfile
```
```
$ sudo vim Dockerfile
```
```
# Dockerfile
FROM node:18

# Set working directory
WORKDIR /app

# Install Medusa CLI globally
RUN npm install -g @medusajs/medusa-cli

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the application port
EXPOSE 9000

# Start the Medusa server
CMD ["medusa", "develop"]


```
## `Create a docker-compose.yml`

```
$ mkdir docker-compose.yml
```
```
$ sudo vim docker-compose.yml
```

```
#docker-compose.yml:

version: '3.8'

services:
  medusa:
    build: .
    environment:
      - MEDUSA_DB_TYPE=postgres
      - MEDUSA_DB_URL=postgres://medusa:sathish@db:5432/medusadb
      - MEDUSA_REDIS_URL=redis://redis:6379
    ports:
      - "9000:9000"
    depends_on:
      - db
      - redis
    volumes:
      - .:/app
    command: bash -c "npx medusa migrations run && npx medusa develop"
    restart: on-failure

  db:
    image: postgres:14
    environment:
      - POSTGRES_USER=medusa
      - POSTGRES_PASSWORD=sathish
      - POSTGRES_DB=medusadb
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7

volumes:
  postgres_data:

```
## `Run docker-compose up`
```
$ docker-compose up
```
## `Result`

`Successfully build images and run containers of Medusa,Postgresql and Redis Using DOCKER` 
