# 目錄

- [MySQL 交易隔離級別 (Transaction Isolation Level)](#mysql-交易隔離級別-transaction-isolation-level)

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