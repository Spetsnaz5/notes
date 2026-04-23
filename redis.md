## 索引目錄

- [通用指令 (Generic Commands)](#通用指令-generic-commands)
- [String (字串)](#string-字串)
- [Hash (雜湊)](#hash-雜湊)
- [List (列表)](#list-列表)
- [Set (集合)](#set-集合)
- [Sorted Set (有序集合)](#sorted-set-有序集合)
- [資料結構比較](#資料結構比較)
- [交易 (Transactions)](#交易-transactions)
- [發布/訂閱 (Pub/Sub)](#發布訂閱-pubsub)
- [伺服器管理 (Server Management)](#伺服器管理-server-management)
- [持久化機制 (Persistence)](#持久化機制-persistence)
- [高可用性 (High Availability)](#高可用性-high-availability)
- [水平擴展 (Horizontal Scaling)](#水平擴展-horizontal-scaling)
- [進階資料結構](#進階資料結構)

---

## 通用指令 (Generic Commands)

### `DEL`
刪除一個或多個 key。
```bash
DEL key [key ...]
```

### `EXISTS`
檢查指定的 key 是否存在。
```bash
EXISTS key [key ...]
```

### `EXPIRE`
設定 key 的過期時間（單位：秒）。
```bash
EXPIRE key seconds
```

### `PEXPIRE`
設定 key 的過期時間（單位：毫秒）。
```bash
PEXPIRE key milliseconds
```

### `KEYS`
尋找所有符合指定模式的 key。
```bash
KEYS pattern
```
**注意**: 在生產環境中應謹慎使用，因為它會遍歷所有 key，可能導致效能問題。

### `MOVE`
將當前資料庫的 key 移動到指定的資料庫 db 當中。
```bash
MOVE key db
```

### `PERSIST`
移除 key 的過期時間，使其永不過期。
```bash
PERSIST key
```

### `TTL`
以秒為單位，返回 key 的剩餘過期時間。
```bash
TTL key
```

### `PTTL`
以毫秒為單位，返回 key 的剩餘過期時間。
```bash
PTTL key
```

### `TYPE`
返回 key 所儲存的值的類型。
```bash
TYPE key
```

### `RENAME`
修改 key 的名稱。
```bash
RENAME key newkey
```

---

## String (字串)

字符串是 Redis 中最基本的數據類型，可以包含任何類型的數據。適合用於快取、計數器等場景。

### `SET`
設定指定 key 的值。
```bash
SET key value [EX seconds]
```
- `EX seconds`：設定過期時間（秒）。

### `GET`
獲取指定 key 的值。
```bash
GET key
```

### `GETRANGE`
獲取 key 所儲存的字串值的指定範圍內的子字串。
```bash
GETRANGE key start end
```

### `GETSET`
將指定 key 的值設定為 new value，並返回其舊值。
```bash
GETSET key new_value
```

### `MGET`
獲取所有給定 key 的值。
```bash
MGET key1 [key2 ...]
```

### `SETEX`
設定 key 的值和過期時間（秒）。
```bash
SETEX key seconds value
```

### `STRLEN`
返回 key 所儲存的字串值的長度。
```bash
STRLEN key
```

### `MSET`
同時設定一個或多個 key-value 對。
```bash
MSET key1 value1 [key2 value2 ...]
```

### `MSETNX`
同時設定一個或多個 key-value 對，當且僅當所有給定的 key 都不存在時。
```bash
MSETNX key1 value1 [key2 value2 ...]
```

### `INCR`
將 key 中儲存的數字值增一。
```bash
INCR key
```

### `INCRBY`
將 key 所儲存的數字值加上指定的增量。
```bash
INCRBY key increment
```

### `INCRBYFLOAT`
將 key 所儲存的數字值加上指定的浮點數增量。
```bash
INCRBYFLOAT key increment
```

### `DECR`
將 key 中儲存的數字值減一。
```bash
DECR key
```

### `DECRBY`
將 key 所儲存的數字值減去指定的減量。
```bash
DECRBY key decrement
```

### `APPEND`
如果 key 已經存在並且是一個字串，`APPEND` 命令將指定的 value 附加到該 key 原來值（value）的末尾。
```bash
APPEND key value
```

---

## Hash (雜湊)

Hash 是一個 string 類型的 field 和 value 的對應表，特別適合用於儲存物件。

### `HDEL`
刪除一個或多個 Hash 表的欄位。
```bash
HDEL key field1 [field2 ...]
```

### `HEXISTS`
查看 Hash 表的指定欄位是否存在。
```bash
HEXISTS key field
```

### `HGET`
獲取儲存在 Hash 表中指定欄位的值。
```bash
HGET key field
```

### `HGETALL`
獲取在 Hash 表中指定 key 的所有欄位和值。
```bash
HGETALL key
```

### `HINCRBY`
為 Hash 表中的欄位值加上指定的增量。
```bash
HINCRBY key field increment
```

### `HINCRBYFLOAT`
為 Hash 表中的欄位值加上指定的浮點數增量。
```bash
HINCRBYFLOAT key field increment
```

### `HKEYS`
獲取 Hash 表中的所有欄位。
```bash
HKEYS key
```

### `HLEN`
獲取 Hash 表中欄位的數量。
```bash
HLEN key
```

### `HMGET`
獲取 Hash 表中一個或多個給定欄位的值。
```bash
HMGET key field1 [field2 ...]
```

### `HSET`
將 Hash 表中指定欄位的值設為給定值。
```bash
HSET key field value
```

### `HMSET`
同時將多個 field-value (欄位-值)對設定到 Hash 表中。
```bash
HMSET key field1 value1 [field2 value2 ...]
```

### `HSETNX`
只有在欄位 field 不存在時，才設定 Hash 表中欄位的值。
```bash
HSETNX key field value
```

### `HVALS`
獲取 Hash 表中的所有值。
```bash
HVALS key
```

---

## List (列表)

List 是簡單的字串列表，按照插入順序排序。可以在列表的頭部（左邊）或尾部（右邊）添加元素。

### `LPOP`
移出並獲取列表的第一個元素。
```bash
LPOP key
```

### `RPOP`
移出並獲取列表的最後一個元素。
```bash
RPOP key
```

### `LPUSH`
將一個或多個值插入到列表頭部。
```bash
LPUSH key value1 [value2 ...]
```

### `RPUSH`
將一個或多個值插入到列表尾部。
```bash
RPUSH key value1 [value2 ...]
```

### `LRANGE`
獲取列表指定範圍內的元素。
```bash
LRANGE key start stop
```

### `LLEN`
獲取列表的長度。
```bash
LLEN key
```

### `LINDEX`
通過索引獲取列表中的元素。
```bash
LINDEX key index
```

### `LSET`
通過索引來設定列表中元素的值。
```bash
LSET key index value
```

### `LTRIM`
對一個列表進行修剪，只保留指定區間內的元素。
```bash
LTRIM key start stop
```

### `LINSERT`
在列表的元素前或後插入元素。
```bash
LINSERT key BEFORE|AFTER pivot value
```

### `BLPOP` / `BRPOP`
`LPOP` / `RPOP` 的阻塞版本，如果列表中沒有元素，會阻塞連線直到等待逾時或發現可彈出的元素為止。
```bash
BLPOP key1 [key2 ...] timeout
BRPOP key1 [key2 ...] timeout
```

### `RPOPLPUSH` / `BRPOPLPUSH`
從一個列表的尾部彈出一個元素，並將其插入到另一個列表的頭部。
```bash
RPOPLPUSH source destination
BRPOPLPUSH source destination timeout
```

---

## Set (集合)

Set 是 String 類型的無序集合，不允許重複的成員。

### `SADD`
向集合添加一個或多個成員。
```bash
SADD key member1 [member2 ...]
```

### `SMEMBERS`
返回集合中的所有成員。
```bash
SMEMBERS key
```

### `SISMEMBER`
判斷 member 元素是否是集合 key 的成員。
```bash
SISMEMBER key member
```

### `SCARD`
獲取集合的成員數。
```bash
SCARD key
```

### `SPOP`
隨機移除並返回集合中的一個或多個元素。
```bash
SPOP key [count]
```

### `SRANDMEMBER`
隨機返回集合中一個或多個元素，但不移除。
```bash
SRANDMEMBER key [count]
```

### `SREM`
移除集合中一個或多個成員。
```bash
SREM key member1 [member2 ...]
```

### `SUNION` / `SINTER` / `SDIFF`
對多個集合執行聯集、交集、差集運算。
```bash
SUNION key1 [key2 ...]
SINTER key1 [key2 ...]
SDIFF key1 [key2 ...]
```

### `SSCAN`
迭代集合中的元素。
```bash
SSCAN key cursor [MATCH pattern] [COUNT count]
```

---

## Sorted Set (有序集合)

Sorted Set 是 String 類型的有序集合，每個元素都會關聯一個 double 類型的分數 (score)，Redis 正是通過分數來為集合中的成員進行排序。

### `ZADD`
向有序集合添加一個或多個成員，或者更新已存在成員的分數。
```bash
ZADD key score1 member1 [score2 member2 ...]
```

### `ZRANGE`
通過索引區間返回有序集合成指定範圍的成員（按分數遞增排序）。
```bash
ZRANGE key start stop [WITHSCORES]
```

### `ZREVRANGE`
返回有序集合中指定區間內的成員（按分數遞減排序）。
```bash
ZREVRANGE key start stop [WITHSCORES]
```

### `ZRANGEBYSCORE`
通過分數區間返回有序集合的成員（按分數遞增排序）。
```bash
ZRANGEBYSCORE key min max [WITHSCORES]
```

### `ZCARD`
獲取有序集合的成員數。
```bash
ZCARD key
```

### `ZCOUNT`
計算在有序集合中指定分數區間的成員數。
```bash
ZCOUNT key min max
```

### `ZINCRBY`
為有序集合中指定成員的分數加上增量。
```bash
ZINCRBY key increment member
```

### `ZRANK`
返回有序集合中指定成員的排名（按分數遞增排序）。
```bash
ZRANK key member
```

### `ZREVRANK`
返回有序集合中指定成員的排名（按分數遞減排序）。
```bash
ZREVRANK key member
```

### `ZREM`
移除有序集合中的一個或多個成員。
```bash
ZREM key member [member ...]
```

### `ZREMRANGEBYRANK`
移除有序集合中給定排名區間的所有成員。
```bash
ZREMRANGEBYRANK key start stop
```

### `ZREMRANGEBYSCORE`
移除有序集合中給定分數區間的所有成員。
```bash
ZREMRANGEBYSCORE key min max
```

### `ZSCORE`
返回有序集合中，成員 member 的分數。
```bash
ZSCORE key member
```

### `ZINTERSTORE` / `ZUNIONSTORE`
計算給定一個或多個有序集的交集/聯集，並將結果集儲存在一個新的有序集中。
```bash
ZINTERSTORE destination numkeys key [key ...]
ZUNIONSTORE destination numkeys key [key ...]
```

### `ZSCAN`
迭代有序集合中的元素（包括元素成員和元素分數）。
```bash
ZSCAN key cursor [MATCH pattern] [COUNT count]
```

---

### 資料結構比較

| 資料結構 | 核心特點 | 主要應用場景 |
| :--- | :--- | :--- |
| String (字串) | 單一的 Key-Value，值可以是字串、數字或二進位資料。 |  快取：快取頁面、API 回應、使用者資訊。 <br> 計數器：文章點閱數、按讚數、庫存量。 <br> 分散式鎖：利用 SETNX 實現。 | 
| List (列表) | 有序的字串列表，可在頭尾兩端快速操作 (雙向鏈結串列)。 |  訊息佇列：簡單的非同步任務佇列 (LPUSH + BRPOP)。 <br> 最新動態：最新發布的文章、留言 (LPUSH + LTRIM)。  <br> 貼文牆 (Timeline)：關注者的最新貼文。 |
| Hash (雜湊) | Key-Field-Value 結構，像是一個 Key 對應一個小型 Key-Value Map。 | 物件儲存：使用者個人資料、商品詳細資訊、文章內容。 <br> 集中管理：將一個物件的屬性集中在一個 Key 中，方便管理。 |
| Set (集合) | 無序、唯一的字串集合。 |  標籤系統：為文章、商品、使用者加上標籤。  <br> 共同好友/興趣：利用交集 (SINTER) 運算。 <br> 抽獎系統：利用 SPOP 或 SRANDMEMBER。 <br> 獨立 IP 統計：利用其唯一性。 |
| Sorted Set (有序集合) | 有序、唯一的字串集合，每個成員都關聯一個分數 (score)。 |  排行榜：遊戲積分榜、熱門文章榜、銷售額排行。 <br> 優先級佇列：帶有權重的任務佇列。 <br> 範圍查詢：例如「薪資在 5-10 萬之間的使用者」。 |

---

## 交易 (Transactions)
Redis 交易可以一次執行多個命令，並帶有兩個重要的保證：序列化和原子性。

### `MULTI`
標記一個交易區塊的開始。之後的指令都會被放入一個佇列中，直到 `EXEC` 被呼叫。
```bash
MULTI
```

### `EXEC`
執行所有在 `MULTI` 之後入隊的指令。
```bash
EXEC
```

### `DISCARD`
取消交易，放棄執行佇列中的所有指令。
```bash
DISCARD
```

---

## 發布/訂閱 (Pub/Sub)
Redis 的發布/訂閱功能允許客戶端訂閱頻道，並接收發送到這些頻道的訊息。

### `SUBSCRIBE`
訂閱一個或多個給定的頻道。
```bash
SUBSCRIBE channel [channel ...]
```

### `PUBLISH`
將訊息發送到指定的頻道。
```bash
PUBLISH channel message
```

### `UNSUBSCRIBE`
退訂給定的頻道。
```bash
UNSUBSCRIBE [channel [channel ...]]
```

---

## 伺服器管理 (Server Management)
用於監控和管理 Redis 伺服器實例的指令。

### `INFO`
返回關於 Redis 伺服器的詳細資訊和統計數據。
```bash
INFO [section]
```

### `CONFIG GET` / `CONFIG SET`
在執行時期動態地查詢或設定 Redis 的設定參數。
```bash
CONFIG GET parameter
CONFIG SET parameter value
```

### `FLUSHDB`
**[危險]** 刪除當前資料庫中所有的 key。
```bash
FLUSHDB
```

### `FLUSHALL`
**[極度危險]** 刪除所有資料庫中所有的 key。
```bash
FLUSHALL
```

---

## 持久化機制 (Persistence)
Redis 是一個記憶體資料庫，為了在伺服器重啟後不遺失資料，提供了兩種持久化機制：RDB 和 AOF。

### RDB (Redis Database)
在指定的時間間隔內，將記憶體中的資料集快照寫入磁碟。RDB 檔案是一個緊湊的二進位檔案，非常適合用於備份和災難恢復。

- **優點**:
  - 檔案緊湊，恢復速度快。
  - 對效能影響較小，因為由子行程進行。
- **缺點**:
  - 如果在兩次快照之間 Redis 發生故障，會遺失最後一次快照之後的所有變更。

### AOF (Append-Only File)
以日誌的形式記錄每個「寫入」操作。當 Redis 重啟時，會重新執行 AOF 檔案中的所有指令來恢復資料集。

- **優點**:
  - 資料安全性更高，最多只會遺失最後一秒的資料（取決於設定）。
  - 檔案內容是可讀的協議文字。
- **缺點**:
  - AOF 檔案通常比 RDB 檔案大。
  - 恢復速度通常比 RDB 慢。

---

## 高可用性 (High Availability)
為了確保 Redis 服務不因單點故障而中斷，通常會採用主從複製和 Sentinel 架構。

### 主從複製 (Replication)
將一台 Redis 伺服器（Master）的資料，即時地、非同步地複製到一台或多台從伺服器（Slave）。
- **讀寫分離**: Master 處理寫入請求，Slaves 處理讀取請求，分攤讀取壓力。
- **資料備份**: Slave 是 Master 的一個熱備份。

### 哨兵模式 (Sentinel)
Sentinel 是一個獨立的程序，它會監控所有的 Redis 伺服器（Master 和 Slaves）。
- **自動故障轉移**: 當 Sentinel 發現 Master 故障時，會自動從 Slaves 中選舉出一個新的 Master，並讓其他 Slaves 指向新的 Master，從而恢復服務。

---

## 水平擴展 (Horizontal Scaling)
當單一 Redis 實例無法滿足記憶體或效能需求時，就需要使用叢集來進行水平擴展。

### Redis 叢集 (Redis Cluster)
Redis Cluster 是一個官方的、去中心化的叢集方案，它將資料自動分片（sharding）到多個節點上。
- **資料分片**: 叢集將整個資料集分割成 16384 個雜湊槽 (hash slots)。每個 key 根據其 CRC16 校驗值被分配到一個特定的 slot，而每個 Redis 節點負責處理一部分 slots。
- **高可用性**: 叢集中的每個 Master 節點都可以有多個 Slave 節點。當某個 Master 故障時，其對應的 Slave 會被提升為新的 Master，保證服務的可用性。

---

## 進階資料結構
除了核心資料類型，Redis 還提供了一些針對特定場景的最佳化資料結構。

### Bitmaps (點陣圖)
Bitmaps 本質上是 String 類型，但它允許你對位元 (bit) 進行操作。非常適合用於大量的二元狀態統計。
- `SETBIT key offset value`: 設定或清除 key 在指定 offset 上的位元 (0 或 1)。
- `GETBIT key offset`: 獲取 key 在指定 offset 上的位元。
- `BITCOUNT key [start end]`: 計算給定範圍內被設定為 1 的位元數量。
- **使用場景**: 使用者每日簽到、使用者在線狀態、功能開關等。

### HyperLogLog
用極小的、固定的記憶體來估算一個集合中不重複元素的數量（基數）。結果是近似值，有標準誤差。
- `PFADD key element [element ...]`: 將一個或多個元素添加到 HyperLogLog 中。
- `PFCOUNT key [key ...]`: 返回一個或多個 HyperLogLog 的基數估算值。
- `PFMERGE destkey sourcekey [sourcekey ...]`: 將多個 HyperLogLog 合併為一個。
- **使用場景**: 統計網站的獨立訪客數 (UV)、搜尋結果的獨立點擊數等。

### Streams (串流)
Redis 5.0 引入的強大資料類型，是一個附加日誌 (Append-only Log)，專為訊息佇列和事件流設計。
- `XADD streamID ID field string [field string ...]`: 向串流添加一條新訊息。
- `XREAD [COUNT count] [BLOCK milliseconds] STREAMS key [key ...] ID [ID ...]`: 從一個或多個串流中讀取訊息。
- **使用場景**: 訊息佇列、事件溯源 (Event Sourcing)、即時資料處理等。
