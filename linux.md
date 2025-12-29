## 索引目錄

- [1. 套件管理 (Package Management)](#1-套件管理-package-management)
- [2. 檔案與目錄操作 (File & Directory Operations)](#2-檔案與目錄操作-file--directory-operations)
- [3. 管道與重導向 (Piping & Redirection)](#3-管道與重導向-piping--redirection)
- [4. 檔案內容檢視與處理 (File Content & Processing)](#4-檔案內容檢視與處理-file-content--processing)
- [5. 搜尋檔案與指令 (Searching Files & Commands)](#5-搜尋檔案與指令-searching-files--commands)
- [6. 權限與擁有者 (Permissions & Ownership)](#6-權限與擁有者-permissions--ownership)

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