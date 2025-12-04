# sqlmap 支援的 SQL Injection 類型

`sqlmap` 是一個強大的自動化滲透測試工具，主要支援 **6 種** SQL Injection (SQLi) 技術。這些技術涵蓋了從直接數據提取到完全無回應（Blind）的場景。

## 1. Boolean-based blind (布林盲注)
* **代號：** `B`
* **原理：** 網頁不會回傳資料庫錯誤訊息，也不會直接顯示查詢結果，但**網頁內容會根據 SQL 語句的真假 (True/False) 而發生變化**。
* **運作方式：** Sqlmap 發送一系列邏輯判斷語句（如 `AND 1=1` vs `AND 1=2`），比對 HTTP 回應的頁面大小或內容差異，逐字元推算出資料庫內容。

## 2. Time-based blind (時間盲注)
* **代號：** `T`
* **原理：** 當網頁完全沒有回傳任何差異（無論 SQL 語句對錯，頁面看起來都一樣），利用時間延遲來判斷。
* **運作方式：** 注入包含延遲函數的語句（如 MySQL 的 `SLEEP(5)` 或 SQL Server 的 `WAITFOR DELAY`）。若伺服器回應時間變長，代表注入條件為真。這是最慢但最通用的方法。

## 3. Error-based (報錯注入)
* **代號：** `E`
* **原理：** 應用程式未正確處理錯誤，將**資料庫的詳細錯誤訊息**直接顯示在網頁上。
* **運作方式：** Sqlmap 構造特定語法誘發資料庫錯誤，並將查詢的資料（如版本號、表名）夾帶在錯誤訊息中回傳。通常比盲注快。

## 4. UNION query-based (聯合查詢注入)
* **代號：** `U`
* **原理：** 最高效的注入方式。適用於網頁將 SQL 查詢結果直接顯示在頁面上的欄位。
* **運作方式：** 利用 SQL 的 `UNION` 操作符，將原本查詢的結果與攻擊者注入的查詢結果合併，直接顯示資料庫內容。

## 5. Stacked queries (堆疊查詢注入)
* **代號：** `S`
* **原理：** 資料庫配置允許在一次請求中執行多條 SQL 語句（以分號 `;` 隔開）。
* **運作方式：** 在原本查詢後附加全新的 SQL 語句。常用於執行非查詢操作，如 `INSERT`、`UPDATE`、`DELETE` 或開啟 OS Shell (`xp_cmdshell`)。
    * *注意：並非所有環境（如 PHP + MySQL 預設配置）都支援此方式。*

## 6. Out-of-band (OOB / 帶外注入)
* **代號：** `Q`
* **原理：** 當網頁無回顯且時間盲注不穩定時，利用資料庫發送外部請求的能力。
* **運作方式：** 利用資料庫功能（如 Oracle `UTL_HTTP`、SQL Server `xp_dirtree`）向攻擊者控制的伺服器發送 DNS 或 HTTP 請求，將數據「帶」出來。

---

## 指令用法：指定技術類型

使用 `--technique` 參數可指定測試類型（預設為全部測試）。參數值為上述代號的組合。

```bash
# 僅測試 Boolean-based 和 Time-based (盲注模式)
python sqlmap.py -u "[http://target.com/id=1](http://target.com/id=1)" --technique=BT

# 僅測試 UNION query-based (通常最快)
python sqlmap.py -u "[http://target.com/id=1](http://target.com/id=1)" --technique=U

# 測試所有類型 (預設行為)
python sqlmap.py -u "[http://target.com/id=1](http://target.com/id=1)" --technique=BEUSTQ
