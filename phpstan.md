## 索引目錄

- [PHPStan 是什麼？](#phpstan-是什麼)
- [安裝與設定](#安裝與設定)
- [基本使用](#基本使用)
- [分析級別 (Level)](#分析級別-level)
- [設定檔 `phpstan.neon`](#設定檔-phpstanneon)
- [其他常用指令](#其他常用指令)

---

## PHPStan 是什麼？

PHPStan 是一個 PHP 的 **靜態分析工具**。它不需要實際執行程式碼，就能在原始碼層級找出潛在的錯誤。

靜態分析可以幫助開發者在開發週期的早期發現問題，例如：
- 類型錯誤：呼叫方法時傳遞了錯誤的型別。
- 在 `null` 物件上呼叫方法。
- 使用了未定義的變數或方法。
- 方法的 PHPDoc 與實際回傳的型別不符。

使用 PHPStan 能顯著提升程式碼品質、強制執行型別規範，並減少上線後才發現的潛在錯誤。

---

## 安裝與設定

PHPStan 通常作為開發依賴套件，透過 Composer 進行安裝。

```bash
composer require --dev phpstan/phpstan
```
安裝完成後，執行檔會放在 `vendor/bin/phpstan`。

---

## 基本使用

安裝後，你可以使用 `analyse` 指令來分析你的程式碼。

### `analyse`
分析指定的目錄或檔案。建議只分析你自己的程式碼（如 `src`, `app` 目錄），而不是 `vendor` 目錄下的第三方套件。

```bash
# 分析 src 目錄
vendor/bin/phpstan analyse src

# 同時分析多個目錄
vendor/bin/phpstan analyse src tests
```

---

## 分析級別 (Level)

PHPStan 提供從 `0` 到 `9` (或 `max`) 的多個分析級別，數字越高，檢查規則越嚴格。

- **`0` 級**: 最基礎的檢查，例如未定義的類別、變數等。
- **`5` 級**: 一個不錯的起點，會檢查 PHPDoc 型別與實際程式碼是否匹配。
- **`9` / `max` 級**: 最嚴格的級別，包含對 `mixed` 型別的嚴格檢查。

建議從較低的級別開始（例如 `1` 或 `2`），逐步修正錯誤後，再慢慢提高級別。

你可以透過 `--level` 選項指定分析級別：
```bash
vendor/bin/phpstan analyse src --level=5
```

---

## 設定檔 `phpstan.neon`

為了方便管理與團隊協作，建議在專案的根目錄建立一個設定檔 `phpstan.neon`。

這是一個基礎的 `phpstan.neon` 範例：
```yaml
parameters:
    level: 5
    paths:
        - src
        - tests
    excludePaths:
        - src/Legacy/*
```

- `parameters`: 所有設定的核心區塊。
- `level`: 指定預設的分析級別。設定後，執行 `analyse` 時就不需要再加 `--level` 參數。
- `paths`: 指定要分析的目錄或檔案列表。
- `excludePaths`: 排除不需要分析的目錄或檔案。

有了設定檔後，你可以直接執行：
```bash
vendor/bin/phpstan analyse
```

---

## 其他常用指令

### `clear-result-cache`
清除 PHPStan 的分析結果快取。當你覺得分析結果不正確，或修改設定檔後，可以執行此指令來強制重新進行完整分析。
```bash
vendor/bin/phpstan clear-result-cache
```

### `--version`
顯示目前安裝的 PHPStan 版本。
```bash
vendor/bin/phpstan --version
```
