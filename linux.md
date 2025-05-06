### 檔案和目錄操作
```
ls [選項] [目錄或檔案] 
```
- -l 以詳細格式顯示（包含權限、大小、修改時間等）
- -h	詳細格式且檔案大小人類可讀（KB/MB）
- /path/to/dir	查看特定目錄內容

```
cd [目錄路徑]
```
- .. 回到上一層目錄
- ../.. 回到上上層目錄
- /path/to/dir	切換到指定的絕對路徑
- dir_name	切換到相對路徑中的資料夾

```
mkdir [選項] 目錄名稱
```
- new_folder	建立一個名為 new_folder 的資料夾
- folder1 folder2	一次建立多個資料夾
- -p a/b/c	遞迴建立多層資料夾（如果 a 或 b 不存在也會自動建立）
- -m 755 folder	建立資料夾並設定權限（如 755）


mkdir 
mkdir 
mkdir 
mkdir -v folder	顯示建立過程（verbose 模式）
mkdir 








建立目錄
mkdir directory
mkdir -p parent-directory/new-directory    #遞迴建立

建立檔案
cat > example.txt

刪除檔案或目錄
rm file
rm -r directory    # 遞迴刪除目錄
rm -f file         # 強制刪除

複製檔案或目錄
cp source_file destination
cp -r source_directory destination_directory   # 遞迴複製目錄

移動或重新命名檔案或目錄
mv old_name new_name
mv file /new/path

顯示當前目錄
pwd
```

## 檔案內容處理
```
分頁顯示檔案內容
less file

持續輸出檔案最後幾行內容
tail -n 10 file

-n k  #顯示最後k行
-f  #持續輸出檔案內容

搜尋檔案或輸出內容
grep 'abc' file
grep -rnw --include="*.php" 877 /var/www/html | grep -v 'vendor'
zgrep

-n  #顯示匹配行的行號 
-r  #遞迴搜尋目錄 
-v  #反向匹配，顯示不包含匹配模式的行 
--include="*.txt"  #搜尋特定類型檔案
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

```
