## 索引目錄

- [1. 套件管理 (Package Management)](#1-套件管理-package-management)
- [2. 檔案與目錄操作 (File & Directory Operations)](#2-檔案與目錄操作-file--directory-operations)
- [3. 管道與重導向 (Piping & Redirection)](#3-管道與重導向-piping--redirection)
- [4. 檔案內容檢視與處理 (File Content & Processing)](#4-檔案內容檢視與處理-file-content--processing)
- [5. 搜尋檔案與指令 (Searching Files & Commands)](#5-搜尋檔案與指令-searching-files--commands)
- [6. 權限與擁有者 (Permissions & Ownership)](#6-權限與擁有者-permissions--ownership)
- [7. 系統資訊 (System Information)](#7-系統資訊-system-information)
- [8. 行程管理 (Process Management)](#8-行程管理-process-management)
- [9. 網路 (Networking)](#9-網路-networking)

---

## 1. 套件管理 (Package Management)

### `apt`
處理 Debian/Ubuntu 系統中軟體包的安裝、升級和移除。
```bash
apt [option] [package_name]
```
- `install [package]`：安裝軟體包。
- `update`：更新可用的軟體包列表。
- `upgrade`：升級所有已安裝的軟體包。
- `remove [package]`：移除軟體包。
- `purge [package]`：完全移除軟體包（包含設定檔）。

## 2. 檔案與目錄操作 (File & Directory Operations)

### `pwd`
顯示當前工作目錄的完整路徑。
```bash
pwd
```

### `ls`
列出目錄中的檔案與子目錄。
```bash
ls [options] [path]
```
- `-l`：使用詳細格式顯示。
- `-a`：顯示所有檔案，包含隱藏檔（以 `.` 開頭）。
- `-h`：以人類可讀的格式顯示檔案大小（如 KB, MB）。
- `-t`：按修改時間排序，最新的在前。

### `cd`
切換當前工作目錄。
```bash
cd [directory_path]
```
- `cd ~` 或 `cd`：切換到家目錄。
- `cd ..`：切換到上一層目錄。
- `cd -`：切換到前一個工作目錄。

### `mkdir`
建立新的目錄。
```bash
mkdir [options] [directory_name]
```
- `-p`：遞迴建立多層目錄（例如 `mkdir -p a/b/c`）。
- `-m 755`：建立目錄並同時設定權限。

### `rm`
刪除檔案或目錄。
```bash
rm [options] [file_or_directory]
```
- `-i`：刪除前進行詢問確認。
- `-f`：強制刪除，不進行任何提示。
- `-r`：遞迴刪除目錄及其所有內容（**請謹慎使用**）。

### `cp`
複製檔案或目錄。
```bash
cp [options] [source] [destination]
```
- `-r`：遞迴複製整個目錄。
- `-i`：如果目標已存在，在覆蓋前提示。
- `-u`：僅在來源檔案比目標檔案新時才複製。

### `mv`
移動或重新命名檔案、目錄。
```bash
mv [source] [destination]
```

## 3. 管道與重導向 (Piping & Redirection)
管道與重導向是 Linux Shell 的核心功能，能將多個指令組合起來，完成複雜的任務。

### 管道 `|`
將一個指令的「標準輸出 (stdout)」連接到另一個指令的「標準輸入 (stdin)」。簡單來說，就是把左邊指令的結果，交給右邊的指令處理。

**語法**: `command1 | command2`

**範例**:
```bash
# 查看目前系統所有行程，並從中篩選出包含 "nginx" 的行
ps aux | grep nginx

# 列出目前目錄的詳細資訊，並交由 less 分頁顯示
ls -l | less
```

### 輸出重導向 `>` 與 `>>`
將指令的輸出結果寫入檔案，而不是顯示在螢幕上。

**`>` (覆蓋)**: 將結果寫入檔案。如果檔案已存在，會**覆蓋**掉所有舊內容。如果檔案不存在，則會建立新檔案。

**語法**: `command > file.txt`

**範例**:
```bash
# 將目前目錄的列表寫入 files.txt，覆蓋舊有內容
ls -l > files.txt
```

**`>>` (附加)**: 將結果**附加**到檔案的末尾。如果檔案不存在，同樣會建立新檔案。

**語法**: `command >> file.txt`

**範例**:
```bash
# 將錯誤日誌附加到 system.log 檔案的末尾
cat error.log >> system.log
```

## 4. 檔案內容檢視與處理 (File Content & Processing)

### `less`
分頁顯示檔案內容，提供互動式瀏覽。
```bash
less [file_name]
```
- `q`：離開。
- `/keyword`：向下搜尋關鍵字。
- `n` / `N`：跳至下一個/上一個搜尋結果。
- `g` / `G`：跳至檔案開頭/結尾。

### `tail`
顯示檔案的最後幾行。
```bash
tail [options] [file_name]
```
- `-n k`：顯示最後 k 行（預設為 10）。
- `-f`：持續監控檔案的新增內容，常用於查看日誌 (log)。

### `grep`
在檔案中搜尋符合指定模式的文字行。
```bash
grep [options] 'pattern' [file_name]
```
- `-i`：忽略大小寫。
- `-v`：反向搜尋，顯示不符合模式的行。
- `-r` 或 `-R`：遞迴搜尋目錄下的所有檔案。
- `-n`：顯示符合行的行號。
- `-w`：只尋找完全符合的單字。
- `-l`：只列出包含符合模式的檔名，不顯示內容。
- `-E`：使用擴充正規表示式 (E-grep)。
- `-C k`：顯示符合行的前後 k 行內容 (Context)。

## 5. 搜尋檔案與指令 (Searching Files & Commands)

### `find`
在檔案系統中搜尋檔案或目錄。
```bash
find [path] [expressions]
```
- `-name 'pattern'`：根據檔名搜尋（例如 `'*.log'`）。
- `-type d`：只搜尋目錄。
- `-type f`：只搜尋檔案。
- `-mtime -7`：搜尋 7 天內被修改過的檔案。
- `-size +10M`：搜尋大於 10MB 的檔案。
- `-exec command {} \;`：對每個搜尋結果執行指定的指令。

### `whereis`
查找指令的可執行檔、原始碼、說明文件的位置。
```bash
whereis [command_name]
```

## 6. 權限與擁有者 (Permissions & Ownership)

### `chmod`
變更檔案或目錄的權限。
```bash
chmod [mode] [file_or_directory]
```
- `u` (user), `g` (group), `o` (others), `a` (all)
- `+` (新增權限), `-` (移除權限), `=` (設定權限)
- `r` (讀=4), `w` (寫=2), `x` (執行=1)
- **範例**: `chmod 755 script.sh` (擁有者可讀寫執行，群組和其他人可讀可執行)。
- `-R`：遞迴變更目錄及其內容的權限。

### `chown`
變更檔案或目錄的擁有者與群組。
```bash
chown [user]:[group] [file_or_directory]
```
- `-R`：遞迴變更目錄及其內容的擁有者。

## 7. 系統資訊 (System Information)

### `df`
顯示磁碟空間使用情況。
```bash
df [options]
```
- `-h`：以人類可讀的格式顯示（GB, MB）。

### `du`
顯示目錄或檔案所佔用的磁碟空間大小。
```bash
du [options] [path]
```
- `-h`：以人類可讀的格式顯示。
- `-s`：只顯示總計大小。
- `--max-depth=1`：只顯示第一層目錄的大小。

### `free`
顯示系統記憶體（RAM）的使用情況。
```bash
free [options]
```
- `-h`：以人類可讀的格式顯示。

### `uname`
顯示系統核心與作業系統資訊。
```bash
uname [options]
```
- `-a`：顯示所有詳細資訊。

### `whoami`
顯示當前登入的使用者名稱。
```bash
whoami
```

### `who`
顯示目前登入系統的使用者列表。
```bash
who
```

### `hostname`
顯示或設定系統的主機名稱。
```bash
hostname
```

## 8. 行程管理 (Process Management)

### `top`
動態即時顯示系統的行程狀態。
```bash
top
```
- `P`：依 CPU 使用率排序。
- `M`：依記憶體使用量排序。
- `k`：輸入 PID 來終止行程。
- `q`：離開。

### `ps`
顯示當前系統的行程快照（靜態）。
```bash
ps [options]
```
- `aux`：顯示所有使用者的所有行程（詳細格式）。
- `ef`：顯示所有行程（標準格式）。

### `kill`
傳送訊號給指定的行程，通常用來終止行程。
```bash
kill [signal] [PID]
```
- `-9`：強制終止行程 (SIGKILL)。
- `-15`：正常終止行程 (SIGTERM，預設)。

### `crontab`
管理定時執行的任務排程。
```bash
crontab [options]
```
- `-e`：編輯當前使用者的 crontab。
- `-l`：列出當前使用者的 crontab。

## 9. 網路 (Networking)

### `ping`
測試與目標主機的網路連線狀態。
```bash
ping [host_or_ip]
```

### `telnet`
測試遠端主機的特定埠號是否開啟。
```bash
telnet [host] [port]
```

### `ssh`
以加密方式遠端登入另一台主機。
```bash
ssh [user]@[host]
```
- `-p [port]`：指定連線的埠號。
- `-i [key_file]`：指定用於驗證的私鑰檔案。

### `scp`
在本地與遠端主機之間安全地複製檔案。
```bash
scp [options] [source] [destination]
```
- `-r`：遞迴複製整個目錄。
- `-P [port]`：指定遠端主機的 SSH 埠號（注意是大寫 P）。

### `curl`
強大的 URL 傳輸工具，可用於發送 HTTP 請求。
```bash
curl [options] [URL]
```
- `-X POST`：指定請求方法為 POST。
- `-d 'data'`：傳送 POST 請求的資料。
- `-H 'Header: Value'`：自訂請求標頭。
- `-i`：在輸出中包含 HTTP 回應標頭。
- `-L`：自動跟隨 HTTP 轉址 (Redirection)。

### `host`
查詢 DNS 資訊。
```bash
host [domain_name]
```
