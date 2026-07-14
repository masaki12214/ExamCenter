# 06 · 技術診斷：為何無法複製 TNT（正式服 ecadf15d）

- **資料來源**：`config/paper-global.yml`、`config/paper-world-defaults.yml`、`plugins/Insights/config.yml` 與 `limits/*.yml`、`plugins/ChunkEntityLimiter/config.yml`、`spigot.yml`
- **診斷時間**：2026-07-14

## 結論
**不是原版機制擋的，是兩個「防卡頓」插件在擋。**

## 排查過程

### 已排除：Paper 複製開關是開的 ✅
`config/paper-global.yml` → `unsupported-settings`：
```
allow-piston-duplication: true
allow-permanent-block-break-exploits: true
allow-headless-pistons: true
```
且 `paper-global.yml` 修改時間（04:00:37）＝當日開機時間（04:00:56），確認 `true` 已生效於運行中的伺服器（非未重啟）。`paper-world-defaults.yml` 無覆寫。

### 主因：Insights
`plugins/Insights/limits/redstone-limit.yml` 把一組限制為**每區塊 64 個**，清單含：
`PISTON、STICKY_PISTON、TNT、REDSTONE_WIRE、REPEATER、COMPARATOR、DISPENSER…`
且 `plugins/Insights/config.yml` → `apply-piston-limits: true`，並以 `BlockPistonExtendEvent: LOWEST` 攔截活塞。
→ 活塞推 TNT（受限方塊）時被攔截，**複製不觸發**；區塊紅石/活塞/TNT 超過 64 也放不下。

### 次因：ChunkEntityLimiter
`plugins/ChunkEntityLimiter/config.yml`：`default-limit: 100`（玩家附近 ×1.5 = 150），每 600 tick（30 秒）清理超出的實體。被點燃的 TNT 是實體、不在忽略清單 → 複製出來的 TNT 量一多就被清掉。

> Grim 反作弊（grimac-bukkit-2.3.74）為移動/戰鬥類，不涉紅石活塞，已排除。

## 開放方式（擇一／組合）
- **Insights**：移除 redstone-limit 中的 PISTON/STICKY_PISTON/TNT；或 `apply-piston-limits: false`；或發 `insights.bypass.limit.redstone` 權限；或提高 limit。
- **ChunkEntityLimiter**：把 TNT 加入 `ignored-types`，或提高 `default-limit`。

⚠️ 兩者本為防卡頓，TNT 複製機每 tick 狂生實體，全開恐拉高延遲。建議只在特定世界或特定玩家開放。

**（使用者決定：暫不修改，僅需知道原因。）**
