## 索引目錄

- [1. 套件管理 (Package Management)](#1-套件管理-package-management)
- [2. 檔案與目錄操作 (File & Directory Operations)](#2-檔案與目錄操作-file--directory-operations)
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
