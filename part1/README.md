# Part 1

## Exercise 1.1

![](https://raw.githubusercontent.com/Desipeli/devopswithdocker2023/main/part1/exercise1_1.png)
## Exercise 1.2

![](https://raw.githubusercontent.com/Desipeli/devopswithdocker2023/main/part1/exercise1_2.png)
## Exercise 1.3

![](https://raw.githubusercontent.com/Desipeli/devopswithdocker2023/main/part1/exercise1_3.png)
```
sudo docker run -d -it --name tehtava devopsdockeruh/simple-web-service:ubuntu
sudo docker exec -it tehtava bash
tail -f ./text.log
```
## Exercise 1.4

![](https://raw.githubusercontent.com/Desipeli/devopswithdocker2023/main/part1/exercise1_4_1.png)
![](https://raw.githubusercontent.com/Desipeli/devopswithdocker2023/main/part1/exercise1_4_2.png)

flags `-it` and `--rm` and added `apt-get update; apt-get -y install curl;` to sh

## Exercise 1.5

```
devopsdockeruh/simple-web-service   ubuntu    4e3362e907d5   2 years ago   83MB
devopsdockeruh/simple-web-service   alpine    fd312adc88e0   2 years ago   15.7MB
```

```
sudo docker exec -it 30 sh
/usr/src/app # ls
server    text.log
/usr/src/app # tail -f text.log 
2023-04-04 15:56:03 +0000 UTC
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```

## Exercise 1.6

```
sudo docker run -it devopsdockeruh/pull_exercise
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

## Exercise 1.7

```
FROM ubuntu:20.04

WORKDIR /usr/src/app

COPY skripti.sh .

RUN chmod +x skripti.sh; apt-get update; apt-get install curl -y

CMD ./skripti.sh
```
## Exercise 1.8

```
### Dockerfile:

FROM devopsdockeruh/simple-web-service:alpine

CMD server
```
## Exercise 1.9

```
docker run --rm -v "$(pwd)/mydir/text.log:/usr/src/app/text.log" devopsdockeruh/simple-web-service
```

## Exercise 1.10

```
docker run -p 127.0.0.1:8080:8080 --rm web-server
```
## Exercise 1.11

```
FROM openjdk:8

EXPOSE 8080

WORKDIR /usr/src/app

COPY . .

RUN ./mvnw package

CMD java -jar ./target/docker-example-1.1.3.jar



docker run -p 127.0.0.1:8080:8080 --rm -d spring111:latest
```

## Exercise 1.12

```
FROM node:16

EXPOSE 5000

WORKDIR usr/src/app

COPY . .

RUN apt-get update && apt-get install -y curl
RUN npm install
RUN npm run build
RUN npm install -g serve

CMD serve -s -l 5000 build



docker run -p 127.0.0.1:5000:5000 example-frontend
```
## Exercise 1.13

```
FROM golang:1.16

EXPOSE 8080

WORKDIR usr/src/app

COPY . .

RUN go build

CMD ["./server"]


docker build -t example-backend .
docker run -d -p 127.0.0.1:8080:8080 example-backend
```
