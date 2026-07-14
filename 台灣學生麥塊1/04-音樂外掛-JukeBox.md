# 04 — 音樂外掛（`/music` 指令所屬）

- **問題**：查「music 是什麼外掛」
- **來源**：`jukebox-1.20.15.jar` 內 `plugin.yml`、`plugins/JukeBox/config.yml`、SpigotMC 資源頁
- **擷取時間**：2026-07-13（台北時間）

## 結論

`/music` 不是獨立叫「music」的外掛，而是 **JukeBox** 外掛註冊的指令。

## 外掛資訊（讀自 jar 內 `plugin.yml`）

| 項目 | 內容 |
|------|------|
| 名稱 | JukeBox |
| **作者** | **SkytAsul** |
| 版本 | 1.20.15 |
| 主類別 | `fr.skytasul.music.JukeBox`（內部套件名 `music`，即 `/music` 的來源） |
| 描述 | A plugin which allows you to propose note block songs to your players. |
| 官方頁面 | https://www.spigotmc.org/resources/jukebox-music-plugin.40580/（資源 #40580） |
| 依賴 | NoteBlockAPI（必需）、PlaceholderAPI（選用） |
| 指令 | `/music`（別名 `/jukebox`）、`/adminmusic`（別名 `/amusic`） |
| 權限 | `music.*`（完整），含 `music.command`、`music.radio`、`music.favorites` 等 |

## 本伺服器的 JukeBox 設定（`plugins/JukeBox/config.yml`）

| 設定 | 值 | 說明 |
|------|----|------|
| `lang` | `tw` | 繁體中文介面 |
| `radio` | `true` | 開啟伺服器電台（全服同步播放） |
| `jukeboxClick` | `true` | 手持唱片點擊唱片機方塊開啟選單 |
| `reloadOnJoin` | `true` | 重新上線接續播放離線前曲目 |
| `noteParticles` / `actionBar` | `true` | 播放時有音符粒子與動作列提示 |
| `forceJoinMusic` / `radioOnJoin` | `false` | 不強制加入時播放 |

- 歌曲檔（`.nbs`）放在 `plugins/JukeBox/songs/`。
- 依賴外掛 NoteBlockAPI 版本為 1.7.0（`NoteBlockAPI-1.7.0.jar`）。
