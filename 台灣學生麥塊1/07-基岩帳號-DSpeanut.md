# 07 — 基岩版帳號 DSpeanut 資料

- **來源**：GeyserMC XUID API `https://api.geysermc.org/v2/xbox/xuid/DSpeanut`、Floodgate UUID 換算、後台日誌
- **時間**：2026-07-13（台北時間）

## 帳號資料

| 項目 | 值 |
|------|----|
| 基岩版玩家名 (gamertag) | DSpeanut |
| 遊戲內顯示名 | `.DSpeanut`（Floodgate 前綴 `.`） |
| XUID（GeyserMC API 查得） | `2535464041664476`（十進位）／`901fdb98b4fdc`（十六進位） |
| Floodgate UUID | `00000000-0000-0000-0009-01fdb98b4fdc` |
| 基岩版本 | 26.33（使用者回報） |
| 連線來源 IP | `118.150.197.230`（與屋主 Java 帳號同 IP） |

## Floodgate UUID 換算方式

基岩帳號沒有 Mojang UUID，Floodgate 以 `new UUID(0, xuid)` 產生專屬 UUID：

```
xuid            = 2535464041664476
xuid (hex,16位) = 0000901fdb98b4fdc  → 補零為 0009 01fdb98b4fdc
Floodgate UUID  = 00000000-0000-0000-0009-01fdb98b4fdc
```

> 因基岩帳號不能用 `maintenance add <名稱>`（該指令僅認 Mojang Java 帳號），故以 XUID 換算出的 Floodgate UUID 直接寫入 `WhitelistedPlayers.yml`，維修外掛才認得。

## 目前狀態

- 已在維修白名單中，維修期間可進入。
- 更換為經典造型後，已成功連線進入遊戲（見 `05-Geyser基岩版連線問題-處理紀錄.md`）。
