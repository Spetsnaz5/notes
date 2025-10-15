## 索引目錄

- [專案初始化與設定](#專案初始化與設定)
- [管理依賴套件](#管理依賴套件)
- [檢視與檢查](#檢視與檢查)
- [自動載入與效能](#自動載入與效能)
- [其他常用指令](#其他常用指令)

---

## 專案初始化與設定

Composer 的核心是 `composer.json` 檔案，它定義了專案的所有依賴、版本、自動載入規則等元數據。

### `init`
以互動式問答的方式，在當前目錄下建立一個新的 `composer.json` 檔案。
```bash
composer init
```

### `composer.json` 檔案詳解

這是一個 `composer.json` 的完整範例，涵蓋了最常用的欄位。

```json
{
    "name": "myvendor/myproject",
    "description": "A sample PHP project",
    "type": "project",
    "license": "MIT",
    "version": "1.0.0",
    "require": {
        "php": "^8.1",
        "guzzlehttp/guzzle": "^7.0",
        "monolog/monolog": "^2.0"
    },
    "require-dev": {
        "phpunit/phpunit": "^10.0",
        "fakerphp/faker": "^1.9"
    },
    "autoload": {
        "psr-4": {
            "App\": "src/"
        },
        "files": [
            "helpers.php"
        ]
    },
    "autoload-dev": {
        "psr-4": {
            "Tests\": "tests/"
        }
    },
    "scripts": {
        "test": "phpunit",
        "post-install-cmd": [
            "@php artisan key:generate"
        ]
    },
    "config": {
        "optimize-autoloader": true,
        "sort-packages": true
    }
}
```

- `name`: 專案名稱 (格式為 `vendor/package`)。
- `description`: 專案的簡短描述。
- `require`: **正式環境**需要的套件與版本約束。
- `require-dev`: **開發環境**才需要的套件（例如測試工具）。
- `autoload`: 設定 [PSR-4](https://www.php-fig.org/psr/psr-4/) 命名空間與目錄的對應，這是實現自動載入的關鍵。
- `scripts`: 定義可以透過 `composer run-script` 執行的自定義指令，或在特定事件（如 `post-install-cmd`）後自動觸發的指令。
- `config`: 用於調整 Composer 的行為，例如 `optimize-autoloader` 用於提升效能。

---

## 管理依賴套件

### `require`
新增一個新的套件到 `composer.json` 的 `require` 區塊，並立即安裝它。
```bash
composer require <vendor/package>:<version>
```
- **版本約束**:
  - `^2.0`: 接受 `2.x` 版本的更新，但不升級到 `3.0` (推薦)。
  - `~2.0.1`: 接受 `2.0.x` 的更新，但不升級到 `2.1`。
  - `7.0.1`: 精確鎖定版本。
- `--dev`: 將套件加入到 `require-dev` 區塊。

### `install`
根據 `composer.lock` 檔案安裝所有依賴套件。如果 `composer.lock` 不存在，則會讀取 `composer.json` 並在安裝後建立 `composer.lock`。
```bash
composer install
```
- `--no-dev`: 在正式環境部署時使用，跳過 `require-dev` 中的開發套件。
- **核心觀念**: `composer.lock` 檔案鎖定了所有套件的精確版本，確保團隊中每個成員和伺服器上安裝的都是完全相同的版本，避免「在我電腦上可以跑」的問題。

### `update`
根據 `composer.json` 中定義的版本約束，將套件更新到最新的相容版本，並**重新產生** `composer.lock` 檔案。

更新所有套件
```bash
composer update
```

只更新特定的套件
```bash
composer update <vendor/package>
```
- `--no-dev`: 更新時，排除 `require-dev` 的套件。

### `remove`
從 `composer.json` 中移除一個套件，並將其從 `vendor` 目錄中刪除。
```bash
composer remove <vendor/package>
```

---

## 檢視與檢查

### `show`
顯示所有已安裝套件的列表，包含它們的版本和描述。
```bash
composer show
```

### `outdated`
檢查目前已安裝的套件中，有哪些版本落後於 `composer.json` 中允許的最新版本。
```bash
composer outdated
```

### `validate`
檢查 `composer.json` 檔案的格式是否正確，避免語法錯誤。
```bash
composer validate
```

---

## 自動載入與效能

### `dump-autoload`
重新產生 `vendor/autoload.php` 檔案。當您手動在 `autoload` 對應的目錄中新增類別，或修改 `composer.json` 的 `autoload` 區塊後，應執行此指令。
```bash
composer dump-autoload
```
- `-o` 或 `--optimize`: 產生一個經過最佳化的 classmap，在正式環境中可以顯著提升類別載入的效能。

---

## 其他常用指令

### `create-project`
基於一個現有的套件來建立一個新專案。常用於快速搭建一個框架（如 Laravel, Symfony）的初始環境。
```bash
composer create-project <vendor/package> <project-name>
```

### `run-script`
執行在 `composer.json` 的 `scripts` 區塊中自定義的指令。
```bash
composer run-script test
```

### `--version`
顯示當前 Composer 的版本。
```bash
composer --version
```

### `composer.phar`
以 composer.phar 檔案 初始化專案 
```bash
php composer.phar init
```