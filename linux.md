## 檔案和目錄操作
```
ls [選項] [目錄或檔案]  列出目前目錄檔案
```
- -l 以詳細格式顯示（包含權限、大小、修改時間等）
- -h	詳細格式且檔案大小人類可讀（KB/MB）
- /path/to/dir	查看特定目錄內容
---

```
cd [目錄路徑]  切換當前工作目錄
```
- .. 回到上一層目錄
- ../.. 回到上上層目錄
- /path/to/dir	切換到指定的絕對路徑
- dir_name	切換到相對路徑中的資料夾
---

```
mkdir [選項] [目錄名稱]  建立新的資料夾（目錄）
```
- new_folder	建立一個名為 new_folder 的資料夾
- folder1 folder2	一次建立多個資料夾
- -p a/b/c	遞迴建立多層資料夾（如果 a 或 b 不存在也會自動建立）
- -m 755 folder	建立資料夾並設定權限（如 755）
---

```
rm [選項] [檔案或資料夾名稱]  刪除檔案或目錄（資料夾）
```
- filename 刪除 filename 檔案
- filename filename2 同時刪除多個檔案
- -i 刪除前詢問確認
- -f 強制刪除，不詢問、不顯示錯誤
- -r folder/	遞迴刪除資料夾及其內容（小心使用）
- -rf folder/	強制刪除整個資料夾及內容，最危險但常用
---

```
cp [選項] [原始路徑] [目標路徑]  將檔案或資料夾從一個位置複製到另一個位置
```
- file backup 複製 file 為 backup
- file /home/user/	將 file 複製到 /home/user/ 資料夾
- -i file backup	複製時如目標檔案存在，會提示是否覆蓋
- -r folder1/ folder2/	遞迴複製資料夾 folder1（含內容）到 folder2/
- -u file backup	僅在原始檔案較新時才覆蓋目標檔案
---

```
mv [選項] [原始名稱] [目標名稱] 移動或重新命名，檔案或資料夾
```
- file /home/user/  將 file 移動到 /home/user/ 資料夾
- oldname newname	將檔案重新命名 oldname => newname
- folder1/ folder2/	將 folder1 移動到 folder2 裡面（若存在）
- -i file backup	移動前詢問是否覆蓋現有檔案
- -u file backup	只有當來源檔案較新時才會覆蓋目標檔案
---

## 檔案內容處理
```
less [檔案名稱]  分頁顯示檔案內容
```
|  鍵盤操作  |  功能說明
|  :--:  |  :--:
|  ↑ / ↓ 或 k / j  |  上/下移動一行
|  Space 或 f  |  向下翻一頁
|  n / N  |  搜尋下一個 / 上一個出現處
|  /關鍵字  |  向下搜尋（按 n 跳下一個，N 上一個）
|  /關鍵字  |  向下搜尋（按 n 跳下一個，N 上一個）
|  ?關鍵字  |  向上搜尋（按 n 跳下一個，N 上一個）
|  g  |  跳到檔案最上面
|  G  |  跳到檔案最下面
|  q  |  離開 less
|  v  |  呼叫預設編輯器（通常是 vi）編輯目前檔案
|  &pattern  |  僅顯示符合 pattern 的行（類似 grep 篩選）
|  h  |  顯示 help 說明畫面
|  &pattern  |  僅顯示符合 pattern 的行（類似 grep 篩選）
|	-N  |  顯示行號（執行 less -N filename）
---

```
tail [選項] [檔案名稱]  看檔案最後幾行內容
```
- filename 顯示檔案最後 10 行（預設）
- -n k filename	顯示最後 k 行
- -f filename	持續監控檔案變化（像 log 檔）
- -F filename	類似 -f，但檔案被移動或重建時會自動追蹤
- -c k filename	顯示最後 k 個位元組（字元）
- -q file1 file2	同時查看多檔，不顯示檔名標題
- -v file1 file2	同時查看多檔，強制顯示檔名標題
---

```
grep [選項] '搜尋模式' [檔案名稱]  檔案中搜尋並列出符合指定模式 (檔案名稱可搭配 pattern) (zgrep	用於 .gz 壓縮檔案中的搜尋)
```
- 'pattern' filename	在 filename 中搜尋 pattern（不區分大小寫）
- -v 排除不符合 pattern 的行（反向搜尋）
- -r 'pattern' dir/	遞歸搜尋目錄中的檔案
- -l 'pattern' filename	顯示包含 pattern 的檔案名（不顯示具體內容）
- -n 'pattern' filename	顯示符合 pattern 的行及其行號
- -c 'pattern' filename	顯示符合 pattern 的行數
- -o 'pattern' filename	只顯示符合的文字，並不顯示整行
- -H 'pattern' filename	顯示符合 pattern 的行及其檔案名
- -w 'pattern' filename	精確匹配整個字詞，而不僅是包含該字詞的行
- -E 'pattern' filename	支援擴展正規表達式（grep 預設使用基本正規表達式）
- -A 3 'pattern' filename	顯示匹配行及其後 3 行
- -B 3 'pattern' filename	顯示匹配行及其前 3 行
- -C 3 'pattern' filename	顯示匹配行及其前後 3 行（上下文行）
- --color=auto 顏色突顯符合的關鍵字
- --include="*.txt" 搜尋特定類型檔案
---










grep -rnw --include="*.php" 877 /var/www/html | grep -v 'vendor'
zgrep

-n  #顯示匹配行的行號 
-r  #遞迴搜尋目錄 
-v  #反向匹配，顯示不包含匹配模式的行 

--color  #高亮顯示匹配模式
-c  #顯示匹配行的計數 
-e  #指定多個搜索模式 grep -e "cat" -e "dog" file.txt
-E  #啟用擴展正規表示式
-A num  #顯示匹配行及其後的 num 行
-B num  #顯示匹配行及其前的 num 行
```

## 系統資訊
```
顯示系統Process(動態)
top

顯示當前Process信息(靜態)
ps
ps aux  # 顯示所有Process信息

顯示系統硬碟空間使用狀況
df
df -h  # 轉換空間單位

顯示目錄硬碟使用狀況
du
du -h  # 轉換空間單位

顯示系統記憶體使用狀況
free
free -h  # 轉換空間單位

```

## 檔案權限與擁有權
```
變更檔案權限
chmod 755 file

變更檔案擁有人
chown user:group file

user | group | other
r: 4 讀
w: 2 寫
x: 1 執行

```

## 網路相關
```
測試網路連接
ping example.com

使用ssh連至遠端主機
ssh user@host -p port

```

## 安裝與管理 Ubuntu
```
sudo apt-get update  # 更新軟體
sudo apt-get upgrade  # 升級所有安裝軟體
sudo apt-get install package_name  # 安裝軟體
sudo apt-get remove package_name  # 刪除軟體

```

## 其他
```
顯示當前目錄
pwd 

查詢版本
uname -a

查詢特定工具位置
whereis <name>

顯示系統運行的服務狀態
service --status-all

Windows 進入wsl2
explorer.exe . #或者在windows資料夾路徑改\\wsl$\Ubuntu

啟用apache mod_rewrite 模組(/etc/apache2/apache2.conf改AllowOverride All)
a2enmod rewrite

echo	顯示字串或寫入檔案	echo "hello" > hi.txt
man	查詢指令說明手冊	man cp
which / whereis	找出執行檔路徑	which php
clear	清除終端機畫面	clear
history	顯示輸入過的指令記錄	history
```
