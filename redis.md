## 基礎
```
進入redis
redis-cli

刪除key
del key

檢查key是否存在
exists key

設定key過期時間(秒)
expire key seconds

設定key過期時間(毫秒)
pexpire key milliseconds

查詢符合 pattern key
keys pattern

移動key至其他資料庫
move key db

移除key過期時間
persist key

回傳剩餘時間(秒)
ttl key

回傳剩餘時間(毫秒)
pttl key

回傳key類型
type key

修改key名稱
rename key newkey
```

## String
```
字符串是 Redis 中最基本的數據類型，可以包含任何類型的數據，包括純文本、序列化對象、二進制數據等。
使用情境：
  緩存數據：儲存用戶會話信息、頁面緩存等。
  計數器：實現網站的點擊量計數、視頻播放次數計數等。
  配置管理：儲存配置參數和簡單的鍵值對數據。

設定key
set key value [Ex seconds]

取得key
get key

取得key字串範圍
getrange key start end

設定key value並返回舊value
getset key value

取得多個key
mget key [key2...]

設定key與過期時間
setex key seconds value

返回key長度
strlen key

設定多個key value
mset key value [key2 value ....]

設定多個key value(具原子性 key必須都不存在)
msetnx key value [key2 value ....]

將key中的數字+1
incr key

將key中的數字+x
incrby key x

將key中的數字+x(浮點數字)
Incrbyfloat key x

將key中的數字-1
decr key

將key中的數字-x
decrby key x

對key字尾追加字串
append key value

```

## Hash
```
hash 是 string 類型的 field-value 的映射表，適合儲存對象數據，如用戶資料。
使用情境：
  用戶資料存儲：儲存用戶信息，如用戶名、年齡、郵箱等。
  商品信息：儲存商品的詳細信息，如名稱、價格、庫存量等。

刪除
hdel key field [field2...]

檢查key field是否存在
hexists key field

取得key field
hget key field

取得key所有field
hgetall key

將key field中的數字+x(浮點數字)
hincrby key field x

將key field中的數字+x
hincrbyfloat key field x

查詢符合 pattern key
hkeys key

取得key field數量
hlen key

取得key多個field
hmget key field [field2 field3 ...]

設定key field value
hset key field value

設定key多個field value
hmset key field value field2 value2 [field3 value3 ...]

設定key field value(具原子性 key必須都不存在)
hsetnx key field value

取得key所有value
hvals key

```

## List
```
列表是簡單的字符串列表，按插入順序排序。它支持從兩端插入和移除元素。
使用情境：
  消息隊列：實現簡單的消息隊列系統，儲存待處理的任務。
  最新活動：儲存最新的用戶活動記錄，如評論、帖子等。
  排行榜：儲存實時更新的排行榜數據。

取得多個List第一個元素
blpop List List2 [List3 ...] seconds

取得多個List最後一個元素
brpop List List2 [List3 ...] seconds

取得List最後一個元素，插入至另一個List至首位
brpoplpush List List2

獲得列表索引中的元素
lindex key index

在列表中的元素前或後插入元素
linsert key BEFORE|AFTER pivot value

獲得列表範圍索引的元素
lrange key start end

獲得列表長度
llen key

移出並獲取列表第一個元素
lpop key

將一個或多個加入列表頭部
lpush key value [value2...]

將一個或多個加入列表頭部，必須存在key
lpushx key value [value2...]

移出並獲取列表最後一個元素
rpop key

移除List最後一個元素，插入至另一個List至首位
rpoplpush source_key destination_key

將一個或多個加入列表尾部
rpush key value [value2...]

將一個或多個加入列表尾部，必須存在key
rpushx key value [value2...]

透過索引設定元素
lset key index value

對列表修剪只保留範圍內個元素
ltrim ket start stop
```

## Set
```
集合是無序的字符串集合，確保集合內的每個元素是唯一的。
使用情境：
  標籤系統：儲存用戶標籤、文章標籤等。
  共同好友：計算兩個用戶的共同好友。
  唯一訪問計數：統計唯一訪問者，如每天的唯一訪問IP。

集合加入一個或多個成員
sadd key member1 [member2...]

獲取集合總數
scard key

回傳集合差集
sdiff key key2

回傳集合交集
sinter key key2

回傳集合聯集
sunion key key2

檢查member是否存在集合中
sismember key member

回傳集合所有成員
smembers key

隨機移除一個元素
spop key

隨機返回count數量元素
srandmember key count

移除一個或多個元素
srem key member [member2 ...]
```

## Sorted Set
```
有序集合類似於集合，但每個元素都會關聯一個分數，根據分數對元素進行排序，且不允許重複的成員。
使用情境：
  排行榜：實現遊戲中的高分榜，按分數排序。
  優先級隊列：儲存具有優先級的任務，如定時任務。
  時間序列數據：儲存時間戳和事件對，如股票價格、傳感器數據。
```

