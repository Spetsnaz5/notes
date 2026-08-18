# Mermaid

## 索引目錄

- [簡介](#簡介)
- [流程圖 (Flowchart)](#流程圖-flowchart)
- [時序圖 (Sequence Diagram)](#時序圖-sequence-diagram)
- [類別圖 (Class Diagram)](#類別圖-class-diagram)
- [狀態圖 (State Diagram)](#狀態圖-state-diagram)
- [實體關係圖 (ER Diagram)](#實體關係圖-er-diagram)
- [甘特圖 (Gantt Chart)](#甘特圖-gantt-chart)
- [圓餅圖 (Pie Chart)](#圓餅圖-pie-chart)
- [實用資源](#實用資源)

---

## 簡介

Mermaid 是一種以純文字描述圖表的語法，可在 Markdown 中直接渲染成圖形。

````markdown
```mermaid
圖表類型
  圖表內容
```
````

支援環境：GitHub、GitLab、Notion、VS Code（需插件）、Obsidian 等。

---

## 流程圖 (Flowchart)

### 基本語法

```mermaid
flowchart TD
    A[開始] --> B{判斷條件}
    B -- 是 --> C[執行動作]
    B -- 否 --> D[結束]
    C --> D
```

### 方向

| 語法 | 方向 |
| :--- | :--- |
| `TD` / `TB` | 上到下 |
| `BT` | 下到上 |
| `LR` | 左到右 |
| `RL` | 右到左 |

### 節點形狀

```mermaid
flowchart LR
    A[方形]
    B(圓角方形)
    C{菱形 / 判斷}
    D((圓形))
    E>非對稱]
    F[(資料庫)]
```

| 語法 | 形狀 | 常用於 |
| :--- | :--- | :--- |
| `[文字]` | 方形 | 一般步驟 |
| `(文字)` | 圓角方形 | 開始/結束 |
| `{文字}` | 菱形 | 判斷/條件 |
| `((文字))` | 圓形 | 事件 |
| `[(文字)]` | 資料庫形 | 儲存 |

### 連線樣式

```mermaid
flowchart LR
    A --> B          %% 實線箭頭
    C --- D          %% 實線無箭頭
    E -.-> F         %% 虛線箭頭
    G ==> H          %% 粗線箭頭
    I -- 標籤 --> J  %% 帶文字的連線
```

| 語法 | 樣式 |
| :--- | :--- |
| `-->` | 實線箭頭 |
| `---` | 實線無箭頭 |
| `-.->` | 虛線箭頭 |
| `==>` | 粗線箭頭 |
| `-- 文字 -->` | 帶標籤的連線 |

### 子圖 (Subgraph)

```mermaid
flowchart TD
    subgraph 前端
        A[使用者介面] --> B[API 呼叫]
    end
    subgraph 後端
        C[Controller] --> D[Service]
        D --> E[(資料庫)]
    end
    B --> C
```

---

## 時序圖 (Sequence Diagram)

描述多個參與者之間的訊息互動流程。

### 基本語法

```mermaid
sequenceDiagram
    participant 使用者
    participant 前端
    participant 後端
    participant DB

    使用者->>前端: 點擊登入
    前端->>後端: POST /login
    後端->>DB: 查詢帳號
    DB-->>後端: 回傳資料
    後端-->>前端: 回傳 Token
    前端-->>使用者: 登入成功
```

### 訊息類型

| 語法 | 樣式 |
| :--- | :--- |
| `->>` | 實線箭頭（請求） |
| `-->>` | 虛線箭頭（回應） |
| `->` | 實線無箭頭 |
| `-->` | 虛線無箭頭 |

### 進階語法

```mermaid
sequenceDiagram
    participant A
    participant B

    %% 啟動區塊（顯示 A 的生命線）
    activate A
    A->>B: 發送請求
    activate B
    B-->>A: 回傳結果
    deactivate B
    deactivate A

    %% 備註
    Note over A,B: 這是一段備註

    %% 條件迴圈
    loop 每秒輪詢
        A->>B: 心跳檢測
    end

    %% 條件判斷
    alt 成功
        B-->>A: 200 OK
    else 失敗
        B-->>A: 500 Error
    end
```

---

## 類別圖 (Class Diagram)

描述物件導向的類別結構與關係。

### 基本語法

```mermaid
classDiagram
    class Animal {
        +String name
        +int age
        +makeSound() void
    }

    class Dog {
        +String breed
        +fetch() void
    }

    class Cat {
        +bool indoor
        +purr() void
    }

    Animal <|-- Dog : 繼承
    Animal <|-- Cat : 繼承
```

### 存取修飾符

| 符號 | 意義 |
| :---: | :--- |
| `+` | public |
| `-` | private |
| `#` | protected |
| `~` | package |

### 關係類型

```mermaid
classDiagram
    A <|-- B : 繼承 (Inheritance)
    C *-- D : 組合 (Composition)
    E o-- F : 聚合 (Aggregation)
    G --> H : 關聯 (Association)
    I ..> J : 依賴 (Dependency)
    K ..|> L : 實作 (Realization)
```

| 語法 | 關係 |
| :--- | :--- |
| `<\|--` | 繼承 |
| `*--` | 組合（強擁有） |
| `o--` | 聚合（弱擁有） |
| `-->` | 關聯 |
| `..>` | 依賴 |
| `..\|>` | 實作介面 |

---

## 狀態圖 (State Diagram)

描述系統在不同狀態間的轉換。

### 基本語法

```mermaid
stateDiagram-v2
    [*] --> 待機
    待機 --> 處理中 : 收到請求
    處理中 --> 成功 : 處理完成
    處理中 --> 失敗 : 發生錯誤
    成功 --> [*]
    失敗 --> 待機 : 重試
```

> `[*]` 代表開始或結束狀態。

### 巢狀狀態

```mermaid
stateDiagram-v2
    [*] --> 已登入

    state 已登入 {
        [*] --> 瀏覽中
        瀏覽中 --> 結帳中 : 前往結帳
        結帳中 --> 瀏覽中 : 取消
    }

    已登入 --> [*] : 登出
```

---

## 實體關係圖 (ER Diagram)

描述資料庫的資料表結構與關聯。

### 基本語法

```mermaid
erDiagram
    USER {
        int id PK
        string name
        string email
        datetime created_at
    }

    ORDER {
        int id PK
        int user_id FK
        decimal total
        string status
    }

    ORDER_ITEM {
        int id PK
        int order_id FK
        int product_id FK
        int quantity
    }

    USER ||--o{ ORDER : "擁有"
    ORDER ||--|{ ORDER_ITEM : "包含"
```

### 關係符號

| 符號 | 意義 |
| :--- | :--- |
| `\|\|` | 恰好一個 |
| `o\|` | 零個或一個 |
| `\|{` | 一個或多個 |
| `o{` | 零個或多個 |

範例：`USER ||--o{ ORDER` = 一個 USER 對應零個或多個 ORDER。

---

## 甘特圖 (Gantt Chart)

描述專案時程與任務排程。

### 基本語法

```mermaid
gantt
    title 專案開發時程
    dateFormat YYYY-MM-DD

    section 需求分析
    需求訪談     : done,    task1, 2026-08-01, 3d
    文件撰寫     : done,    task2, after task1, 2d

    section 開發
    前端開發     : active,  task3, 2026-08-06, 7d
    後端開發     :          task4, 2026-08-06, 10d

    section 測試
    整合測試     : crit,    task5, after task4, 5d
    上線部署     : crit,    task6, after task5, 1d
```

### 任務狀態標籤

| 標籤 | 顯示效果 |
| :--- | :--- |
| `done` | 已完成（灰色） |
| `active` | 進行中（藍色） |
| `crit` | 關鍵路徑（紅色） |
| 無標籤 | 預設（綠色） |

---

## 圓餅圖 (Pie Chart)

```mermaid
pie title 技術棧使用比例
    "PHP" : 40
    "JavaScript" : 30
    "Python" : 20
    "其他" : 10
```

---

## 實用資源

- [Mermaid 官方文件](https://mermaid.js.org/)
- [Mermaid Live Editor](https://mermaid.live/)（即時預覽）
