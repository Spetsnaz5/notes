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

# 七、Getter / Setter

封裝物件屬性。

| 命名 | 說明 | 範例 |
|-----|-----|-----|
| get | 取得 | getUser() |
| set | 設定 | setPassword() |
| retrieve | 擷取 | retrieveToken() |
| fetch | 抓取 | fetchUser() |

---

# 八、初始化 / Lifecycle

物件生命週期。

| 命名 | 說明 | 範例 |
|-----|-----|-----|
| init | 初始化 | initCache() |
| boot | 啟動 | bootService() |
| setup | 設定 | setupEnvironment() |
| configure | 配置 | configureApp() |
| mount | 掛載 | mountComponent() |
| destroy | 銷毀 | destroySession() |

---

# 九、事件 / Callback

事件命名。

| 命名 | 說明 | 範例 |
|-----|-----|-----|
| on | 事件觸發 | onUserCreated() |
| before | 事件之前 | beforeSave() |
| after | 事件之後 | afterLogin() |
| when | 條件事件 | whenOrderPaid() |

---

# 十、測試命名（Testing）

測試名稱應「可讀即文件」。

| 命名 | 說明 | 範例 |
|-----|-----|-----|
| test | PHPUnit 標準 | test_user_can_create_order |
| mock | 模擬物件 | mockPaymentGateway |
| assert | 斷言 | assertOrderPaid |
| expect | 預期 | expectException |

---

# 十一、架構層命名（Architecture Naming）

常見於大型系統。

| 命名 | 說明 | 範例 |
|-----|-----|-----|
| Factory | 建立物件 | UserFactory |
| Builder | 建立複雜物件 | OrderBuilder |
| Manager | 管理物件 | CacheManager |
| Provider | 提供服務 | AuthProvider |
| Resolver | 解析 | RouteResolver |
| Adapter | 轉接 | PaymentAdapter |
| Strategy | 策略 | PaymentStrategy |
| Handler | 處理流程 | OrderHandler |
| Service | 商業邏輯 | OrderService |
| Repository | 資料存取 | UserRepository |

---

# 十二、DTO / VO / Entity 命名

DDD 或分層架構常見。

| 命名 | 說明 | 範例 |
|-----|-----|-----|
| DTO | Data Transfer Object | UserDto |
| VO | Value Object | MoneyVO |
| Entity | 具有 Identity | OrderEntity |
| Model | ORM Model | UserModel |

---

# 十三、API 命名建議

RESTful API。

| HTTP 方法 | 說明 | 範例 |
|-----|-----|-----|
| GET | 取得資料 | GET /users |
| POST | 建立資料 | POST /users |
| PUT | 更新資料 | PUT /users/{id} |
| DELETE | 刪除資料 | DELETE /users/{id} |

---

# 十四、常見命名反模式

| 壞命名 | 問題 | 建議 |
|-----|-----|-----|
| doSomething | 無語意 | createOrder |
| handleData | 不清楚 | processOrder |
| processStuff | 不明確 | processPayment |
| util | 太泛用 | DateFormatter |
| helper | 容易變垃圾桶 | OrderCalculator |

---

# 命名最佳實務總結

| 原則 | 說明 | 範例 |
|-----|-----|-----|
| Command vs Query 分離 | 修改與讀取分開 | createUser / getUser |
| Boolean 使用 is/has/can | 清楚表達判斷 | isPaid / hasStock |
| 集合使用複數 | 表示多筆資料 | users / orders |
| 動詞 + 名詞 | 提高可讀性 | calculatePrice |