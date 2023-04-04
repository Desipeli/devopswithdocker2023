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
