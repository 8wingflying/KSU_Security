# Nmap 常用指令速查表 (Nmap Cheatsheet)

Nmap (Network Mapper) 是網路掃描與安全審計的標準工具。
**語法格式：** `nmap [掃描類型] [選項] {目標規格}`

---

## 1. 目標指定 (Target Specification)
如何指定要掃描的 IP 或網段。

| 指令 | 說明 |
| :--- | :--- |
| `nmap 192.168.1.1` | 掃描單一 IP |
| `nmap 192.168.1.1-50` | 掃描 IP 範圍 (1 到 50) |
| `nmap 192.168.1.0/24` | 掃描整個 CIDR 子網段 (256 個 IP) |
| `nmap -iL targets.txt` | **從檔案匯入目標清單** (最常用於批量掃描) |
| `nmap --exclude 192.168.1.5` | 排除特定 IP 不掃描 |

---

## 2. 主機發現 (Host Discovery)
在進行端口掃描前，先確認哪些主機是「存活」的。

| 指令 | 說明 |
| :--- | :--- |
| `nmap -sn 192.168.1.0/24` | **Ping 掃描** (不掃描端口)，僅列出存活主機 (舊版為 -sP) |
| `nmap -Pn 192.168.1.1` | **跳過主機發現** (假設主機在線)。當目標防火牆阻擋 Ping 時使用 |
| `nmap -PS 80,443` | 使用 TCP SYN 封包探測主機 (穿透防火牆常用技巧) |

---

## 3. 端口掃描技術 (Port Scanning Techniques)
決定如何探測端口狀態（Open, Closed, Filtered）。

| 指令 | 說明 |
| :--- | :--- |
| `nmap -sS <target>` | **TCP SYN 掃描** (半開放掃描)。**預設且最常用**，速度快、隱蔽性較高，不建立完整連線 |
| `nmap -sT <target>` | **TCP Connect 掃描**。建立完整連線，會在目標日誌留下紀錄 (當沒有 Root 權限時使用) |
| `nmap -sU <target>` | **UDP 掃描**。掃描 DNS (53), SNMP (161) 等 UDP 服務，速度極慢 |
| `nmap -p 80,443 <target>` | 僅掃描特定端口 |
| `nmap -p- <target>` | **全端口掃描** (掃描 1-65535 所有端口)，非常花時間但能避免遺漏 |
| `nmap -F <target>` | 快速掃描 (僅掃描最常見的 100 個端口) |

---

## 4. 服務與版本偵測 (Service & OS Detection)
獲取更詳細的目標資訊。

| 指令 | 說明 |
| :--- | :--- |
| `nmap -sV <target>` | **版本偵測**。探測服務具體版本 (如 Apache 2.4.41) |
| `nmap -O <target>` | **作業系統偵測**。猜測目標 OS (如 Windows, Linux) |
| `nmap -A <target>` | **綜合掃描**。同時啟用 OS 偵測、版本偵測、腳本掃描與 Traceroute (資訊量大，易被發現) |

---

## 5. 效能與時序 (Timing & Performance)
控制掃描速度以規避防火牆或加快速度。

| 指令 | 說明 |
| :--- | :--- |
| `nmap -T0` 到 `-T5` | 設定掃描速度模板。預設為 T3。 |
| `nmap -T4 <target>` | **推薦速度**。比預設快，適合現代寬頻網路環境 |
| `nmap -T1 <target>` | 非常慢 (Sneaky)，用於躲避 IDS/IPS 偵測 |
| `nmap --min-rate 1000` | 強制每秒至少發送 1000 個封包 (高速掃描用) |

---

## 6. Nmap 腳本引擎 (NSE - Nmap Scripting Engine)
使用內建腳本進行漏洞檢測。

| 指令 | 說明 |
| :--- | :--- |
| `nmap -sC <target>` | 使用**預設腳本**集合 (Default scripts) |
| `nmap --script=vuln <target>` | **漏洞掃描**。檢測常見漏洞 (如 CVE) |
| `nmap --script=http-title <target>` | 僅獲取網頁標題 |
| `nmap --script=auth <target>` | 嘗試枚舉認證資訊 |

---

## 7. 輸出格式 (Output)
保存掃描結果以便後續分析或報告使用。

| 指令 | 說明 |
| :--- | :--- |
| `nmap -oN output.txt` | 輸出為標準文字檔 (Normal format) |
| `nmap -oX output.xml` | 輸出為 XML 格式 (可匯入 Metasploit 或 Zenmap) |
| `nmap -oA scan_result` | **全格式輸出**。同時建立 .nmap, .xml, .gnmap 三種檔案 |

---

## 🚀 實戰常用組合 (Best Practice Combos)

**1. 快速列舉網段內存活主機：**
```bash
nmap -sn -T4 192.168.1.0/24
```

這是一份整理好的 Nmap 常用指令速查表 (Cheatsheet)。我將其組織為 Markdown 格式，您可以直接複製保存為 nmap_cheatsheet.md。

Markdown

# Nmap 常用指令速查表 (Nmap Cheatsheet)

Nmap (Network Mapper) 是網路掃描與安全審計的標準工具。
**語法格式：** `nmap [掃描類型] [選項] {目標規格}`

---

## 1. 目標指定 (Target Specification)
如何指定要掃描的 IP 或網段。

| 指令 | 說明 |
| :--- | :--- |
| `nmap 192.168.1.1` | 掃描單一 IP |
| `nmap 192.168.1.1-50` | 掃描 IP 範圍 (1 到 50) |
| `nmap 192.168.1.0/24` | 掃描整個 CIDR 子網段 (256 個 IP) |
| `nmap -iL targets.txt` | **從檔案匯入目標清單** (最常用於批量掃描) |
| `nmap --exclude 192.168.1.5` | 排除特定 IP 不掃描 |

---

## 2. 主機發現 (Host Discovery)
在進行端口掃描前，先確認哪些主機是「存活」的。

| 指令 | 說明 |
| :--- | :--- |
| `nmap -sn 192.168.1.0/24` | **Ping 掃描** (不掃描端口)，僅列出存活主機 (舊版為 -sP) |
| `nmap -Pn 192.168.1.1` | **跳過主機發現** (假設主機在線)。當目標防火牆阻擋 Ping 時使用 |
| `nmap -PS 80,443` | 使用 TCP SYN 封包探測主機 (穿透防火牆常用技巧) |

---

## 3. 端口掃描技術 (Port Scanning Techniques)
決定如何探測端口狀態（Open, Closed, Filtered）。

| 指令 | 說明 |
| :--- | :--- |
| `nmap -sS <target>` | **TCP SYN 掃描** (半開放掃描)。**預設且最常用**，速度快、隱蔽性較高，不建立完整連線 |
| `nmap -sT <target>` | **TCP Connect 掃描**。建立完整連線，會在目標日誌留下紀錄 (當沒有 Root 權限時使用) |
| `nmap -sU <target>` | **UDP 掃描**。掃描 DNS (53), SNMP (161) 等 UDP 服務，速度極慢 |
| `nmap -p 80,443 <target>` | 僅掃描特定端口 |
| `nmap -p- <target>` | **全端口掃描** (掃描 1-65535 所有端口)，非常花時間但能避免遺漏 |
| `nmap -F <target>` | 快速掃描 (僅掃描最常見的 100 個端口) |

---

## 4. 服務與版本偵測 (Service & OS Detection)
獲取更詳細的目標資訊。

| 指令 | 說明 |
| :--- | :--- |
| `nmap -sV <target>` | **版本偵測**。探測服務具體版本 (如 Apache 2.4.41) |
| `nmap -O <target>` | **作業系統偵測**。猜測目標 OS (如 Windows, Linux) |
| `nmap -A <target>` | **綜合掃描**。同時啟用 OS 偵測、版本偵測、腳本掃描與 Traceroute (資訊量大，易被發現) |

---

## 5. 效能與時序 (Timing & Performance)
控制掃描速度以規避防火牆或加快速度。

| 指令 | 說明 |
| :--- | :--- |
| `nmap -T0` 到 `-T5` | 設定掃描速度模板。預設為 T3。 |
| `nmap -T4 <target>` | **推薦速度**。比預設快，適合現代寬頻網路環境 |
| `nmap -T1 <target>` | 非常慢 (Sneaky)，用於躲避 IDS/IPS 偵測 |
| `nmap --min-rate 1000` | 強制每秒至少發送 1000 個封包 (高速掃描用) |

---

## 6. Nmap 腳本引擎 (NSE - Nmap Scripting Engine)
使用內建腳本進行漏洞檢測。

| 指令 | 說明 |
| :--- | :--- |
| `nmap -sC <target>` | 使用**預設腳本**集合 (Default scripts) |
| `nmap --script=vuln <target>` | **漏洞掃描**。檢測常見漏洞 (如 CVE) |
| `nmap --script=http-title <target>` | 僅獲取網頁標題 |
| `nmap --script=auth <target>` | 嘗試枚舉認證資訊 |

---

## 7. 輸出格式 (Output)
保存掃描結果以便後續分析或報告使用。

| 指令 | 說明 |
| :--- | :--- |
| `nmap -oN output.txt` | 輸出為標準文字檔 (Normal format) |
| `nmap -oX output.xml` | 輸出為 XML 格式 (可匯入 Metasploit 或 Zenmap) |
| `nmap -oA scan_result` | **全格式輸出**。同時建立 .nmap, .xml, .gnmap 三種檔案 |

---

## 🚀 實戰常用組合 (Best Practice Combos)

**1. 快速列舉網段內存活主機：**
```bash
nmap -sn -T4 192.168.1.0/24
```
**2. 標準滲透測試起手式 (掃描版本、OS、預設腳本)：

```Bash

nmap -sV -sC -O -T4 192.168.1.5
```
**3. 全端口深度掃描 (不遺漏任何服務)：

```Bash

nmap -p- -sV -T4 192.168.1.5
```
**4. 掃描特定漏洞 (例如 SMB 漏洞)：

```Bash

nmap -p 445 --script=smb-vuln* 192.168.1.5
```
