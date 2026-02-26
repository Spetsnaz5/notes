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
