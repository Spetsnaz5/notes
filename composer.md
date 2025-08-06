```
# 查詢版本
composer --version

# 初始化專案
composer init
php composer.phar init

# 安裝特定套件
composer require <vendor/package>

# 正式環境部署：跳過開發工具，減少依賴，提升效能、安全性
composer require phpunit/phpunit --no-dev

# 限制套件版本更新範圍（鎖定版本） ^2.0: 接受 2.x 版本的更新，但不會升級到 3.x。
composer require monolog/monolog:^2.0

# 安裝指定版本套件
composer require guzzlehttp/guzzle:7.0.1

# 更新所有套件
composer update

# 更新 require 套件
composer update --no-dev

# 更新特定套件
composer update <vendor/package>

# 移除套件
composer remove <vendor/package>

# 重新產生 autoload 檔案
composer dump-autoload

# 顯示已安裝的所有套件
composer show

# 檢查有哪些套件有新版本
composer outdated

# 建立新專案並安裝套件，常用於框架專案（例如 Laravel）
composer create-project <vendor/package>

# 檢查 composer.json 格式是否正確，避免語法錯誤
composer validate

```

```
composer.json 文件範例

{
    "name": "myproject/app",
    "description": "A simple PHP project using Composer",
    "require": {
        "guzzlehttp/guzzle": "^7.0"
    },
    "require-dev": {
        "phpunit/phpunit": "^9.0"
    },
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    }
}

require: 正式環境需要的套件。
require-dev: 開發環境需要的套件。
autoload: 定義自動加載的命名空間。
```
