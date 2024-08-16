Voting Application

This repository contains the source code for a simple distributed voting application. The application consists of multiple services, each with a specific role in the system.
Project Overview

    Vote Service: A web application where users can vote.
    Result Service: Displays the current voting results.
    Worker Service: Processes the votes and stores them in the database.

Setup Instructions
1. Create Docker Containers
Redis Container

Redis is used as a memory cache to store messages temporarily.

bash

docker run -d --name redis -h redis redis

PostgreSQL Container

PostgreSQL is used as the database for storing persistent data.

bash

docker run -d --name postgres -h postgres -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres postgres

Verify Containers

Ensure that both Redis and PostgreSQL containers are running.

bash

docker ps

2. Set Up the Application Services
Vote Application

The Vote application allows users to cast their votes. Link it to the Redis container.

bash

docker run -d -p 1000:80 --link redis:redis vote

You can access the Vote application using the instance's IP address on port 1000.
Worker Application

The Worker application connects to both Redis and PostgreSQL databases to process the votes.

bash

docker run -d --link redis:redis --link postgres:db worker

Result Application

The Result application shows the current voting results. Link it to the PostgreSQL container.

bash

docker run -d -p 1001:80 --link postgres:db result

Accessing the Applications

    Vote Application: Accessible via http://<instance-ip>:1000
    Result Application: Accessible via http://<instance-ip>:1001

Application Architecture

Below are the services and their connections:

    Vote Service: Connected to Redis
    Worker Service: Connected to Redis and PostgreSQL
    Result Service: Connected to PostgreSQL
