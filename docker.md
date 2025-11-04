## 索引目錄

- [核心指令 (Core Commands)](#核心指令-core-commands)
- [Docker Compose](#docker-compose)
- [Dockerfile](#dockerfile)

---

## 核心指令 (Core Commands)

### 註冊庫與搜尋 (Registry & Search)

- `docker login`: 登入 Docker Registry (預設為 Docker Hub)。
- `docker logout`: 登出 Docker Registry。
- `docker search <image-name>`: 在 Docker Hub 搜尋映像檔。

### 映像檔 (Images)

- `docker images`: 列出本機的所有映像檔。
- `docker pull <image-name>`: 從 Registry 下載映像檔。
- `docker push <username>/<image-name>`: 將本地映像檔推送到 Registry， **myusername/myapp:1.0**。
- `docker tag <source-image:tag> <target-image:tag>`: 為映像檔新增一個標籤。
- `docker rmi <image-id or image-name>`: 移除一個或多個本地映像檔。

### 容器 (Containers)
- `docker start <container-id>`: 啟動容器。
- `docker stop <container-id>`: 停止容器。
- `docker restart <container-id>`: 重啟容器。
- `docker run [OPTIONS] <image-name> [COMMAND]`: 根據指定的映像檔建立並啟動一個新容器。
  - `-d`: 在背景執行容器。
  - `-i`: 開啟標準輸入 (STDIN)，用於互動模式。
  - `-t`: 分配一個虛擬終端 (pseudo-TTY)。通常與 `-i` 合併為 `-it`。
  - `-p <host-port>:<container-port>`: 將主機的埠號對應到容器的埠號。
  - `-v <host-path>:<container-path>`: 將主機的目錄或 Volume 掛載到容器中。
  - `-e <KEY=VALUE>`: 設定環境變數。
  - `--name <name>`: 為容器指定一個名稱。
  - `--network <network>`: 將容器連接到指定的網路。
  - `--restart <policy>`: 設定重啟策略 (如 `always`, `unless-stopped`)。
  - `--rm`: 容器停止後自動刪除。
- `docker ps`: 列出正在執行的容器。
  - `-a`: 顯示所有容器（包含已停止的）。
- `docker rm <container-id>`: 刪除一個或多個已停止的容器。
  - `-f`: 強制刪除容器。
- `docker logs <container-id>`: 查看容器的日誌。
  - `-f`: 持續追蹤容器日誌（類似 tail -f）。
- `docker exec [OPTIONS] <container-id> [COMMAND]`: 在一個正在執行的容器內執行指令。
  - `-i`: 開啟標準輸入 (互動模式)。
  - `-t`: 分配一個終端。
  - `-d`: 在背景執行指令。
- `docker attach <container-id>`: 連接到正在執行的容器主程序中(使用 `Ctrl+p` `Ctrl+q` 可退出而不停止容器)。
- `docker stats`: 動態顯示容器的資源使用狀況。

### 資料卷 (Volumes)

- `docker volume create <volume-name>`: 建立 Volume。
  - `--driver <driver>`: 指定驅動。
    - `local`: 預設，資料存放在本機
    - `nfs`: 掛載到網路檔案系統
- `docker volume ls`: 列出所有 Volume。
- `docker volume rm <volume-name>`: 刪除 Volume（必須沒有被容器使用中）。
- `docker volume prune`: 清理未使用的 Volume。

### 網路 (Networks)

- `docker network create <network-name>`: 建立網路。
  - `-d, --driver`: 指定網路驅動 (如 `bridge`, `host`, `overlay`)。
    - `bridge`: 預設，本地容器互聯。
    - `host`: 使用主機網路
    - `overlay`: 跨多台 Docker 主機的分散式網路，用於 Swarm。
    - `none`: 容器不連接任何網路。
- `docker network ls`: 列出所有網路。
- `docker network rm <network-name>`: 刪除網路（需確保沒有容器在使用）。
- `docker network prune`: 清理未使用的網路。
- `docker network connect <network-name> <container>`: 容器連接指定網路。
- `docker network disconnect <network-name> <container>`: 容器中斷指定網路。

### 系統 (System)

- `docker version`: 顯示版本資訊。
- `docker info`: 顯示系統範圍資訊。
- `docker system prune`: 清理系統中未使用的資源 (懸空映像檔、已停止容器等)。
  - `-a`: 同時移除未被使用的映像檔。
  - `--volumes`: 同時移除未被使用的資料卷。

---

## Docker Compose

定義多個容器服務的設定

- `docker compose ps`: 列出所有由 Compose 啟動的容器。 
- `docker compose up`: 建立並啟動所有服務。
  - `-d`: 在背景執行。
  - `--build`: 在啟動前重新建構映像檔。
  - `--force-recreate`: 強制重建容器。
  - `--no-deps`: 不啟動服務所依賴的其他服務。
  - `--scale <service=NUM>`: 指定服務的實例數量。
  - `--remove-orphans`: 移除在 `yml` 檔案中已不存在的服務容器。
- `docker compose build`: 建構或重建服務的映像檔。
  - `-t <image-name>:<tag> <path>`:  <br> 指定映像檔名稱，方便後續管理與執行 `<tag>` 可選，指定版本標籤（預設是 latest）`<path>` Dockerfile 所在目錄（. 代表當前目錄）。
  - `--no-cache`: 不使用快取。
  - `--pull`: 總是嘗試拉取最新的基礎映像檔。
  - `--parallel`: 同時建構多個服務。
- `docker compose down`: 停止並移除所有服務、網路。
  - `-v, --volumes`: 同時移除 volume。
  - `--rmi all`: 移除建構的映像檔。
- `docker compose logs`: 查看服務日誌。
  - `-f, --follow`: 持續追蹤日誌。
- `docker compose start <image-name>`: 啟動容器。
- `docker compose stop <image-name>`: 停止容器。
- `docker compose restart <image-name>`: 重啟容器。

---

## 基本結構
``` yml
version: <version>                  # Compose 文件版本
services:                           # 定義服務
  web:                              # 服務名稱
    image: <image-name>             # 使用映像檔
    container_name: <name>          # 容器名稱（可選）
    ports:                          # 埠口對應
      - <local-port:container-port> # 主機 8080 對應容器 80
    environment:                    # 環境變數
      - <key=value>
    volumes:                        # 掛載 Volume 或目錄
      - <volume-name:container-path>
    networks:                       # 服務使用網路
      - <network-name>
    depends_on:                     # 依賴其他服務
      - <container-name>
    working_dir: <paht>             #切至工作的目錄

  db:
    image: <image-name> 
    container_name: <name>
    environment:
      MYSQL_ROOT_PASSWORD: <password>
      MYSQL_DATABASE: <db-name>
    volumes:
      - <volume-name:container-path>
    networks:
      - <network-name>

volumes:                            # 定義 Volume
  <volume-name>:
  <volume-name2>:

networks:                           # 定義網路
  <network-name>:
    driver: <driver>                  # 可選：bridge, overlay, host
```
