# phpDocumentor 筆記

這是一份關於 PHP 文件產生器 `phpDocumentor` 的基礎速查筆記。

## 1. phpDocumentor 是什麼？

phpDocumentor 是一個 PHP 的開源文件產生工具。它會解析您程式碼中的特定註解 (稱為 "DocBlocks")，並自動產生出專業、易於閱讀的 API 文件。這對於團隊協作和長期專案維護非常有幫助。

## 2. 如何安裝 (使用 Composer)

推薦使用 Composer 來安裝 phpDocumentor，將它作為專案的開發依賴項。

```bash
composer require --dev phpdocumentor/phpdocumentor
```

## 3. 基本使用方法

安裝完成後，您可以在專案的根目錄下，透過 `vendor/bin/phpdoc` 指令來執行。

```bash
# 基本指令
vendor/bin/phpdoc -d [要掃描的原始碼目錄] -t [產生文件的輸出目錄]

# 範例：掃描 src/ 目錄，並將文件產生到 docs/api 目錄
vendor/bin/phpdoc -d ./src -t ./docs/api
```

## 4. 常用 DocBlock 標籤

DocBlock 是一個以 `/**` 開頭，`*/` 結尾的特殊註解區塊。您可以在裡面使用 `@` 標籤來提供額外資訊。

| 標籤 (Tag)      | 用途                                                     | 範例                                                 |
| --------------- | -------------------------------------------------------- | ---------------------------------------------------- |
| `@param`        | 描述函式或方法的參數 (型別、變數名、說明)                | `@param string $name 使用者名稱`                         |
| `@return`       | 描述函式或方法的回傳值 (型別、說明)                      | `@return bool 處理是否成功`                          |
| `@var`          | 描述類別屬性 (Property) 或變數的型別                     | `@var int 使用者 ID`                                 |
| `@author`       | 標示作者資訊                                             | `@author John Doe <john.doe@example.com>`            |
| `@version`      | 標示版本號                                               | `@version 1.0.0`                                     |
| `@link`         | 提供一個 URL 連結                                        | `@link https://www.example.com 相關文件`             |
| `@see`          | 參考另一個相關的函式、方法或類別                         | `@see \MyNamespace\MyClass::anotherMethod()`         |
| `@throws`       | 描述可能拋出的例外 (Exception)                           | `@throws \InvalidArgumentException 當參數無效時`      |
| `@deprecated`   | 標示此元素已被棄用，不建議再使用                         | `@deprecated 2.0.0 請改用 newMethod()`               |

## 5. 完整範例

這是一個 documenting 一個 PHP 類別和方法的完整範例。

```php
<?php
namespace App\Service;

/**
 * Class UserService
 * 
 * 這是一個處理使用者相關操作的服務類別。
 * 
 * @package App\Service
 * @author Jane Doe <jane.doe@example.com>
 */
class UserService
{
    /**
     * @var \PDO 資料庫連線物件
     */
    protected $db;

    /**
     * UserService 的建構子。
     *
     * @param \PDO $pdo 資料庫連線物件
     */
    public function __construct(\PDO $pdo)
    {
        $this->db = $pdo;
    }

    /**
     * 根據使用者 ID 尋找使用者資料。
     *
     * 這個方法會查詢資料庫並回傳指定 ID 的使用者陣列。
     * 如果找不到使用者，則回傳 false。
     *
     * @param int $userId 要尋找的使用者 ID，必須是正整數。
     * @return array|false 如果找到使用者則回傳資料陣列，否則回傳 false。
     * @throws \InvalidArgumentException 當 $userId 不是一個正整數時拋出。
     * @see \App\Repository\UserRepository::find()
     */
    public function findUserById(int $userId)
    {
        if ($userId <= 0) {
            throw new \InvalidArgumentException('使用者 ID 必須是正整數。');
        }

        $stmt = $this->db->prepare("SELECT * FROM users WHERE id = ?");
        $stmt->execute([$userId]);
        return $stmt->fetch(\PDO::FETCH_ASSOC);
    }
}
```
