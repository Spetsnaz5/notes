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
