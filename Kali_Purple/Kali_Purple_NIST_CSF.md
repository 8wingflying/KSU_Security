# Kali Purple 應用程式選單說明：Identify 階段

這份文件針對 Kali Purple 作業系統的應用程式選單截圖進行解析。該畫面展示了 **NIST 網路安全框架 (CSF)** 中的第一階段：**Identify (識別)**。

## 1. 什麼是 Kali Purple？
**Kali Purple** 是 Kali Linux 推出的一個特殊版本，其定位與傳統側重於滲透測試（紅隊）的 Kali 不同。Kali Purple 專注於 **防禦性安全（藍隊）** 和 **紫隊（紅藍對抗/協作）** 的工作流程。

---

## 2. 左側選單結構：NIST CSF 框架
Kali Purple 的選單依據防禦流程進行分類，左側最上方的五個項目對應 **NIST Cybersecurity Framework** 的核心功能：

* **001 - Identify (識別)**：*(目前畫面所在位置)* 盤點資產、識別風險。
* **002 - Protect (保護)**：部署防護措施。
* **003 - Detect (偵測)**：監控與發現異常。
* **004 - Recover (復原)**：災難復原與業務連續性。
* **005 - Respond (回應)**：事件應變處理。

> **備註**：下方的編號（01 - 13）則混合了 **MITRE ATT&CK** 框架的階段（如 Reconnaissance, Execution 等），方便從攻擊者視角測試防禦。

---

## 3. 右側工具列表解析 (Identify 階段)
此階段的目標是「了解你的環境、資產與潛在風險」。工具主要分為資產發現、弱點管理與情報蒐集。

### A. 資產發現與 OSINT (開源情報)
用於搜尋子網域、發現網路資產，了解暴露在外的攻擊面。
* **amass**：強大的子網域枚舉與資產發現工具。
* **assetfinder**：快速尋找相關網域與子網域。
* **maltego**：資料探勘與連結分析工具，可視覺化資產間的關係。
* **spiderfoot / spiderfoot-cli**：自動化 OSINT 工具，收集目標的各種情資。
* **maryam**：開源情報蒐集框架。 OWASP Maryam, a free and open-source Open-Source Intelligence (OSINT) framework for data gathering and web reconnaissance. 
* **witnessme**：用於擷取網站截圖並記錄 HTTP 標頭的工具（方便快速瀏覽大量網頁資產）。

### B. 弱點管理與追蹤
* **defectdojo / defectdojo-stop**：開源的弱點管理工具。
* 在紫隊演練中，這是核心平台，用來匯入、記錄並追蹤所有掃描到的漏洞修補進度。
* DefectDojo is a DevSecOps, ASPM (application security posture management), and vulnerability management tool. 
* DefectDojo orchestrates end-to-end security testing, vulnerability tracking, deduplication, remediation, and reporting.
* https://github.com/DefectDojo/django-DefectDojo

### C. 弱點掃描與配置審計
* **zaproxy (OWASP ZAP)**：世界知名的網頁應用程式弱點掃描器。
* **wapiti**：另一款網頁應用程式漏洞掃描器（黑箱測試）。
* **searchsploit**：用於離線搜尋 Exploit-DB 資料庫，確認資產是否存在已知的漏洞利用程式。
* **nipper**：網路基礎設施解析器，用於審計(稽核)防火牆、交換器等網路設備的配置安全性。
* **tiger**：Unix 系統安全掃描與審計(稽核)工具。

---

## 總結
這張畫面展示了建立防禦架構的第一步：**「盤點與識別」**。資安人員利用這些工具找出網路中所有的伺服器與服務，並建立弱點管理流程，以便後續進行保護與監控。

# Kali Purple | Protect 階段

這份文件針對 Kali Purple 作業系統的應用程式選單截圖進行解析。該畫面展示了 **NIST 網路安全框架 (CSF)** 中的第二階段：**Protect (保護)**。

## 1. 階段定義：Protect (保護)
在 NIST 框架中，繼「識別 (Identify)」資產與風險之後，「保護」階段的目標是 **制定並實施適當的防護措施**，以確保關鍵基礎設施服務的傳遞。此階段著重於限制或遏制潛在網路安全事件的影響。

此選單中的工具涵蓋了三個核心防護領域：**惡意軟體防護**、**資料加密**與**網路存取控制**。

---

## 2. 工具列表解析

### A. 端點與內容安全 (Endpoint Security)
* **clamscan**
    * **描述**：ClamAV 防毒引擎的命令列介面工具。
    * **功能**：用於掃描系統檔案、目錄或電子郵件附件，以偵測並移除病毒、木馬、惡意軟體及其他威脅。它是 Linux 伺服器上最常見的開源防毒解決方案。

### B. 資料安全與加密 (Data Security)
* **cryptsetup**
    * **描述**：用於設定磁碟加密的工具，方便管理 dm-crypt 後端。
    * **功能**：主要用於建立和管理 LUKS (Linux Unified Key Setup) 加密分區。
    * **防禦價值**：確保「靜態資料 (Data at Rest)」的機密性。即使物理設備（如硬碟、筆電）被竊取，攻擊者在沒有金鑰的情況下也無法讀取資料。

### C. 網路安全與存取控制 (Network Security)
* **fwbuilder (Firewall Builder)**
    * **描述**：一個跨平台的防火牆配置與管理圖形化介面 (GUI) 工具。
    * **功能**：讓管理者以物件導向的方式設計防火牆策略，並自動將其編譯為不同平台（如 iptables, pf, Cisco ACLs 等）可執行的規則集。
    * **防禦價值**：簡化複雜的網路存取控制規則設定，減少因配置錯誤導致的安全漏洞。

---

## 總結
雖然此畫面中的工具數量較少，但它們精準地代表了防禦架構中的三大支柱：
1. **Clamscan**：防止惡意程式碼執行。
2. **Cryptsetup**：防止資料外洩。
3. **Fwbuilder**：防止未經授權的網路存取。

## 2. 003 - Detect (偵測階段)
此階段目標為制定並實施適當的活動，以識別網路安全事件的發生。工具重點在於**日誌鑑識**與**主動誘捕**。

### A. Windows 日誌鑑識工具 (GrokEVT Suite)
這是一套在 Linux 環境下分析 Windows 事件日誌 (Event Logs) 的腳本集合，常用於事後鑑識 (Forensics)。

* **grokevt-builddb**：讀取 Windows 登錄檔 (Registry) 與 PE 檔案，建立解析日誌所需的資料庫。
* **grokevt-parselog**：核心工具，利用上述資料庫來解析 `.evt` 日誌檔，將其轉換為人類可讀的文字格式。
* **grokevt-findlogs / addlog / ripdll**：輔助工具，用於尋找日誌檔、手動添加日誌或從 DLL 中提取訊息資源。
* **偵測價值**：協助分析師在不啟動受駭 Windows 系統的情況下，檢查歷史紀錄以發現異常登入、權限變更或惡意程式執行的痕跡。

### B. 主動式威脅偵測 (Honeypot)
* **sentrypeer**
    * **類型**：SIP (VoIP) 蜜罐 / 威脅情資
    * **功能**：一個點對點 (P2P) 的分散式蜜罐，專門模擬 VoIP 伺服器。
    * **偵測價值**：主動偵測針對網路電話系統的掃描與攻擊（如盜打電話詐欺、暴力破解）。它會記錄攻擊來源 IP 並與社群共享，提供即時的威脅預警。

---

## 總結
這兩個選單展示了防禦者的不同思維：
1.  **Protect**：是被動的「加固」，透過加密、防火牆和防毒來建立防線。
2.  **Detect**：是主動的「感知」，透過分析過去的日誌 (GrokEVT) 或設置陷阱 (SentryPeer) 來發現敵人是否已經入侵或正在嘗試入侵。

## 1. 004 - Recover (復原階段)
此階段的目標是**「恢復因資安事件而受損的功能或服務」**。
在 Kali Purple 中，這個選單主要包含**資料救援 (Data Recovery)** 與**檔案系統修復**的工具。當遭受勒索軟體攻擊、惡意刪除或系統損毀時，這些工具是最後的救命稻草。

### 核心工具列表
* **ddrescue**
    * **功能**：強大的資料救援工具。
    * **用途**：它可以從損壞的硬碟或有壞軌的儲存裝置中複製資料。它會嘗試略過讀取錯誤的部分，盡可能搶救出可讀取的數據，是製作受損硬碟映像檔的首選工具。
    * **復原價值**：災難復原 (Disaster Recovery)。

* **extundelete / ext3grep / ext4magic**
    * **功能**：針對 Linux 檔案系統 (ext3/ext4) 的檔案救援工具。
    * **用途**：透過分析檔案系統的日誌 (Journal)，嘗試復原被 `rm` 指令誤刪或被惡意程式刪除的檔案。
    * **復原價值**：誤刪資料恢復。

* **recoverjpeg / foremost / scalpel**
    * **功能**：檔案雕刻 (File Carving) 工具。
    * **用途**：即使檔案系統結構已經嚴重損毀（例如硬碟被格式化），這些工具仍能透過識別檔案標頭（如 JPEG, PDF 的特定二進位特徵）直接從磁碟原始數據中「雕刻」出檔案。

---

## 3. 004 - Recover (復原階段)
**目標**：恢復因資安事件而受損的功能或服務，重點在於資料搶救。

### A. 磁碟映像與災難救援 (處理壞軌)
* **dd_rescue**：強大的資料複製工具，能處理讀取錯誤，適合從受損硬碟製作映像檔。
* **myrescue**：類似 dd_rescue，專為救援有大量壞軌的硬碟設計，策略是先讀取好的區塊，最後再嘗試壞區塊。
* **recoverdm**：專門用於救援有壞軌的磁碟或光碟。

### B. Linux 檔案系統救援 (誤刪復原)
* **extundelete**：利用 ext3/ext4 分區的日誌 (journal) 來復原被刪除的檔案。
* **ext4magic** / **ext3grep**：針對 ext4 與 ext3 檔案系統的高階救援工具，可依時間點或目錄結構復原檔案。

### C. 特定系統與格式救援
* **scrounge-ntfs**：資料救援工具，專門從損毀的 Windows NTFS 分區中搶救資料。
* **undbx**：郵件救援工具，用於從損壞的 Outlook Express DBX 檔案中提取電子郵件。
* **recoverjpeg**：檔案雕刻 (File Carving) 工具，忽略檔案系統結構，直接掃描磁碟以找回 JPEG 圖片。

---

## 2. 005 - Respond (回應階段)
此階段的目標是**「針對已偵測到的資安事件採取行動」**。
這不僅僅是阻擋攻擊，更包含了**事件管理 (Incident Management)**、**協同作業**與**分析**。Kali Purple 在此階段引入了完整的 SOC (資安監控中心) 平台。

### 核心平台與工具
* **TheHive**
    * **類型**：資安事件回應平台 (Security Incident Response Platform, SIRP)。
    * **功能**：這是 Kali Purple "Respond" 階段的核心靈魂。它提供了一個 Web 介面，讓資安分析師可以：
        * **建立案卷 (Cases)**：記錄每一個資安事件的詳細資訊。
        * **指派任務**：團隊成員分工合作（如：一人分析惡意程式，一人檢查防火牆日誌）。
        * **整合分析**：通常與 Cortex 引擎搭配，自動分析可疑 IP 或網域。
    * **回應價值**：將零散的調查工作流程化、標準化，確保團隊能有效率地處理威脅。

* **Forensics Tools (鑑識工具)**
    * 雖然許多鑑識工具位於 "Detect" 或 "Identify"，但在回應階段，分析師需要深入調查「攻擊者到底做了什麼？」。
    * **Autopsy**：數位鑑識平台，用於分析受駭主機的硬碟映像檔。
    * **OllyDbg / Ghidra**：如果回應過程中捕獲了惡意程式樣本，逆向工程工具可用於分析其行為以制定阻擋策略。
## 4. 005 - Respond (回應階段)
**目標**：針對已偵測到的資安事件採取行動。此階段工具涵蓋**數位鑑識 (Forensics)**、**逆向工程**與**網路分析**。
*(參考圖片: image_58d0eb.jpg)*

### A. 數位證據取證 (Acquisition)
* **dc3dd**：加強版的 `dd` 指令，具備雜湊驗證功能，用於製作具有法律效力的磁碟映像檔。
* **ewfacquire**：用於獲取 EWF (Expert Witness Format) 格式的磁碟映像，這是鑑識軟體通用的格式。
* **guymager**：圖形化的磁碟鑑識映像檔製作工具，速度快且介面友善。

### B. 檔案與系統鑑識 (File & System Forensics)
* **foremost**：經典的檔案雕刻工具，根據檔案標頭特徵從映像檔中復原資料。
* **galleta**：專門用於分析與提取 Internet Explorer Cookie 資訊的鑑識工具。
* **icat / ils**：屬於 The Sleuth Kit 工具集，用於查看檔案系統的 Inode 與區塊資訊。
* **mac-robber / mactime**：用於建立與分析檔案系統的時間軸 (Timeline)，追蹤檔案的修改、存取與改變時間 (MAC times)。
* **hashrat**：支援多種演算法的雜湊計算工具，用於驗證檔案完整性。

### C. 惡意程式分析與逆向工程 (Malware Analysis)
* **ghidra**：由 NSA 開發的強大開源逆向工程框架，用於分析惡意程式碼。
* **ollydbg**：經典的 x86 組合語言除錯器，常用於動態分析惡意軟體。
* **yara**：惡意軟體特徵比對工具，用來分類與識別惡意樣本。
* **rkhunter (Rootkit Hunter)**：掃描系統中是否存在 Rootkit、後門程式與可疑漏洞。

### D. 網路與流量分析 (Network Analysis)
* **wireshark**：世界標準的網路封包分析工具，用於深入檢查網路流量中的攻擊痕跡。
* **netsniff-ng**：高效能的網路嗅探器與封包分析工具包。
* **impacket-scripts**：一組強大的 Python 腳本，常用於與網路協定互動（如 SMB, Kerberos），既可用於攻擊也可用於驗證網路行為。
---

## 總結：Kali Purple 的 NIST 完整流程

透過這五個選單 (001-005)，Kali Purple 試圖為防禦者建立一個完整的作業流程：

1.  **Identify (識別)**：用 `Nmap`, `Amass` 知道自己有哪些資產。
2.  **Protect (保護)**：用 `Firewall Builder`, `ClamAV` 建立防線。
3.  **Detect (偵測)**：用 `Suricata` (IDS), `GrokEVT` 發現異常。
4.  **Respond (回應)**：用 `TheHive` 開立案件並協調團隊處理攻擊。
5.  **Recover (復原)**：用 `ddrescue` 救回被破壞的資料。

這就是 Kali Purple 作為 "SOC In-A-Box" (盒裝資安監控中心) 的設計理念。
