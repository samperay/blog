---
title: "PostgreSQL"
date: 2023-02-05T13:04:18+05:30
draft: false
tags: ["database"]
---

## Development Environment Setup

In order to setup an database for development environment, we are using here an docker container and would add an sample database from [postgresql-sample-database](https://www.postgresqltutorial.com/postgresql-getting-started/postgresql-sample-database/)

## Installation

Create a new directory and file called `docker-compose-postgres.yml`. 
Copy the below content into newly created file. 

```
version: '3.8'
services:
  db:
    image: sunlnx/postgresql:v1
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
    ports:
      - '5432:5432'
    volumes: 
      - db:/var/lib/postgresql/data
volumes:
  db:
    driver: local
```

Save the file, bring up the postgres container using 
`docker-compose -f docker-compose-postgres.yml -d up` that starts the container in the background. Verify container status by `docker ps` 

## Database Restoration using pgadmin4

You can [Load PostgreSQL Sample Database](https://www.postgresqltutorial.com/postgresql-getting-started/load-postgresql-sample-database/) as described.