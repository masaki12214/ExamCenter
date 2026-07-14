# 07 · 技術診斷：CraftBlock 洗頻來源

- **資料來源**：使用者截圖（`CraftBlock{...}` 輸出）＋ `plugins/BetterSMPPlugin-1.0.0.jar` 內 `plugin.yml` 與位元碼字串反查
- **診斷時間**：2026-07-14

## 現象
畫面／主控台狂噴 `CraftBlock{pos=BlockPos(x,y,z), type=..., data=..., fluid=...}`，
內容為一小片方塊掃描（SLIME_BLOCK、STRIPPED_OAK_WOOD、TNT[unstable=false]、AIR…＝一台 TNT 複製機的方塊）。

## 定位結果
這是你們**自製插件**在洗頻。`BetterSMPPlugin-1.0.0.jar` 的 `plugin.yml`：
- `name: TSMPlugin`，`main: me.hina.tsm.BetterSMPPlugin`，作者 **Hina**
- 自帶技能／任務／官方商店／自訂附魔系統，並含 debug 命令 `haha` / `haha2`（權限 `tsm.commands.temp`）

**兇手類別：`me.hina.tsm.listeners.PlacedBlockListener`**，位元碼可見：
- `onPistonExtend(BlockPistonExtendEvent)`、`onPistonRetract(BlockPistonRetractEvent)`
- 取得被移動方塊清單 `getBlocks() : List<Block>`
- 呼叫 **`broadcast(String.valueOf(block))`**（`String.valueOf(Object)` → `CraftBlock.toString()`）

→ **每次活塞一動就全服廣播被移動的方塊**。TNT 複製機的活塞狂推 → 洗爆畫面。這是一行**忘記拿掉的 debug 廣播**。

## 解法
無設定檔可關（寫死在 jar）：
1. **正解（給 Hina）**：刪除 `PlacedBlockListener.onPistonExtend/onPistonRetract` 內的 debug `Bukkit.broadcast(...)`，或包 debug 開關，重編譯換 jar。
2. **臨時**：暫停 TSMPlugin（會連帶關技能/任務/商店，不建議），或先別開活塞機器。

> 此插件（TSMPlugin）與 08 篇的當機亦相關：其官方商店 GUI 點擊會同步觸發經濟存檔。
