## Exercise 2.1

#### docker-compose.yml
```
version: '3.8'

services:
  simple-web-service:
    image: devopsdockeruh/simple-web-service
    build: .
    volumes:
      - ./text.log:/usr/src/app/text.log
    container_name: web_service
```

## Exercise 2.2

#### docker-compose.yml

```
version: '3.8'

services:
  simple-web-service:
    image: devopsdockeruh/simple-web-service
    ports:
      - 8080:8080
    container_name: web_service
    command: server
```

## Exercise 2.3

#### docker-compose.yml
```
version: '3.8'

services:

  exaple-frontend:
    build: ./example-frontend
    ports:
      - 5000:5000

  example-backend:
    build: ./example-backend
    ports:
      - 8080:8080
```

- ./example-frontend contains also this [Dockerfile](https://github.com/Desipeli/devopswithdocker2023/blob/main/part1/README.md#exercise-112)
- ./example-backend contains also this [Dockerfile](https://github.com/Desipeli/devopswithdocker2023/blob/main/part1/README.md#exercise-113)

## Exercise 2.4

#### docker-compose.yml

```
version: '3.8'

services:

  redis:
    image: redis:latest

  exaple-frontend:
    build: ./example-frontend
    ports:
      - 5000:5000

  example-backend:
    build: ./example-backend
    ports:
      - 8080:8080
    environment:
      - REDIS_HOST=redis
```
- ./example-frontend & ./example-backend contain these [Dockerfiles](https://github.com/Desipeli/devopswithdocker2023/blob/main/part1/README.md#exercise-114)

## Exercise 2.5

`docker compose up --scale compute=3`

## Exercise 2.6

#### docker-compose.yml
```
version: '3.8'

services:

  db:
    image: postgres:13.2-alpine
    restart: unless-stopped
    environment:
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_USER=postgres
      - POSTGRES_DB=postgres
    volumes:
      - database:/var/lib/postgresql/data
      
  redis:
    image: redis:latest

  exaple-frontend:
    build: ./example-frontend
    ports:
      - 5000:5000

  example-backend:
    build: ./example-backend
    ports:
      - 8080:8080
    environment:
      - REDIS_HOST=redis
      - POSTGRES_HOST=db
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_DATABASE=postgres


volumes:
  database:
```

## Exercise 2.7

#### docker-compose.yml
```
version: '3.8'

services:

  db:
    image: postgres:13.2-alpine
    restart: unless-stopped
    environment:
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_USER=postgres
      - POSTGRES_DB=postgres
    volumes:
      - ./database:/var/lib/postgresql/data
      
  redis:
    image: redis:latest

  exaple-frontend:
    build: ./example-frontend
    ports:
      - 5000:5000

  example-backend:
    build: ./example-backend
    ports:
      - 8080:8080
    environment:
      - REDIS_HOST=redis
      - POSTGRES_HOST=db
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_DATABASE=postgres
```
## Exercise 2.8

#### docker-compose.yml
```
version: '3.8'

services:

  proxy:
    image: nginx
    ports:
      - 80:80
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    
  db:
    image: postgres:13.2-alpine
    restart: unless-stopped
    environment:
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_USER=postgres
      - POSTGRES_DB=postgres
    volumes:
      - ./database:/var/lib/postgresql/data
      
  redis:
    image: redis:latest

  example-frontend:
    build: ./example-frontend
    ports:
      - 5000:5000

  example-backend:
    build: ./example-backend
    ports:
      - 8080:8080
    environment:
      - REDIS_HOST=redis
      - POSTGRES_HOST=db
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_DATABASE=postgres
```
#### nginx.conf
```
events { worker_connections 1024; }

http {
  server {
    listen 80;

    location / {
      proxy_pass http://example-frontend:5000/;
    }

    # configure here where requests to http://localhost/api/...
    # are forwarded
    location /api/ {
      proxy_set_header Host $host;
      proxy_pass http://example-backend:8080/;
    }
  }
}

```
## Exercise 2.9

#### docker-compose.yml
```
version: '3.8'

services:

  proxy:
    image: nginx
    ports:
      - 80:80
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    
  db:
    image: postgres:13.2-alpine
    restart: unless-stopped
    environment:
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_USER=postgres
      - POSTGRES_DB=postgres
    volumes:
      - ./database:/var/lib/postgresql/data
      
  redis:
    image: redis:latest

  example-frontend:
    build: ./example-frontend
    ports:
      - 5000:5000
    environment:
      - REACT_APP_BACKEND_URL=http://localhost/api/

  example-backend:
    build: ./example-backend
    ports:
      - 8080:8080
    environment:
      - REDIS_HOST=redis
      - POSTGRES_HOST=db
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_DATABASE=postgres
      - REQUEST_ORIGIN=http://localhost/
```
Now all envs are declared in docker-compose.yml
