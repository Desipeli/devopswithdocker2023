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
