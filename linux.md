- [Ubuntu 安裝與管理套件](#Ubuntu-安裝與管理套件)
- [檔案系統 File system](#檔案系統-File-system)
- [程式 Processes](#程式-Processes)
- [使用者環境 User environment](#使用者環境-User-environment)
- [文字編輯 Text processing](#文字編輯-Text-processing)
- [殼層內建 Shell builtins](#殼層內建-Shell-builtins)
- [搜尋 Searching](#搜尋-Searching)
- [網路 Network](#網路-Network)
- [雜項 Miscellaneous](#雜項-Miscellaneous)

## Ubuntu 安裝與管理套件
```
apt [option] [package]  處理軟體包的安裝、升級和移除
```
- install [package]  安裝軟體
- update  更新軟體
- upgrade  升級所有安裝軟體
- remove [package]  刪除軟體
- purge [package]  完全移除軟體包（包含設定檔）
---

## 檔案系統 File system
```
pwd [選項]  將當前工作目錄的完整路徑
```
---

```
ls [選項] [目錄或檔案]  列出目前目錄檔案
```
- -l  以詳細格式顯示（包含權限、大小、修改時間等）
- -h  詳細格式且檔案大小人類可讀（KB/MB）
---

```
mkdir [選項] [目錄名稱]  建立新的資料夾（目錄）
```
- -p a/b/c  遞迴建立多層資料夾（如果 a 或 b 不存在也會自動建立）
- -m 755 folder  建立資料夾並設定權限（如 755）
---

```
rm [選項] [檔案或資料夾名稱]  刪除檔案或目錄（資料夾）
```
- -i  刪除前詢問確認
- -f  強制刪除，不詢問、不顯示錯誤
- -r  遞迴刪除資料夾及其內容（小心使用）
- -rf  強制刪除整個資料夾及內容，最危險但常用
---

```
cp [選項] [原始路徑] [目標路徑]  將檔案或資料夾從一個位置複製到另一個位置
```
- -i  複製時如目標檔案存在，會提示是否覆蓋
- -r  遞迴複製資料夾含內容到目標路徑
- -u  僅在原始檔案較新時才覆蓋目標檔案
---

```
mv [選項] [原始名稱] [目標名稱] 移動或重新命名，檔案或資料夾
```
- -i  移動前詢問是否覆蓋現有檔案
- -u  只有當來源檔案較新時才會覆蓋目標檔案
---

```
chmod [選項] [模式] [目錄或檔案]  變更檔案或目錄權限
```
```
[擁有者][群組][其他人]  →  r: 讀  w: 寫  x: 執行
```
|  數字  |  模式  |  說明
|  --  |  ---  |  ------
|  4  | r | 讀
|  2  | w | 寫
|  1  | x | 執行

- -R  對目錄及子目錄加權限
- \+  加上權限 (ex: a+r 給 fil 的所有使用者增加讀權限)
- \-  移除權限 (ex: g-x 刪除 file 的群組執行權限)
- =  指定為某權限
- u  擁有者（user）
- g  群組（group）
- o  其他人（others）
- a  所有人（all）
---

```
chown [選項] 使用者[:群組] [檔案或目錄]  變更檔案或資料夾的擁有者
```
- -R  目錄與子目錄所有內容都變更
---

```
df [選項] [目錄]  顯示系統硬碟使用狀況
```
- -h  詳細格式且檔案大小人類可讀（KB/MB）
---

```
du  顯示目錄硬碟使用狀況
```
- -h  以「人類易讀」格式顯示（KB、MB、GB)
- --max-depth=1  僅列出目錄第一層的大小
---

```
free  顯示記憶體使用狀況
```
- -h  以「人類易讀」格式顯示（KB、MB、GB)
---

```
du  顯示目錄硬碟使用狀況
```
- -h  以「人類易讀」格式顯示（KB、MB、GB)
- --max-depth=1  僅列出目錄第一層的大小
---

```
free  顯示記憶體使用狀況
```
- -h  以「人類易讀」格式顯示（KB、MB、GB)
---

## 程式 Processes
```
top [選項]  顯示系統Process(動態)
```
|  鍵盤操作  |  功能說明
|  :--:  |  :--:
|  P  |  依 CPU 使用率排序（預設）
|  M  |  依記憶體使用量排序
|  T  |  依執行時間排序
|  k  |  終止程序（會要求輸入 PID）
|  q  |  離開 top
|  c  |  顯示/隱藏完整命令列路徑
---

```
ps [選項]  顯示當前Process信息(靜態)
```
- -e  顯示系統中所有程序
- -ef  顯示所有程序（完整格式）
- -aux  顯示所有使用者程序（BSD 風格）
---

```
crontab [選項]  系統中的定時任務排程工具
```
```
* * * * * /usr/bin/php /var/www/html/index.php
```
- -e  編輯 crontab 文件
- -l  目前用戶的 cron 任務

|  設定  |  說明
|  :--:  |  :--:
|  *  |  每一個可能的值（例如：* * * * * 表示每分鐘都執行）
|  * / n  |  每 n 個時間單位執行一次（例如：*/5 * * * * 表示每 5 分鐘執行一次）
|  n,m  |  在指定的時間點執行（例如：0,30 * * * * 表示在每小時的第 0 分鐘和第 30 分鐘執行）
|  n-m  |  在指定範圍內的時間點執行（例如：1-5 * * * * 表示從 1 分鐘到 5 分鐘都會執行）

|  星號位置  |  說明
|  :--:  |  :--:
|  1  |  分鐘 (0 - 59)
|  2  |  小時 (0 - 23)
|  3  |  日期 (1 - 31)
|  4  |  月份 (1 - 12)
|  5  |  星期幾 (0 - 6，其中 0 是星期日)
---

```
kill [選項] <PID>  終止進程
```
- -15  中止一個進程(預設)
- -9  強制中止
- -19  暫停（可恢復）
- -18  續已暫停的進程
- -2  中斷（Ctrl+C）
---

## 使用者環境 User environment
```
uname  顯示系統資訊
```
- -a  顯示所有可用的系統資訊
- -n  顯示主機名稱
---

```
clear  除終端機螢幕上的顯示內容
``` 
---

```
whoami  顯示當前登入使用者的名稱
```
---

```
who  顯示目前有哪些登入系統的使用者資訊
```
- -a 顯示更詳細的登入資訊
---

## 文字編輯 Text processing
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
- -n k filename 顯示最後 k 行
- -f filename 持續監控檔案變化（像 log 檔）
- -F filename 類似 -f，但檔案被移動或重建時會自動追蹤
- -c k filename 顯示最後 k 個位元組（字元）
- -q file1 file2 同時查看多檔，不顯示檔名標題
- -v file1 file2 同時查看多檔，強制顯示檔名標題
---

## 殼層內建 Shell builtins
```
cd [目錄路徑]  切換當前工作目錄
```
- .. 回到上一層目錄
- ../.. 回到上上層目錄
- /path/to/dir 切換到指定的絕對路徑
- dir_name 切換到相對路徑中的資料夾
---

## 搜尋 Searching
```
grep [選項] '搜尋模式' [檔案名稱]  檔案中搜尋並列出符合指定模式 (檔案名稱可搭配 pattern、zgrep 用於 .gz 壓縮檔案中的搜尋)
```
- 'pattern' filename  在 filename 中搜尋 pattern（不區分大小寫）
- -v  排除不符合 pattern 的行（反向搜尋）
- -r 'pattern' dir/  遞歸搜尋目錄中的檔案
- -l 'pattern' filename  顯示包含 pattern 的檔案名（不顯示具體內容）
- -n 'pattern' filename  顯示符合 pattern 的行及其行號
- -c 'pattern' filename  顯示符合 pattern 的行數
- -o 'pattern' filename  只顯示符合的文字，並不顯示整行
- -H 'pattern' filename  顯示符合 pattern 的行及其檔案名
- -w 'pattern' filename  精確匹配整個字詞，而不僅是包含該字詞的行
- -E 'pattern' filename  支援擴展正規表達式（grep 預設使用基本正規表達式）
- -A k 'pattern' filename  顯示匹配行及其後 k 行
- -B k 'pattern' filename  顯示匹配行及其前 k 行
- -C k 'pattern' filename  顯示匹配行及其前後 k 行（上下文行）
- --color=auto  顏色突顯符合的關鍵字
- --include="*.txt"  搜尋特定類型檔案
---

```
whereis [程式名稱]  查找可執行檔、原始碼、說明文件（man page）的位置
```
---

```
find [搜尋路徑] [條件] [動作]  在檔案系統中搜尋檔案或目錄
```
- -name  比對檔名（大小寫敏感）
- -path  比對完整路徑
- -regex  用正規表達式比對完整路徑
- -type f  普通檔案
- -type d  目錄
---

## 網路 Network
```
ping [目標位址]  測試網路連線狀態
```
---

```
telnet [主機位址] [port]  測試遠端主機的特定埠口 (port)
```
---

```
ssh [使用者名稱]@[主機位址]  遠端登入其他主機
```
- -p [port]  指定連接的 port
- -v  顯示詳細連線過程（debug 用）
- -i [keyfile]  指定私鑰檔案來驗證身份（如 .pem）
---

```
scp [選項] [帳號@來源主機]:[來源路徑] [帳號@目的主機]:[目的地路徑]  本機與遠端伺服器之間 安全地複製檔案
``` 
- -r  遞迴複製資料夾
- -P  指定 SSH port（注意是大寫）
- -v  顯示詳細連線過程（debug 用）
- -i [keyfile]  指定私鑰檔案來驗證身份（如 .pem）
---

```
curl [options] [URL]  用於與 URL 通訊，支援多種協定（HTTP、HTTPS、FTP、SFTP、SMTP...）
```
- -X  指定 HTTP 方法（GET、POST、PUT、DELETE 等）
- -d  傳送資料（POST、PUT）
- -H  自訂 HTTP headers
- -o  將回應寫入檔案
- -v  顯示詳細請求/回應細節（Verbose）
---

```
host [選項] [主機名稱或IP]  查詢 DNS（Domain Name System）資訊的命令
```
---

```
hostname  顯示或設定系統主機名稱
```
---

## 雜項 Miscellaneous
```
顯示系統運行的服務狀態
service --status-all

Windows 進入wsl2
explorer.exe . #或者在windows資料夾路徑改\\wsl$\Ubuntu

啟用apache mod_rewrite 模組(/etc/apache2/apache2.conf改AllowOverride All)
a2enmod rewrite

查詢指令說明手冊
man  ex: man cp
```
