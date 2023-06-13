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

## Exercise 3.2

- Repo: [https://github.com/Desipeli/pistepankki_backend](https://github.com/Desipeli/pistepankki_backend)
- Dockerhub [https://hub.docker.com/repository/docker/desipeli/pistepankki/general](https://hub.docker.com/repository/docker/desipeli/pistepankki/general)
- Deployed to [https://pistepankki.fly.dev/](https://pistepankki.fly.dev/)

This part from .github/workflows/main.yml is responsible for deploying the app to fly.io
```
  deploy-flyio:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: superfly/flyctl-actions/setup-flyctl@master
      - run: flyctl deploy --remote-only
        env:
          FLY_API_TOKEN: ${{ secrets.FLY_API_TOKEN }}
```
fly.toml
```
app = "pistepankki"
primary_region = "arn"

[build]
  dockerfile = "./Dockerfile"

[http_service]
  internal_port = 3001
  force_https = true
  auto_stop_machines = true
  auto_start_machines = true
  min_machines_running = 0
```

## Exercise 3.3

#### builder.sh
```
#!/bin/sh

read repo target

git clone https://github.com/$repo.git
folder=$(basename $repo)
cd $folder

docker build . -t $target
docker login
docker push $target
```

## Exercise 3.5

#### frontend Dockerfile
```
FROM node:16

EXPOSE 5000

WORKDIR usr/src/app

COPY . .

RUN apt-get update && apt-get install -y curl
RUN npm install
RUN npm run build
RUN npm install -g serve
RUN useradd -m appuser
RUN chown appuser .

USER appuser

CMD serve -s -l 5000 build
```

#### backend Dockerfile
```
FROM golang:1.16

EXPOSE 8080

WORKDIR usr/src/app

COPY . .

RUN go build
RUN adduser appuser
USER appuser

CMD ["./server"]
```
