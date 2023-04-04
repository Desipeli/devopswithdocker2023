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
