# 目錄

- [MySQL 交易隔離級別 (Transaction Isolation Level)](#mysql-交易隔離級別-transaction-isolation-level)

---

# MySQL 交易隔離級別 (Transaction Isolation Level)

## 1. 讀未提交 (Read Uncommitted)
最低的隔離級別，允許讀取其他事務尚未提交的變更，可能導致髒讀 (Dirty Read)。
- **效能**：最高，因為不需要加鎖，不會阻止其他事務。
- **鎖資料**：否。
- **適用場景**：對數據一致性要求極低，追求極致效能的場景 (如簡單的數據分析)。
