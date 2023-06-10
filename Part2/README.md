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
- ./example-backend containse also this [Dockerfile](https://github.com/Desipeli/devopswithdocker2023/blob/main/part1/README.md#exercise-113)
