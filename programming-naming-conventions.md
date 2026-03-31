# 程式命名規範大全（Engineering Naming Convention Guide）
---

# 一、動作類（Action / Command）

用於「會產生副作用」的方法。

| 命名 | 說明 | 範例 |
|-----|-----|-----|
| send | 傳送資料 | sendEmail() |
| save | 儲存 | saveUser() |
| load | 載入 | loadConfig() |
| update | 更新 | updateStatus() |
| create | 建立 | createOrder() |
| delete | 刪除 | deleteUser() |
| remove | 移除 | removeItem() |
| add | 新增 | addProduct() |
| fetch | 取得遠端資料 | fetchUsers() |
| process | 處理流程 | processOrder() |
| dispatch | 派送任務 | dispatchJob() |
| handle | 處理事件 | handleRequest() |
| generate | 產生 | generateToken() |
| reset | 重置 | resetPassword() |
| calculate | 計算 | calculateTotal() |
| execute | 執行 | executeTask() |

---

# 二、查詢類（Query）

用於 **只讀資料，不改變狀態**。

| 命名 | 說明 | 範例 |
|-----|-----|-----|
| get | 取得單一資料 | getUser() |
| find | 查找 | findUserById() |
| findAll | 查找全部 | findAllUsers() |
| list | 列出集合 | listOrders() |
| query | 查詢 | queryProducts() |
| search | 搜尋 | searchOrders() |
| retrieve | 擷取 | retrieveConfig() |

---

# 三、Boolean 判斷類（Predicate）

回傳 `true / false`

| 命名 | 說明 | 範例 |
|-----|-----|-----|
| is | 是否為某狀態 | isActive() |
| has | 是否擁有 | hasPermission() |
| can | 是否能 | canEdit() |
| should | 是否應該 | shouldRetry() |
| exists | 是否存在 | existsInDb() |
| contains | 是否包含 | containsKey() |
| equals | 是否相等 | equalsTo() |
| isValid | 是否有效 | isValidToken() |

---

# 四、資料轉換（Transform）

資料轉換或解析。

| 命名 | 說明 | 範例 |
|-----|-----|-----|
| to | 轉換 | toArray() |
| from | 從資料建立 | fromJson() |
| parse | 解析 | parseToken() |
| map | 映射 | mapUserDto() |
| convert | 轉換 | convertCurrency() |
| format | 格式化 | formatDate() |
| normalize | 正規化 | normalizeEmail() |

---

# 五、屬性 / 狀態命名

用於變數、DTO、Model 欄位。

| 命名 | 說明 | 範例 |
|-----|-----|-----|
| status | 狀態 | orderStatus |
| type | 類型 | userType |
| options | 選項 | requestOptions |
| attributes | 屬性集合 | userAttributes |
| data | 原始資料 | responseData |
| config | 設定 | appConfig |
| params | 參數 | requestParams |
| value | 值 | totalValue |
| info | 簡要資訊 | userInfo |
| details | 詳細資訊 | orderDetails |
| meta | 中繼資料 | pageMeta |

---

# 六、集合命名（Collection）

表示多筆資料。

| 命名 | 說明 | 範例 |
|-----|-----|-----|
| List | 有順序集合 | userList |
| Set | 不重複集合 | productSet |
| Map | Key-Value | orderMap |
| Collection | 通用集合 | userCollection |

---
