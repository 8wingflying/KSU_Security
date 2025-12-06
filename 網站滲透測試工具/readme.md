
# 網站滲透測試工具(Web Penetration Testing Tools)

- 網站滲透測試（Web Penetration Testing）是模擬駭客攻擊以找出網站安全漏洞的過程。
- 本文件整理了從資訊蒐集、漏洞掃描到實際漏洞利用（Exploitation）的常用工具。

---

## 1. 綜合型代理與掃描工具 (Proxy & Scanners)
這是滲透測試中最核心的工具，允許在瀏覽器與伺服器之間攔截、修改數據包。

### Burp Suite
* **地位：** 行業標準，滲透測試人員的必備工具。
* **功能：**
    * **Proxy：** 攔截並修改 HTTP/HTTPS 封包。
    * **Repeater：** 手動重放請求以測試回應。
    * **Intruder：** 進行暴力破解或模糊測試（Fuzzing）。
    * **Scanner：** 自動漏洞掃描（僅限 Professional 付費版）。
* **特點：** 介面直觀，擁有豐富的擴充套件商店（BApp Store）。

### OWASP ZAP (Zed Attack Proxy)
* **地位：** 全球最受歡迎的**免費開源**替代品，由 OWASP 維護。
* **功能：** 提供類似 Burp 的攔截代理、主動/被動掃描器、蜘蛛爬蟲（Spider）。
* **特點：** 完全免費，支援自動化腳本，非常適合整合進 CI/CD 流程。

---

## 2. 資訊蒐集與偵察工具 (Reconnaissance)
在攻擊前，必須先了解目標的架構、開放端口與服務。

### Nmap (Network Mapper)
* **用途：** 網路探索與安全審計的神器。
* **功能：** 掃描主機開放的 Port、辨識作業系統版本 (OS Fingerprinting)、檢測防火牆/WAF。
* **常用指令：** `nmap -sV -p- <target_ip>`

### Gobuster / Dirb
* **用途：** 目錄與檔案枚舉（Directory Busting）。
* **功能：** 透過字典檔暴力掃描網站上隱藏的目錄與檔案（如 `/admin`, `/backup`, `.git`, `.env`）。
* **特點：** Gobuster 使用 Go 語言編寫，掃描速度極快。

---

## 3. 特定漏洞掃描工具 (Specific Vulnerability Scanners)
針對特定類型的漏洞進行深度檢測。

### SQLMap
* **用途：** SQL 注入（SQL Injection）檢測與利用的自動化工具。
* **功能：** 自動識別後端資料庫類型、提取數據庫資料、甚至獲取系統 Shell。
* **特點：** 功能強大，支援 MySQL, PostgreSQL, Oracle, MSSQL 等主流資料庫。

### Nikto
* **用途：** 網頁伺服器掃描器。
* **功能：** 掃描過時的伺服器版本、危險的 CGI 文件、錯誤的配置檔（如 `.htaccess` 暴露）。

### WPScan
* **用途：** 專門針對 WordPress CMS 的掃描器。
* **功能：** 檢測 WordPress 核心版本漏洞、枚舉使用者名稱、檢查有漏洞的外掛（Plugins）與佈景主題（Themes）。

---

## 4. 漏洞利用框架 (Exploitation Frameworks)
當發現漏洞後，用來驗證漏洞是否能被實際利用。

### Metasploit Framework (MSF)
* **用途：** 世界上最完整的漏洞利用開發與執行平台。
* **功能：** 內建數千種 Exploit（攻擊模組）和 Payload（攻擊載荷）。雖然常用於系統層級攻擊，但也包含大量 Web 應用模組（如 Tomcat, Jenkins, Struts2 等漏洞利用）。

### BeEF (The Browser Exploitation Framework)
* **用途：** 專注於客戶端（瀏覽器）的攻擊。
* **功能：** 透過 XSS 漏洞鉤住（Hook）受害者的瀏覽器，進而控制其行為或竊取資訊。

---

## 5. 工具比較：Burp Suite vs. OWASP ZAP

| 特性 | Burp Suite (Professional) | OWASP ZAP |
| :--- | :--- | :--- |
| **價格** | 昂貴 (年費訂閱制) | **完全免費 (開源)** |
| **易用性** | 介面精緻，使用者體驗極佳 | 介面較為複雜，功能雖多但需適應 |
| **自動化** | 強大的被動與主動掃描 | 優秀的 API，適合整合進 DevOps 流程 |
| **擴充性** | BApp Store 資源豐富 | Marketplace 亦有不少外掛 |
| **適用對象** | 專業滲透測試人員 | 初學者、開發者、預算有限的團隊 |

---

