## 目錄
  - [Container 操作](#Container)
  - [Dockerfile](#Dockerfile)
  - [Docker Compose](#docker-compose)

## Container
```
查看運行中的 container
docker ps
    -a  # 所有容器包含停止

啟動容器
docker start <container-id>
    -a  # 背景運作

停止容器
docker stop <container-id>

重啟容器
docker restart <container-id>

刪除容器
docker rm <container-id>
    -f  # 強制刪除
```



```
查詢版本
docker version

登入docker hub
docker login

登出docker hub
docker logout

查詢映像檔
docker search ubuntu
    -f is-official=true #過濾指返回官方映像檔

列出本機images
docker images

取得images
docker pull <images-name>

建立標籤
docker tag <source-images> <target-images>

推至docker hub
docker push <username>/<images-name>



建立容器
docker create <images-name>



建立儲存空間
docker volume create <volume-name>

顯示所有儲存空間
docker volume ls

刪除儲存空間
docker volume rm <volume-name>

建立並啟動容器
docker run -it <images-name>
    -it  #進入container shell下指令
    -d  #container後台運作
    -p <port>:<container-port>  #container內部使用的port映射至主機
    -v  <volume-name>:<path> #掛載 volume 至容器中
    -e  HOST=127.0.0.1  #設定環境變數
    --name  #別名
    --network <network-name>  #指定網路設定
        none： 在執行 container 時，網路功能是關閉的，所以無法與此 container 連線
        container： 使用相同的 Network Namespace，所以 container1 的 IP 是 172.17.0.2 那
                    container2 的 IP 也會是 172.17.0.2
        host： container 的網路設定和實體主機使用相同的網路設定，所以 container 裡面也就可以
                  修改實體機器的網路設定，因此使用此模式需要考慮網路安全性上的問題
        bridge： Docker 預設就是使用此網路模式，這種網路模式就像是 NAT 的網路模式，例如實體主機
                  的 IP 是 192.168.1.10它會對應到 Container裡面的 172.17.0.2，在啟動 Docker
                  的 service 時會有一個 docker0 的網路卡就是在做此網路的橋接。
        overlay： container 之間可以在不同的實體機器上做連線，例如 Host1 有一個 container1，
                然後 Host2 有一個container2，container1就可以使用 overlay 的網路模式
                和 container2 做網路的連線。

進入容器(退出後會停止容器)
docker attach <container-id> 

進入容器(退出後不會停止容器)
docker exec -it <container-id> /bin/bash

刪除容器
docker rm <container-id>
    -f  #強制刪除

刪除映像檔
docker rmi <image-name>

查看容器內的資訊
docker logs <container-id>
    -f  #持續更新輸出

建立虛擬網路
docker network create <network-name>
    --driver overlay

顯示所有network
docker network ls

容器加入虛擬網路
docker network connect <network-name> <container-name or container-id>

容器訊息
docker inspect <container-id>

容器IP
docker inspect <container-id> | findstr '"IPAddress"'

容器共用實體位置
docker inspect -f '{{.Mounts}}' <container-id>

查看env並刪除
docker run --rm <image-name> env

```

## Dockerfile 
```
建立 Dockerfile
docker build -t <tag-name> <dockerfile-path>

FROM  #docker 映像檔名稱

MAINTAINER  #說明撰寫和維護人資訊

RUN  #執行指令

ARG  #設定參數(Dockerfile中使用)

ENV  #設定環境變數(容器中使用)

VOLUME  #持久化資料

WORKDIR #設置工作目錄
```

```
# PHP7.4
FROM ubuntu:20.04

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    apache2 \
    php7.4 \
    libapache2-mod-php7.4 \
    php7.4-mysql \
    vim \
    && rm -rf /var/lib/apt/lists/*

RUN sed -i 's/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf

COPY index.php /var/www/html/index.php

#VOLUME ["/storage1", "/storage2", "/storage2"]

#EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]
```

```
# PHP8.3
FROM ubuntu:20.04

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common \
    && add-apt-repository ppa:ondrej/php

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    php8.3 \
    php8.3-cli php8.3-fpm php8.3-mysql php8.3-xml php8.3-mbstring php8.3-curl \
    php8.3-zip php8.3-gd \
    libapache2-mod-php8.3 \
    vim \
    && a2enmod php8.3

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    curl \
    php-cli \
    unzip \
    && curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer

COPY index.php /var/www/html/index.php

#EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]
```

```
# PYTHON3
FROM ubuntu:latest

ENV DEBIAN_FRONTEND=noninteractive    #設置環境變數，防止互動式安裝過程中要求輸入

RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python3-venv 

RUN python3 -m venv /venv # 創建虛擬環境

RUN /venv/bin/pip install --upgrade pip # 使用虛擬環境中的 pip 安裝套件
RUN /venv/bin/pip install Django 

#RUN mkdir -p /var/www/html 
#WORKDIR /var/www/html

#RUN /venv/bin/django-admin startproject mysite

WORKDIR /var/www/html/mysite

EXPOSE 8000

CMD ["/venv/bin/python", "manage.py", "runserver", "0.0.0.0:8000"]
```

## Docker Compose
```
#執行yml檔
docker-compose up -d

顯示docker-compose安裝的images 
docker-compose ps

yml格式
services
  <container-name>
    image: <image-name>  #鏡像名稱
    environment: <var>  #環境變數
    networks: - <network-name>  #虛擬網路名稱
    ports: - <local-port>:<container-port>
    depends_on: - <container-name>  #依賴的容器
    volumes: <path>  #共用的目錄位置
    working_dir: <paht>  #切至工作的目錄
networks
  <network-name>
    driver: <type>  #bridge:容器可以連接到這個網絡並與主機以及其他容器通信
```

## docker-compose.yml
```
yml範例
version: "3.8"

services:
  mysql:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: 123
      MYSQL_ALLOW_EMPTY_PASSWORD: 1
    ports:
      - 3306:3306
    networks:
      - my-network
    volumes:
      - ./mysql/data:/var/lib/mysql

  phpmyadmin:
    image: phpmyadmin
    ports:
      - 8080:80
    environment:
      PMA_HOST: mysql
    depends_on:
      - mysql
    networks:
      - my-network

  ubuntu:
    image: my-ubuntu
    #build: .
    ports:
      - 80:80
    networks:
      - my-network
    depends_on:
      - mysql
    volumes:
      - ./php-app:/var/www/html

volumes:
  php-app:

networks:
  my-network:
    driver: bridge
```
