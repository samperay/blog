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
    image: postgres:14.1-alpine
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

The datafile can be [Downloaded](https://www.postgresqltutorial.com/wp-content/uploads/2019/05/dvdrental.zip) from the website. you need to convert it to `.tar` extension and restore using `pgadmin4`

You can [Load PostgreSQL Sample Database](https://www.postgresqltutorial.com/postgresql-getting-started/load-postgresql-sample-database/) by following steps mentioned. 

## Testing

Once all your database is completed, you can test by querying the tables. 

`select * from customer`

