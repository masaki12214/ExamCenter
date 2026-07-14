# 05 — 基岩版連線問題（Geyser）完整處理紀錄

- **問題**：基岩版帳號 **DSpeanut** 進不去，Java 帳號正常。
- **來源**：`logs/latest.log`、`plugins/Geyser-Spigot/config.yml`、GeyserMC 官方 API/wiki、`api.geysermc.org`
- **時間**：2026-07-13（台北時間）

## 症狀（後台錯誤）

Geyser 在 **pre-login** 階段丟出：

```
[Geyser-Spigot] Exception caught in session of unknown (pre-login)
io.netty.handler.codec.DecoderException: java.util.zip.DataFormatException: Inflated data exceeds maximum size
    at org.cloudburstmc.protocol.common.util.Zlib.inflate(Zlib.java:66)
    at ...bedrock.netty.codec.compression.ZlibCompression.decode
Bedrock user with ip: /118.150.197.230 has disconnected for reason An internal error occurred!
```

- 失敗來源 IP `118.150.197.230`。
- 同一 IP 的 Java 帳號 `masakigod214`（走 TCP）**可正常登入**（例：`17:36:13 masakigod214 ... logged in`）。

## 診斷過程與排除項

| 時間 | 動作 | 結果 |
|------|------|------|
| — | 讀日誌，確認 Java 正常、失敗者是基岩版 | 鎖定 Geyser pre-login 解壓縮錯誤 |
| ~17:31 | 更新 Geyser：`2.11.0-SNAPSHOT` → 官方最新 **2.11.0 build 1196**（2026-07-12 建置），重啟伺服器 | **未解決**，錯誤重現（17:33、17:34…） |
| — | 查 GeyserMC 支援版本（geysermc.org wiki）：支援 **Bedrock 26.0–26.33 / Java 26.2** | — |
| — | 使用者回報 DSpeanut 基岩版本為 **26.33**（在支援範圍內） | 排除「版本太新/太舊」 |
| ~17:41 | 調低 Bedrock MTU：`1400` → `1148`，`/geyser reload` | **未解決**，17:41:09 仍同錯 |
| ~17:40–17:41 | 觀察到另一基岩玩家 **technobladed151** 透過 Geyser **成功連入** | 證明伺服器/Geyser 對一般玩家正常 → 問題屬 DSpeanut 個人 |

## 根本原因

**DSpeanut 的基岩版造型（Persona / 複雜 Marketplace 造型）太大**，導致登入封包過大，Geyser 解壓縮超過上限而丟 `Inflated data exceeds maximum size`。這是 Geyser 的已知現象，用簡單造型的玩家不受影響（如 technobladed151 可正常連線）。

## 解法（有效）

請 DSpeanut 在 Minecraft 基岩版更衣室/個人檔案，將造型從 **Persona（角色創作）換成經典造型（Classic Skin，如內建 Steve/Alex）**，完全重開 App 再連線。

## 成功紀錄（後台日誌）

```
[17:41:50] [Geyser-Spigot] Player connected with username DSpeanut (1001)
[17:41:50] [Geyser-Spigot] DSpeanut (logged in as: DSpeanut) has connected to the Java server
[17:41:51] [floodgate] Floodgate player logged in as .DSpeanut joined
           (UUID: 00000000-0000-0000-0009-01fdb98b4fdc)
[17:41:51] .DSpeanut joined the game
[17:41:51] [ 經濟系統 ] ⏵ 已將 500.00 $ 添加給 .DSpeanut。
```

→ DSpeanut 成功進入遊戲，並領到新手 500$。

## 給日後的排錯備忘

若又有基岩玩家卡在「An internal error occurred」/ `Inflated data exceeds maximum size`：
1. 先確認是否只有該玩家、其他基岩玩家是否正常（判斷是全服或個人問題）。
2. 個人問題 → 請該玩家改用**經典造型**。
3. 全服問題 → 檢查 Geyser 是否過舊（`geysermc.org` 支援版本）、必要時更新並重啟。
