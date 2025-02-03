## 目錄
  - [基礎操作](#基礎)
  - [映像檔(Image)操作](#Image)
  - [容器(Container)操作](#Container)
  - [Volume)](#Volume)
  - [Network)](#Network)
  - [Dockerfile](#Dockerfile)
  - [Docker Compose](#docker-compose)

## 基礎
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

# 查看容器資源使用情況
docker stats

```

## Image
```
列出本機images
docker images

取得images
docker pull <images-name>

推至docker hub
docker push <username>/<images-name>

建立標籤
docker tag <source-images> <target-images>

刪除映像檔
docker rmi <image-name>

查看env並刪除
docker run --rm <image-name> env
```

## Container
```
容器詳細資訊
docker inspect <container_id>

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

查看容器內的資訊
docker logs <container-id>
    -f  #持續更新輸出

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
```

## Volume
```
建立儲存空間
docker volume create <volume-name>

顯示所有儲存空間
docker volume ls

刪除儲存空間
docker volume rm <volume-name>
```

## Network
```
建立虛擬網路
docker network create <network-name>
    --driver overlay

顯示所有network
docker network ls

容器加入虛擬網路
docker network connect <network-name> <container-name or container-id>

容器IP
docker inspect <container-id> | findstr '"IPAddress"'

容器共用實體位置
docker inspect -f '{{.Mounts}}' <container-id>
```

## Docker Compose
```
執行所有yml檔
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

## 範例 docker-compose.yml
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
