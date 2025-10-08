## 索引目錄

- [專案初始化與設定](#專案初始化與設定)
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
