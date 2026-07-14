# 03 · yuiop（=Kevin）活動記錄稽核報告

- **資料來源**：Pterodactyl 面板 `/servers/{id}/activity?include=actor` API（含 SFTP／主控台／檔案／電源／資料庫事件）
- **擷取時間**：2026-07-12
- **對象**：yuiop，面板帳號 `0918150353yuioplcy`（= Kevin = 遊戲內 Kevi_28576）
- **對應 PDF**：[`reports/TSM_yuiop_活動記錄報告.pdf`](reports/TSM_yuiop_活動記錄報告.pdf)
- **原始資料**：[`data/正式服_ecadf15d_活動記錄.json`](data/正式服_ecadf15d_活動記錄.json)、[`data/主服_0bd99188_活動記錄.json`](data/主服_0bd99188_活動記錄.json)

## 總覽

| 指標 | 數值 |
|---|---|
| 操作總數 | 409 筆（主服 4 + 正式服 405） |
| 涵蓋期間 | 07/06 – 07/12 |
| 上傳外掛／函式庫 | ~110 個 |
| 開關機 | 22 次 |
| 主控台指令 | 42 條 |

**重點結論**：yuiop 幾乎所有操作集中在正式服（ecadf15d，405 筆），把它從空機**整套重建成正式營運服「臺灣學生麥塊 1」**。7/11 一天 222 筆、7/12 凌晨匯入整份世界 125 筆為最密集兩天。

## 一、主服 0bd99188（4 筆，07/06–07/07）

| 時間 | 類型 | 內容 |
|---|---|---|
| 07-06 23:27:04 | console | `op Kevi_28576` |
| 07-06 23:27:19 | rename | 「進階 - T0Bs #105」→「臺麥測試服」 |
| 07-06 23:27:35 | rename | 「臺麥測試服」→「臺麥測試服 [已公開]」 |
| 07-07 00:03:51 | file.read | 檢視 `/plugins/DiscordSRV/config.yml` |

## 二、正式服 ecadf15d（405 筆，07/06–07/12）

| 日期 | 筆數 | 主要工作 |
|---|---|---|
| 07-06 | 29 | 初始化；刪 EssentialsX + 35 項舊檔；裝 CMI/BlueMap/CoreProtect；改名「開發服」；新增端口 10041 |
| 07-07 | 12 | 資料庫重整（刪 s425_DataBase，建/刪 s425_plugin_data/s425_bluemap）；多次看 TAB 設定；重啟 |
| 07-08 | 11 | 整理端口備註（BlueMap／主端口／RCON）；新增端口 10340 |
| 07-09 | 5 | 新增 query 端口 10893 |
| 07-10 | 1 | 關機 |
| **07-11** | **222** | **大規模重建**（見下） |
| **07-12** | **125** | **01:34–02:02 匯入完整世界存檔**（約 5,900 檔：lobby/buildworld 維度＋玩家資料/統計/成就） |

### 7/11 重建細節

- 改名「開發服」→「**臺灣學生麥塊 1**」、描述「正式服」= 正式上線
- 清空舊環境（刪 root 下 27 項：bluemap、cache、config、libraries、logs、plugins…）
- 上傳約百餘外掛 + 函式庫（Eco 全家桶、Guilds、HuskHomes/Sync、Multiverse 5.7.1、WorldGuard、QuickShop、Skript、TAB v6、Grim 反作弊、Geyser…）
- 經濟重置 `money set/take -all`
- 權限：`lp editor`、多次 `applyedits`、`op Kevi_28576`、Kevi_28576 設 admin
- 世界：Multiverse 複製 survival_nether / survival_the_end、設 END 環境
- Skript：撰寫 `end_portal_fix.sk`（原版終界門導向生存終界），反覆 reload
- WorldGuard：重建多世界 region、多次 `wg reload`
- 7 次開關機循環；新增 Geyser / Plan / RCON 端口備註

## 操作類型分佈（正式服 405 筆）

| 類型 | 次數 | 類型 | 次數 | 類型 | 次數 |
|---|---|---|---|---|---|
| SFTP 建立 | 104 | 主控台指令 | 42 | 檔案上傳 | 5 |
| SFTP 改名 | 98 | 建立資料夾 | 40 | 檔案刪除 | 5 |
| SFTP 寫入 | 28 | 端口備註 | 24 | 資料庫操作 | 5 |
| SFTP 刪除 | 15 | 開/關機 | 22 | 改名/描述 | 3 |
| 檔案讀取 | 7 | 端口建立 | 6 | 其他 | 1 |
