# Git Command Cheatsheet

## 目錄
- [1. Setup and Basics (設定與基礎)](#1-setup-and-basics-設定與基礎)
- [2. Everyday Commands (日常指令)](#2-everyday-commands-日常指令)
- [3. Working with Remotes (遠端協作)](#3-working-with-remotes-遠端協作)
- [4. Branching and Merging (分支與合併)](#4-branching-and-merging-分支與合併)

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

## 3. Working with Remotes (遠端協作)

### `git fetch`
從遠端 Repository 下載最新的 commit，但**不會**自動合併。
```bash
# 獲取預設遠端 (origin) 的所有分支更新
git fetch

# 獲取指定遠端的所有分支更新
git fetch <remote-name>

# 獲取指定遠端的特定分支更新
git fetch <remote-name> <branch-name>
```

### `git pull`
從遠端 Repository 拉取最新的 commit 並**自動合併**至當前分支 (相當於 `git fetch` + `git merge`)。
```bash
# 拉取並合併預設遠端 (origin) 的當前分支
git pull

# 拉取並合併指定遠端的特定分支
git pull <remote-name> <branch-name>
```

### `git push`
將本地的 commit 推送到遠端 Repository。
```bash
# 推送當前分支至預設遠端 (origin)
git push

# 推送至指定的遠端分支
git push <remote-name> <branch-name>

# 強制推送 (會覆蓋遠端歷史，請謹慎使用)
git push --force <remote-name> <branch-name>

# 更安全的強制推送，如果遠端有新的 commit 則會失敗
git push --force-with-lease <remote-name> <branch-name>

# 推送所有本地分支
git push --all <remote-name>

# 刪除遠端分支
git push <remote-name> --delete <branch-name>
```

## 4. Branching and Merging (分支與合併)

### `git branch`
管理分支。
```bash
# 顯示所有本地分支
git branch

# 顯示所有本地與遠端分支
git branch -a

# 建立新分支
git branch <branch-name>

# 刪除本地分支
git branch -d <branch-name>

# 強制刪除本地分支
git branch -D <branch-name>

# 重新命名分支
git branch -m <old-branch-name> <new-branch-name>
```

### `git checkout`
切換分支或還原工作區的檔案。
```bash
# 切換至指定分支
git checkout <branch-name>

# 建立並立即切換至新分支
git checkout -b <branch-name>

# 切換至某個 commit (會進入 detached HEAD 狀態)
git checkout <commit-hash>
```

### `git merge`
將指定分支的變更合併到當前分支。
```bash
git merge <branch-name>
```

### `git cherry-pick <commit-hash>`
將指定的 commit 複製到當前分支。
```bash
git cherry-pick <commit-hash>
```

### `git rebase <branch-name>`
將當前分支的 commit "重新"接到另一個分支的頂端。
```bash
git rebase <branch-name>
```

### `git rebase -i <commit-hash>`
互動式 rebase，可以修改、合併、重新排序 commit。
```bash
git rebase -i <commit-hash>
```

### rebase 衝突處理
當 rebase 發生衝突時，手動解決檔案衝突後，使用以下指令：
```bash
# 將解決衝突的檔案加入暫存區
git add .

# 繼續 rebase
git rebase --continue

# 或選擇中止 rebase，回到 rebase 前的狀態
git rebase --abort
```
