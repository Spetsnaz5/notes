## 基礎
```
建立新的本地端 Repository
git init

複製遠端的 Repository 檔案到本地端
git clone [Repository URL]

與遠端倉庫建立連接
git remote add [Repository URL]

檢查本地端檔案異動狀態
git status

查看先前的 commit 記錄
git log

查看HEAD變更記錄
git reflog

顯示所有標籤
git tag

還原未提交的更改
git restore [檔案或資料夾]

暫存區移除
git restore --staged
```

## add
```
將所有檔案或資料夾加入版本控制
git add .

將指定的檔案或資料夾加入版本控制
git add [檔案或資料夾]
``` 

## stash
```
暫存更改
git stash

暫存並附加訊息
git stash save "message"

列出暫存更改
git stash list

取回暫存，不刪除 stash
git stash apply

取回指定 stash，不刪除 stash
git stash apply stash@{2}

恢復暫存更改並刪除
git stash pop

刪除指定 stash
git stash drop stash@{0}

清除所有暫存條目
git stash clear
``` 

## reset
```
將所有檔案或資料夾移出版本控制
git reset

將指定的檔案或資料夾移出版本控制
git reset [檔案或資料夾]

只重置 HEAD，保留暫存區和工作目錄中的更改
git reset --soft

重置 HEAD 和暫存區，保留工作目錄中的更改（預設行為）
git reset --mixed

完全重置 HEAD、暫存區和工作目錄，丟失未提交的更改
git reset --hard

強制恢復到指定的 commit（透過 Hash 值）
git reset --hard [HASH]
```

## fetch
```
獲取遠端 Repository 所有 branch 更新
git fetch

獲取指定遠端 Repository 所有 branch 更新
git fetch <remote-name>

獲取指定遠端 Repository 特定 branch 更新
git fetch <remote-name> <branch-name>
```

## commit
```
提交目前的異動
git commit

提交目前的異動並設定摘要說明
git commit -m "提交說明內容"
``` 

## branch
```
顯示分支
git branch

建立分支
git branch <branch-name>

刪除本地分支
git branch -d <branch-name>

强制删除本地分支
git branch -D <branch-name>

-a  #列出所有分支，包含本地與遠端
-r  #列出遠端
-m <old-branch-name> <new-branch-name>  #修改分支名稱
--no-merged  #顯示尚未合併當前分支的所有分支
```

## checkout
```
切換至該分支
git checkout <branch-name>

建立並切換至該分支
git checkout -b <branch-name>

強制切換至該 commit
git checkout -f <hash>

切換至該 commit
git checkout <hash>
```

## pull
```
遠端Repository拉取並合併至當前分支(git fetch和git merge的合併)
git pull

指定遠端Repository拉取並合併至當前分支
git pull <remote-name> <branch>
```

## push
```
發佈至遠端分支
git push

發佈至指定的遠端分支
git push <remote-name> <branch-name>

強推至指定的遠端分支
git push --force <remote-name> <branch-name>

安全地推送本地分支到遠端，避免覆蓋他人提交
git push --force-with-lease <remote-name> <branch-name>

發佈所有至指定的遠端
git push --all <remote-name>

刪除遠端分支
git push <remote-name> --delete <branch-name>

發佈本地指定分支到遠端分支
git push <remote-name> <local-branch-name>:<remote-branch-name>
```

## merge
```
合併指定分支至當前分支
git merge <branch-name>
```

## reabse
```
當前分支轉移指定分支上
git rebase <branch-name>

rebase出現衝突，需要手動解决衝突後繼續rebase
git rebase --continue

中止 rebase
git rebase --abort

交互式 rebase (重新排序提交、合并提交、修改提交消息)
git rebase -i <commit>
```
