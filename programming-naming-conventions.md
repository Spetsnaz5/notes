# 程式命名前綴與後綴完整整理（含說明與最佳實務）

> 本文件彙整常見於後端、前端與測試程式中的命名前綴與後綴，
> 內容包含：分類、用途說明、命名範例，以及不建議的反例。

---

## 一、動作類（Action / Command）
> 用於「會產生行為或副作用」的方法（寫入、呼叫、執行）

| 命名 | 說明 | 範例 |
|----|----|----|
| send | 傳送資料或請求 | sendEmail(), sendRequest() |
| save | 儲存資料 | saveUser(), saveFile() |
| load | 載入資料 | loadConfig() |
| update | 更新狀態或資料 | updateStatus() |
| create | 建立新資料 | createOrder() |
| delete | 刪除（不可逆） | deleteUser() |
| remove | 移除（較溫和） | removeItem() |
| add | 新增 | addProduct() |
| fetch | 取得（多為遠端） | fetchUsers() |
| process | 處理流程 | processOrder() |
| dispatch | 派送任務/事件 | dispatchJob() |
| handle | 處理請求或例外 | handleRequest() |
| generate | 產生資料 | generateToken() |
| reset | 重置 | resetPassword() |
| calculate | 計算 | calculateTotal() |

❌ 不建議：`doSomething()`、`action()`（語意不明）

---

## 二、判斷類（Boolean Predicate）
> 回傳 `true / false`，**強烈建議以 is / has / can 開頭**

| 命名 | 說明 | 範例 |
|----|----|----|
| is | 是否為某狀態 | isActive() |
| has | 是否擁有 | hasPermission() |
| can | 是否能夠 | canEdit() |
| should | 是否應該 | shouldRetry() |
| exists | 是否存在 | existsInDb() |
| contains | 是否包含 | containsKey() |
| equals | 是否相等 | equalsTo() |
| isValid | 是否有效 | isValidToken() |

❌ 不建議：`checkUser()`（不知回傳型別）

---

## 三、屬性 / 狀態命名（Attributes / State）
> 用於變數、DTO、Model 欄位

| 命名 | 說明 |
|----|----|
| status | 狀態 |
| type | 類型 |
| options | 選項 |
| attributes | 屬性集合 |
| data | 原始資料 |
| config | 設定 |
| params | 參數 |
| value | 值 |
| info | 簡要資訊 |
| details | 詳細資訊 |
| meta | 中繼資料 |

範例：
```php
$orderStatus
$userType
$requestParams
```

---

## 四、Getter / Setter（存取器）
> 用於封裝物件屬性

| 命名 | 說明 |
|----|----|
| get | 取得 |
| set | 設定 |
| retrieve | 擷取（偏正式） |
| fetch | 抓取（可能遠端） |

範例（Laravel）：
```php
getEmailAttribute()
setPasswordAttribute()
```

❌ 不建議：`email()`（無法判斷用途）

---

## 五、測試命名（Testing）
> 測試名稱應「可讀即文件」

| 命名 | 說明 |
|----|----|
| test | PHPUnit 標準 |
| mock | 模擬物件 |
| assert | 斷言 |
| expect | 預期行為 |

推薦：
```php
test_user_can_create_order()
test_guest_cannot_access_admin()
```

❌ 不建議：`test1()`、`testAAA()`
