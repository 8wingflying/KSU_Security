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

---

**1. 快速列舉網段內存活主機：**
```bash
nmap -sn -T4 192.168.1.0/24
```
---

**2. 標準滲透測試起手式 (掃描版本、OS、預設腳本)：

```Bash

nmap -sV -sC -O -T4 192.168.1.5
```

---

**3. 全端口深度掃描 (不遺漏任何服務)：

```Bash

nmap -p- -sV -T4 192.168.1.5
```

---

**4. 掃描特定漏洞 (例如 SMB 漏洞)：

```Bash

nmap -p 445 --script=smb-vuln* 192.168.1.5
```


## python-nmap
- 設計一個簡單的 **Python 腳本範例**，展示如何使用 `python-nmap` 庫來自動化執行這些掃描並解析結果
```python
import sys
!apt-get update
!apt-get install -y nmap
!pip install python-nmap
import nmap

def run_scanner(target_ip):
    # 初始化 Nmap PortScanner 物件
    nm = nmap.PortScanner()

    print(f"[*] 正在掃描目標: {target_ip} ... (這可能需要幾分鐘)")

    try:
        # 執行掃描
        # arguments: 指定 nmap 參數
        # -sV: 版本偵測, -T4: 加快速度, -F: 快速模式(僅掃描常見100個端口)
        result = nm.scan(hosts=target_ip, arguments='-sV -T4 -F')

    except nmap.PortScannerError as e:
        print(f"[!] Nmap 執行錯誤: {e}")
        sys.exit(0)
    except Exception as e:
        print(f"[!] 發生未預期錯誤: {e}")
        sys.exit(0)

    # 檢查是否有掃描到主機
    if not nm.all_hosts():
        print("[-] 未發現存活主機或主機屏蔽了掃描。")
        return

    # 解析並列印結果
    for host in nm.all_hosts():
        print("-" * 50)
        print(f"目標主機: {host} ({nm[host].hostname()})")
        print(f"狀態: {nm[host].state()}")

        # 遍歷所有協議 (TCP/UDP)
        for proto in nm[host].all_protocols():
            print(f"\n協議: {proto.upper()}")

            # 獲取該協議下所有開放的端口並排序
            lport = nm[host][proto].keys()
            sorted_ports = sorted(lport)

            for port in sorted_ports:
                # 獲取端口詳細資訊
                port_info = nm[host][proto][port]
                state = port_info['state']
                name = port_info['name']
                version = port_info['version']
                product = port_info['product']

                # 格式化輸出
                print(f"    Port: {port}\tState: {state}\tService: {name}")
                if product or version:
                    print(f"        └─ Version: {product} {version}")

    print("-" * 50)
    print("[*] 掃描完成")

if __name__ == "__main__":
    # 範例目標 (也可以改為 input 讓使用者輸入)
    target = input("請輸入要掃描的 IP 或網域: ")
    if target:
        run_scanner(target)
    else:
        print("未輸入目標，程式結束。")
```

- 輸入 ==> scanme.nmap.org

## 實作 網頁版 Nmap 掃描器
- 使用 Streamlit 撰寫一個簡單的網頁版 Nmap 掃描器，讓沒有 CLI 經驗的人也能用。
- Streamlit Nmap 掃描器程式碼 (web_scanner.py

```python
import streamlit as st
import nmap
import pandas as pd
import socket
from datetime import datetime

# 設定網頁標題與佈局
st.set_page_config(page_title="簡易 Nmap 網頁掃描器", page_icon="🔍", layout="wide")

st.title("🔍 簡易 Nmap 網頁掃描器")
st.markdown("讓沒有 CLI 經驗的人也能輕鬆進行網路安全掃描。")

# --- 側邊欄：設定掃描參數 ---
st.sidebar.header("⚙️ 掃描設定")

target = st.sidebar.text_input("輸入目標 IP 或網域", "scanme.nmap.org")

# 定義掃描模式對應的參數 (這就是讓小白好用的關鍵)
scan_profiles = {
    "🚀 快速掃描 (最常用)": "-F -T4",
    "📝 服務版本偵測 (標準)": "-sV -T4",
    "🛡️ 漏洞腳本掃描 (進階)": "-sV --script=vuln",
    "🐢 慢速隱蔽掃描 (躲避偵測)": "-T1",
    "🌐 全端口掃描 (1-65535)": "-p- -T4"
}

mode = st.sidebar.selectbox("選擇掃描模式", list(scan_profiles.keys()))
arguments = scan_profiles[mode]

start_scan = st.sidebar.button("開始掃描")

# --- 主程式邏輯 ---

def run_scan(target_ip, scan_args):
    nm = nmap.PortScanner()
    try:
        # 解析域名為 IP (如果是域名的話)
        ip_address = socket.gethostbyname(target_ip)
        
        # 執行掃描
        nm.scan(ip_address, arguments=scan_args)
        return nm
    except Exception as e:
        st.error(f"發生錯誤: {e}")
        return None

if start_scan:
    if not target:
        st.warning("請輸入目標 IP！")
    else:
        with st.spinner(f"正在掃描 {target} ... 請稍候 (模式: {mode})"):
            # 記錄開始時間
            start_time = datetime.now()
            
            # 執行掃描函數
            nm_result = run_scan(target, arguments)
            
            if nm_result and nm_result.all_hosts():
                host = list(nm_result.all_hosts())[0] # 取第一個主機
                
                # 計算耗時
                duration = datetime.now() - start_time
                st.success(f"掃描完成！耗時: {duration}")

                # --- 顯示主機摘要資訊 ---
                col1, col2, col3 = st.columns(3)
                with col1:
                    st.metric("目標 IP", host)
                with col2:
                    status = nm_result[host].state()
                    st.metric("主機狀態", status, delta="Online" if status=='up' else "Offline")
                with col3:
                    # 嘗試獲取主機名
                    hostname = nm_result[host].hostname()
                    st.metric("主機名稱", hostname if hostname else "Unknown")

                # --- 整理端口數據為 DataFrame 表格 ---
                ports_data = []
                
                # 檢查是否有 TCP 協議的掃描結果
                if 'tcp' in nm_result[host]:
                    for port, info in nm_result[host]['tcp'].items():
                        ports_data.append({
                            "Port": port,
                            "State": info['state'],
                            "Service": info['name'],
                            "Product": info.get('product', ''),
                            "Version": info.get('version', '')
                        })
                
                if ports_data:
                    df = pd.DataFrame(ports_data)
                    st.subheader("📊 開放端口列表")
                    
                    # 使用 Streamlit 的互動式表格
                    st.dataframe(
                        df, 
                        use_container_width=True,
                        column_config={
                            "Port": st.column_config.NumberColumn(format="%d"),
                            "State": "狀態",
                            "Service": "服務名稱",
                            "Product": "軟體",
                            "Version": "版本號"
                        }
                    )
                    
                    # --- 下載報告功能 ---
                    csv = df.to_csv(index=False).encode('utf-8')
                    st.download_button(
                        label="📥 下載 CSV 掃描報告",
                        data=csv,
                        file_name=f'scan_result_{host}.csv',
                        mime='text/csv',
                    )
                else:
                    st.info("未發現開放的 TCP 端口 (或者是被防火牆阻擋)。")
                
                # --- 顯示原始 JSON (給進階使用者看) ---
                with st.expander("查看原始 Nmap JSON 數據"):
                    st.json(nm_result[host])
                    
            else:
                st.error("掃描失敗或主機未回應 (Host Down)。請檢查目標是否正確或防火牆設定。")

# 頁尾
st.divider()
st.caption("⚠️ 免責聲明：本工具僅供授權測試與教育用途，請勿用於非法入侵。")
```
