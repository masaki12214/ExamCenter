# 台灣學生麥塊 1 — 伺服器資料與處理紀錄

本資料夾彙整了本次工作階段中，針對 Minecraft 伺服器「**台灣學生麥塊 1**」所蒐集到的所有資訊，以及所執行的維運操作與故障排除紀錄。

## 基本識別

| 項目 | 內容 |
|------|------|
| 伺服器名稱 | 台灣學生麥塊 1（`臺灣學生麥塊 1`） |
| 說明 | 正式服 |
| 面板 | Pterodactyl（`https://px.athebyne.io`） |
| 伺服器識別碼 | `ecadf15d` |
| 面板網址 | https://px.athebyne.io/server/ecadf15d |

## 檔案索引

| 檔案 | 內容 |
|------|------|
| [`01-伺服器基本資訊.md`](01-伺服器基本資訊.md) | 規格、節點、連接埠、egg 設定 |
| [`02-維修狀態與白名單.md`](02-維修狀態與白名單.md) | 維修模式、結束倒數、維修白名單變更 |
| [`03-外掛清單.md`](03-外掛清單.md) | 全部 69 個外掛 jar 與資料夾清單 |
| [`04-音樂外掛-JukeBox.md`](04-音樂外掛-JukeBox.md) | `/music` 指令所屬外掛的查證 |
| [`05-Geyser基岩版連線問題-處理紀錄.md`](05-Geyser基岩版連線問題-處理紀錄.md) | 基岩版進不去的完整診斷與修復 |
| [`06-本次工作變更彙總.md`](06-本次工作變更彙總.md) | 這次對伺服器做的所有變更（含還原方式） |

## 資料來源總覽

| 來源 | 用途 |
|------|------|
| Pterodactyl Client API（`https://px.athebyne.io/api/client/servers/ecadf15d`） | 伺服器詳情、資源狀態、檔案讀寫、指令、電源 |
| 伺服器後台日誌 `logs/latest.log` | 玩家連線、錯誤堆疊 |
| `plugins/Maintenance/*`（Maintenance 外掛 5.1.0） | 維修狀態、白名單 |
| `plugins/Geyser-Spigot/config.yml` | Geyser 設定 |
| 各外掛 jar 內 `plugin.yml` / `git.properties` | 外掛作者、版本 |
| GeyserMC 官方（`geysermc.org`、`download.geysermc.org`） | 最新版、支援版本 |
| GeyserMC XUID API（`api.geysermc.org`） | 基岩帳號 XUID 查詢 |

## 時間與版本註記

- **資料擷取時間**：2026-07-13（台北時間 UTC+8，依伺服器時鐘與後台日誌）。
- **本紀錄整理日期**：2026-07-14。
- 所有時間戳除另有註明外，皆為台北時間。

## 機敏資訊處理

以下項目屬於憑證/密鑰，**刻意不寫入本 repo**，以免進入版控後外洩：

- Pterodactyl Client API 金鑰（`ptlc_…`）
- Maintenance 外掛設定中的 Discord Webhook 網址

如需這些值，請直接在面板中查看。
