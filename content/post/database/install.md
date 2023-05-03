---
title: "PostgreSQL"
date: 2023-02-05T13:04:18+05:30
draft: false
tags: ["database"]
---

# PostgreSQL

## Development Environment Setup

In order to setup an database for development environment, we are using here an docker container and would add an sample database from [postgresql-sample-database](https://www.postgresqltutorial.com/postgresql-getting-started/postgresql-sample-database/)

## Download and Install

We would spin up the docker container using below `docker-compose` file. 

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

Save the file and bring up the postgres container using 
`docker-compose -f <filename> -d up` that starts the container in the background. 

Verify status of your docker container by executing, 
`docker ps` 

## Database Restoration 

You can [Load PostgreSQL Sample Database](https://www.postgresqltutorial.com/postgresql-getting-started/load-postgresql-sample-database/) by following steps mentioned.

## Testing

Provide an SQL query to test if you are able to retrive the data.

