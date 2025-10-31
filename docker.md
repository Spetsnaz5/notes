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
