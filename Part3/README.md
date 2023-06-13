 ## Exercise 3.1
 
- Repo: [https://github.com/Desipeli/express-app](https://github.com/Desipeli/express-app)
- Docker Hub: [https://hub.docker.com/repository/docker/desipeli/express-app/general](https://hub.docker.com/repository/docker/desipeli/express-app/general)

#### docker-compose.yml
```
version: "3.8"

services:
  watchtower:
    image: containrrr/watchtower
    environment:
      - WATCHTOWER_POLL_INTERVAL=60
      - WATCHTOWER_LABEL_ENABLE=true
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock

  express-app:
    image: desipeli/express-app:latest
    ports:
      - 8080:8080
    labels:
      - "com.centurylinklabs.watchtower.enable=true"
```
