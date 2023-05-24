# Flask Redis Queue

Example of how to handle background processes with Flask, Redis Queue, and Docker

## Quick Start

Build and start the Docker container:

```sh
docker-compose up --build
```

Open your Client to <http://localhost:5004>

```mermaid
---
title: User Sign Up Flow
---
sequenceDiagram
  participant Client
  participant Flask
  participant Redis
  participant Worker
  Note over Flask,Worker: Server
  Client->>Flask: POST /tasks (with task type)
  activate Flask
  Flask->>Redis: Enqueue a new task to Redis
  activate Redis
  Flask-->>Client: 200 OK (Response with task ID)
  deactivate Flask
  Worker--)Redis: Worker picks up task from queue
  Client->>+Flask: GET /task/TASK_ID
  Flask->>Redis: Get Task status from queue
  Flask-->>-Client: Appropriate response

```
