
# 🧑‍💻 工程師 Emoji 分類速查表

> 適用於：Command / Queue / Log / README / 技術文件  
> 原則：**語意清楚、可快速掃描、不干擾系統**

---

## 🔁 流程 / 執行狀態

| Emoji | 用途 |
| ---- | ---- |
| ▶️ | 開始執行 |
| ⏹ | 結束 |
| ⏭ | 略過 |
| 🔁 | 重試 |
| 🔄 | 更新 / 同步 |
| 🧩 | 子流程 |
| 🚀 | 觸發 / 發佈 |
| ⏳ | 處理中 |
| 🛑 | 強制中止 |

---

## 🔍 查詢 / 驗證 / 判斷

| Emoji | 用途 |
| ---- | ---- |
| 🔍 | 檢查 / 查詢 |
| 🧪 | 測試 / 驗證 |
| 📊 | 分析 |
| 🧠 | 判斷邏輯 |
| 🧾 | 規則 / 條件 |
| 🧮 | 計算 |
| 📌 | 關鍵條件 |
| 🧩 | 條件分支 |

---

## 📦 資料 / 資源處理

| Emoji | 用途 |
| ---- | ---- |
| 📦 | 資料處理 |
| 🗃 | 資料表 / 集合 |
| 🧱 | Model / Entity |
| 📝 | 寫入 |
| 📥 | 匯入 |
| 📤 | 匯出 |
| 🧹 | 清理 |
| 🧬 | Mapping / 轉換 |

---

## 🗄 資料庫 / SQL

| Emoji | 用途 |
| ---- | ---- |
| 🗄 | Database |
| 🔑 | PK / Unique Key |
| 🧷 | Index |
| 🔐 | Transaction |
| 🔒 | Lock |
| 📑 | Schema |
| 🧾 | Query 條件 |

---

## ✅ 成功 / ⚠ 警告 / ❌ 錯誤

| Emoji | 用途 |
| ---- | ---- |
| ✔ | 成功 |
| ✅ | 完成 |
| ⚠ | 警告（不中斷） |
| 🚧 | 已知限制 |
| ❌ | 錯誤 |
| 🔥 | 嚴重錯誤 |
| 🐞 | Bug |
| 💥 | Exception |

---

## ⛓ Queue / Job / 非同步

| Emoji | 用途 |
| ---- | ---- |
| ⛓ | Queue |
| 📬 | Dispatch |
| 🧵 | Worker |
| 🕒 | Delay |
| 🔁 | Retry |
| ⏱ | Timeout |
| 📉 | Fail |
| 📈 | Success |

---

## 🧪 測試 / Debug

| Emoji | 用途 |
| ---- | ---- |
| 🧪 | Test |
| 🐞 | Debug |
| 🔎 | 深層檢查 |
| 🧯 | 排錯 |
| 📋 | Log |
| 🪵 | Trace |
| 🧠 | 問題分析 |

---

## 🔐 權限 / 設定

| Emoji | 用途 |
| ---- | ---- |
| 🔐 | Security |
| 🔑 | Auth |
| 🛡 | Permission |
| ⚙ | 設定 |
| 🧾 | Env |
| 🚫 | 禁止 |
| 👤 | 使用者 |

---

## 🌐 API / 系統整合

| Emoji | 用途 |
| ---- | ---- |
| 🌐 | API |
| 🔌 | Integration |
| 📡 | Webhook |
| 🔄 | Sync |
| 📥 | Request |
| 📤 | Response |
| 🛰 | 外部系統 |

---

## 📌 Command / Queue Log 範例

```php
$this->comment('▶️ 開始帳務日結處理');
$this->comment('🔍 檢查 ship_no + rec_bk_date 是否存在');
$this->warn('⚠ 已存在資料，略過寫入');
$this->info('✔ 資料寫入成功');
$this->error('❌ DB 寫入失敗');
$this->comment('⏹ 任務結束');
```

---
