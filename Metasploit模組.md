# Metasploit Framework (MSF) 模組全解

Metasploit Framework (MSF) 的核心力量來自於各類型的**模組 (Modules)**。這些模組就像是積木，可以根據測試目標和需求進行組合。

MSF 的模組主要分為 **7 大類**，以下是詳細的分類說明與路徑對照。

---

## 一、七大模組分類詳解

### 1. Exploit (漏洞利用模組)
這是 Metasploit 最核心的部分。Exploit 是一段程式碼，用來利用目標系統、服務或應用程式中的特定安全漏洞。

* **功能：** 觸發漏洞，為 Payload（攻擊酬載）打開進入目標的大門。
* **命名規則：** `平台/服務/漏洞名稱`
* **範例：** `exploit/windows/smb/ms17_010_eternalblue` (永恆之藍)

### 2. Payload (攻擊酬載模組)
當 Exploit 成功利用漏洞後，Payload 是接著在目標系統上執行的程式碼。
* **功能：** 建立連線、開啟 Shell、執行指令等。
* **分類：**
    * **Singles (Inline):** 獨立且完整的程式碼，穩定但體積較大。
    * **Stagers:** 小型程式碼，負責建立連線並下載更大的 Stage。
    * **Stages:** 由 Stager 下載的完整功能組件（如 Meterpreter）。
* **範例：** `payload/windows/x64/meterpreter/reverse_tcp`

### 3. Auxiliary (輔助模組)
這類模組**不**是為了取得 Shell，而是用於攻擊前的偵查、掃描或攻擊後的輔助工作。
* **功能：** 端口掃描、服務列舉、弱密碼暴力破解、封包嗅探。
* **範例：**
    * `auxiliary/scanner/smb/smb_version` (掃描 SMB 版本)
    * `auxiliary/scanner/ssh/ssh_login` (SSH 暴力破解)

### 4. Post (後滲透模組)
當你已經成功入侵目標並取得 Session (如 Meterpreter) 後使用。
* **功能：** 權限提升 (Privilege Escalation)、竊取憑證 (Hash dumping)、蒐集系統資訊、清除軌跡。
* **注意：** 必須在已建立的 Session 中執行。
* **範例：** `post/windows/gather/hashdump`

### 5. Encoders (編碼模組)
* **功能：** 對 Payload 進行編碼（重新包裝）。
* **目的：**
    1.  **消除壞字元 (Bad Characters):** 避免 Shellcode 中出現 `\x00` 等導致溢位失敗的字元。
    2.  **規避偵測 (Evasion):** 改變特徵碼以嘗試繞過防毒軟體。
* **範例：** `encoder/x86/shikata_ga_nai`

### 6. Nops (空指令模組)
* **功能：** 產生一系列的 "No Operation" (NOP) 指令。
* **用途：** 用於緩衝區溢位攻擊，填充記憶體空間建立「滑動區」(NOP Sled)，增加 Payload 被 CPU 執行的機率。
* **範例：** `nop/x86/opty2`

### 7. Evasion (規避模組)
專門設計用來繞過現代端點防護 (Anti-Virus / EDR) 的模組。
* **功能：** 產生難以被偵測的可執行檔，結合混淆與加密技術。
* **範例：** `evasion/windows/windows_defender_exe`

---

## 二、模組路徑結構對照表

位於 Linux 系統 (Kali) 的 `/usr/share/metasploit-framework/modules/` 下：

| 模組類型 | 資料夾路徑 | 主要用途 |
| :--- | :--- | :--- |
| **Exploits** | `.../exploits/[platform]/[service]/` | 攻擊漏洞 |
| **Payloads** | `.../payloads/[singles/stagers/stages]/` | 建立連線與控制 |
| **Auxiliary** | `.../auxiliary/[category]/[service]/` | 掃描與偵查 |
| **Post** | `.../post/[platform]/[category]/` | 深度挖掘與控制 |
| **Encoders** | `.../encoders/[arch]/` | 編碼與混淆 |

---

## 三、常用指令速查 (msfconsole)

1.  **搜尋模組**
    ```bash
    search type:exploit platform:windows smb
    ```

2.  **選擇模組** ==> use 指令
    ```bash
    use exploit/windows/smb/ms17_010_eternalblue
    ```

3.  **查看說明**
    ```bash
    info
    ```

4.  **設定參數與執行**
    ```bash
    show options           # 查看需要的參數
    set RHOSTS 192.168.1.1 # 設定目標 IP
    set LHOST 192.168.1.5  # 設定攻擊機 IP
    run                    # 或 exploit
    ```
