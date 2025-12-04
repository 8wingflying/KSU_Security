# Kali Purple 作業系統

## 1. 什麼是 Kali Purple？

**Kali Purple** 是 Offensive Security (OffSec) 於 2023 年推出的版本，與傳統專注於滲透測試（紅隊）的 Kali Linux 不同，Kali Purple 專門為 **防禦型安全（藍隊/紫隊）** 設計。

* **核心概念：** SOC In-A-Box (盒裝安全營運中心)。
* **目標用戶：** 藍隊分析師 (Blue Teamers)、SOC 分析師、資安學生、紫隊演練人員。
* **設計架構：** 基於 **NIST CSF (網路安全框架)** 進行構建。

---

## 2. 選單架構：NIST 五大支柱

Kali Purple 的應用程式選單不再按「攻擊類型」分類，而是依循防禦框架：

1.  **Identify (識別):** 資產盤點、弱點掃描 (工具：GVM/Greenbone)。
2.  **Protect (保護):** 防火牆配置、存取控制 (工具：ClamAV, Firewall Builder)。
3.  **Detect (偵測):** 入侵偵測系統、流量分析 (工具：Suricata, Zeek, Snort)。
4.  **Respond (回應):** 事件回應、取證工具 (工具：TheHive, Cortex)。
5.  **Recover (復原):** 系統備份與災難復原工具。

---

## 3. 核心架構與工具

Kali Purple 內建完整的實驗室架構，包含以下關鍵元件：

### A. The "Kali Purple" Stack (防禦核心)
預先配置好的環境，用於練習日誌分析和威脅獵捕：
* **Elasticsearch / Logstash / Kibana (ELK Stack):** 用於收集、解析和視覺化日誌 (SIEM)。
* **Arkime (前身為 Moloch):** 全封包擷取 (Full Packet Capture) 與索引系統，用於網路流量回溯分析。
* **CyberChef:** 「網路瑞士刀」，用於解碼、解密和數據轉換。

### B. 流量與分析工具
* **Suricata / Zeek:** 高階 IDS/IPS (入侵偵測/防禦系統)。
* **Wireshark:** 封包分析神器。
* **Malcolm:** 強大的網路流量分析工具套件 (通常透過 Docker 部署)。

---

## 4. 安裝與系統需求

由於運行大量的分析服務 (如 Elastic Stack)，硬體需求比標準版 Kali 高。

### 建議配置
* **CPU:** 4 核心以上
* **RAM:** 至少 8GB (建議 16GB 以運行完整 ELK)
* **硬碟:** 60GB 以上 (日誌檔案需佔用空間)

### 安裝簡述
1.  前往 [Kali.org](https://www.kali.org/get-kali/#kali-installer-images) 下載 **Kali Purple** ISO 檔。
2.  建議使用虛擬機 (VMware/VirtualBox) 安裝。
3.  安裝過程與標準 Debian/Kali Linux 相同。

---

## 5. 實戰學習路徑

### 第一階段：建立防禦實驗室 (Kali Purple Architecture)
* **目標：** 成功啟動並登入 Kibana 儀表板。
* **操作：** 運行 `kali-purple-install` (或相關 setup scripts) 來部署防禦環境。

### 第二階段：流量分析練習
* **操作：** 1. 使用 `tcpdump` 或 Wireshark 抓取流量。
    2. 將流量匯入 **Arkime**。
    3. 練習從封包中找出異常連線 (如非標準埠口的傳輸)。

### 第三階段：紫隊演練 (Purple Teaming)
* **操作：**
    1. **攻擊 (紅隊):** 使用 Metasploit/Nmap 對 VM 進行輕微掃描。
    2. **防禦 (藍隊):** 查看 Suricata 或 Kibana 是否偵測到行為。
    3. **優化:** 調整 IDS 規則並再次測試。

---

## 6. 常用指令備忘錄

| 功能 | 指令/工具 | 說明 |
| :--- | :--- | :--- |
| **更新系統** | `sudo apt update && sudo apt full-upgrade -y` | 保持工具最新 |
| **啟動 OpenVAS** | `gvm-start` | 啟動弱點掃描服務 |
| **啟動 Elastic** | `sudo systemctl start elasticsearch` | 啟動 SIEM 核心 |
| **流量分析** | `arkime` | 啟動全封包分析介面 |

---

> **免責聲明：** 本文件僅供教育與學術研究用途，請勿用於任何非法活動。
