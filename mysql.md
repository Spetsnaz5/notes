# 目錄

- [MySQL 交易隔離級別 (Transaction Isolation Level)](#mysql-交易隔離級別-transaction-isolation-level)
- [MySQL 鎖機制 (Locking)](#mysql-鎖機制-locking)
- [MySQL 基礎指令](#mysql-基礎指令)
- [索引 (Indexing)](#索引-indexing)
- [資料表約束 (Constraints)](#資料表約束-constraints)

---

# MySQL 交易隔離級別 (Transaction Isolation Level)

## 1. 讀未提交 (Read Uncommitted)
最低的隔離級別，允許讀取其他事務尚未提交的變更，可能導致髒讀 (Dirty Read)。
- **效能**：最高，因為不需要加鎖，不會阻止其他事務。
- **鎖資料**：否。
- **適用場景**：對數據一致性要求極低，追求極致效能的場景 (如簡單的數據分析)。

## 2. 讀已提交 (Read Committed)
保證只能讀取其他事務已提交的數據，避免髒讀，但可能出現不可重複讀 (Non-repeatable Read)。
- **效能**：相對較高，開銷低於更高隔離級別。
- **鎖資料**：部分鎖定。讀取時加共享鎖，修改時加排他鎖。
- **適用場景**：大部分日常應用的理想選擇 (如 OLTP 系統)。

## 3. 可重複讀 (Repeatable Read)
保證同一事務內多次讀取相同數據的結果一致，避免髒讀與不可重複讀。MySQL InnoDB 的默認隔離級別。
- **效能**：略低於 `READ COMMITTED`，因為需要維持一致性快照，並可能使用間隙鎖 (Gap Lock) 來防止幻讀 (Phantom Read)。
- **鎖資料**：是。讀取時加共享鎖和間隙鎖，寫入時加排他鎖。
- **適用場景**：MySQL 預設選擇，適合需要數據一致性但又需要一定性能的場景。

## 4. 可序列化 (Serializable)
最高的隔離級別，通過強制事務順序執行，完全避免所有併發問題，但會大幅降低並發性能。
- **效能**：最差，因為所有操作都會被序列化。
- **鎖資料**：是。讀寫都會鎖定範圍內的所有數據。
- **適用場景**：需要強一致性的極端場景 (如金融系統)。

### 隔離級別綜合比較

| 隔離級別         | 效能 | 是否鎖資料           | 特點                                       |
| ------------------ | ---- | ---------------------- | ------------------------------------------ |
| READ UNCOMMITTED   | 最高 | 不鎖資料               | 無一致性保證，適合快速讀取需求。           |
| READ COMMITTED     | 高   | 部分鎖資料             | 避免脏讀，適合大多數應用場景。             |
| REPEATABLE READ    | 中   | 會鎖資料（含間隙鎖）   | 避免脏讀與不可重複讀，是 MySQL 默認選擇。 |
| SERIALIZABLE       | 低   | 會鎖資料（讀寫都鎖）   | 強一致性，但效能低，僅適用於特殊場景。     |

> **參考資料**: [Transaction 併發錯誤與隔離層級](https://oldmo860617.medium.com/transaction-%E4%BD%B5%E7%99%BC%E9%8C%AF%E8%AA%A4%E8%88%87%E9%9A%94%E9%9B%A2%E5%B1%A4%E7%B4%9A-51b8af6178ae)

---

# MySQL 鎖機制 (Locking)

## 主要鎖類型

| 鎖類型       | 用途             | 特點                               |
| ------------ | ---------------- | ---------------------------------- |
| **共享鎖 (S)** | 保護讀取操作     | 允許多事務同時讀取，禁止寫入       |
| **排他鎖 (X)** | 保護寫入操作     | 寫操作唯一持有，禁止其他讀/寫      |
| **意向鎖 (IS/IX)** | 多層級鎖協調     | 快速檢查表級鎖是否可加             |

## 特定鎖類型與概念

| 鎖類型         | 用途                 | 特點                                     |
| -------------- | -------------------- | ---------------------------------------- |
| **行級鎖**     | 僅對單行資料加鎖     | 粒度小，並發性能高                       |
| **表級鎖**     | 對整個表加鎖         | 粒度大，適合批量操作                     |
| **間隙鎖 (Gap Lock)** | 防止幻讀             | 鎖住索引「間隙」，而非具體行              |
| **Next-Key Lock** | 結合行鎖和間隙鎖     | 鎖住匹配行及其前方間隙                   |
| **悲觀鎖**     | 實時加鎖以避免衝突   | 通常基於資料庫原生鎖 (`SELECT ... FOR UPDATE`) |
| **樂觀鎖**     | 檢查版本號避免衝突   | 不依賴資料庫鎖，應用層實現，效率高       |

---

# MySQL 基礎指令

## 連線與資料庫操作
```sql
-- 登入 MySQL
mysql -u your_username -p

-- 顯示所有資料庫
SHOW DATABASES;

-- 建立新資料庫
CREATE DATABASE database_name;

-- 使用指定的資料庫
USE database_name;

-- 刪除資料庫 (請謹慎使用)
DROP DATABASE database_name;
```

## 資料表操作 (DDL - Data Definition Language)
```sql
-- 建立新資料表
CREATE TABLE table_name (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 查看資料表結構
DESCRIBE table_name;
-- 或
SHOW COLUMNS FROM table_name;

-- 修改資料表 (例如：新增一個欄位)
ALTER TABLE table_name ADD COLUMN age INT;

-- 刪除資料表
DROP TABLE table_name;
```

## 資料操作 (DML - Data Manipulation Language)
```sql
-- 新增資料
INSERT INTO table_name (name, email, age) VALUES ('John Doe', 'john.doe@example.com', 30);

-- 更新資料
UPDATE table_name SET age = 31 WHERE name = 'John Doe';

-- 刪除資料
DELETE FROM table_name WHERE name = 'John Doe';
```

## 資料查詢 (DQL - Data Query Language)
```sql
-- 查詢所有資料
SELECT * FROM table_name;

-- 條件查詢
SELECT * FROM table_name WHERE age > 30;

-- 排序查詢
SELECT * FROM table_name ORDER BY created_at DESC;

-- 限制回傳筆數
SELECT * FROM table_name LIMIT 10;

-- 彙總查詢 (搭配 GROUP BY)
SELECT age, COUNT(*) FROM table_name GROUP BY age;

-- 連接查詢 (JOIN)
SELECT u.name, o.order_details
FROM users u
JOIN orders o ON u.id = o.user_id;
```

---

# 索引 (Indexing)

**索引是資料庫查詢效能的靈魂**。它是一種特殊的資料結構 (在 MySQL 中主要是 B-Tree)，能讓資料庫引擎快速地找到特定資料，而不需要逐行掃描整個資料表 (Full Table Scan)。良好的索引策略可以將查詢速度從 `O(n)` 提升到 `O(log n)`。

不恰當的索引策略是造成查詢緩慢最常見的原因。進階主題包含：複合索引、覆蓋索引、以及索引失效的場景。

```sql
-- 在 'name' 欄位上建立索引
CREATE INDEX idx_name ON table_name (name);

-- 建立唯一索引，確保欄位值不重複
CREATE UNIQUE INDEX idx_email ON table_name (email);

-- 查看資料表的索引
SHOW INDEX FROM table_name;

-- 刪除索引
DROP INDEX idx_name ON table_name;
```

---

# 資料表約束 (Constraints)
約束用於確保資料庫中資料的準確性和可靠性。

- **NOT NULL**: 確保欄位不能有 NULL 值。
- **UNIQUE**: 確保欄位中的所有值都不同。
- **PRIMARY KEY**: `NOT NULL` 和 `UNIQUE` 的組合。唯一標識資料表中的每一行。
- **FOREIGN KEY**: 用於連結兩個資料表，防止破壞資料表之間連結的行為。
- **DEFAULT**: 為欄位提供預設值。
- **CHECK**: (MySQL 8.0.16+ 支持) 確保欄位中的值符合特定條件。

```sql
-- 包含多種約束的建表範例
CREATE TABLE orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    product_name VARCHAR(255) NOT NULL,
    quantity INT NOT NULL CHECK (quantity > 0),
    user_id INT,
    order_date DATE DEFAULT (CURRENT_DATE),
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);
```

---
