# Git Command Cheatsheet

## 目錄
- [1. Setup and Basics (設定與基礎)](#1-setup-and-basics-設定與基礎)
- [2. Everyday Commands (日常指令)](#2-everyday-commands-日常指令)

## 1. Setup and Basics (設定與基礎)

### `git init`
建立新的本地端 Repository。
```bash
git init
```

### `git clone`
複製遠端的 Repository 檔案到本地端。
```bash
git clone [Repository URL]
```

### `git remote`
與遠端倉庫建立連接。
```bash
# 新增遠端
git remote add <remote-name> <Repository URL>

# 查看遠端
git remote -v
```

## 2. Everyday Commands (日常指令)

### `git status`
檢查本地端檔案異動狀態。
```bash
git status
```

### `git add`
將檔案加入暫存區 (Staging Area)。
```bash
# 將所有變更的檔案加入
git add .

# 將指定的檔案或資料夾加入
git add [檔案或資料夾]
```

### `git commit`
將暫存區的內容建立一個新的 commit。
```bash
# 開啟編輯器輸入 commit 訊息
git commit

# 直接在指令中加入 commit 訊息
git commit -m "你的 commit 訊息"
```
