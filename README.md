# Centralized Edit History (local fork)

中文 | English | Français

——

中文（用户指南）：
- 插件将各笔记的历史统一保存在 `/.obsidian/centralized-edit-history`，不再把历史散落在笔记目录中。
- 支持中文 / 英语 / 法语界面，可在设置中切换。

核心功能（改进版）：
- 外部重命名自动接管历史：在资源管理器重命名或移动笔记时，旧历史会被归档为孤立记录，新文件创建或打开时自动“领养”历史，避免断档。
- 孤立历史一键清理与领养：命令把无对应笔记的 `.ceh` 归档到 `/_ORPHAN`，并为当前笔记按同名或内容匹配自动领养。
- 打开即自动领养：打开一个没有历史的笔记，插件会规范孤立记录（生成 128 位哈希名）并按内容哈希自动接管。
- 后台定时领养：每 10 分钟扫描最新孤立历史与笔记，按“长度 + 快速哈希 + 全文一致”自动绑定，并将已处理的孤立历史归档到 `/_ORPHAN/_ADOPTED`。
- 交互体验提升：状态栏显示“已记录次数”，按钮悬浮动画；设置项支持 `button` / `link` 控制风格。

使用方法（场景示例）：
- 在 Obsidian 中编辑 `A.md` 产生历史后，使用资源管理器把它改名为 `B.md`。
- 回到 Obsidian 打开 `B.md`：如接管成功，状态栏显示 `X edits`；如写入失败会提示并保留孤立历史在 `/_ORPHAN`。
- 需要手动处理时，执行命令：
  - `Clean orphan edit histories`：归档无对应笔记的历史到 `/_ORPHAN`。
  - `Adopt orphan history for active file`：为当前笔记领养匹配的孤立历史（同名或内容一致）。

设置项（常用）：
- `Minimum seconds between edits`：两次编辑最小间隔秒数。
- `Max history file size`：历史压缩包体积上限（KB），`0` 表示不限制。
- `Language`：中文 / English / Français。
- `Control style`：`button` 或 `link`。

常见问题（FAQ）：
- 打开历史面板提示“暂无历史”：刚写入的 `.ceh` 可能尚未索引到 Vault，插件会以适配器读取；稍后再试即可。
- 旧版残留的 `file-open` 回调错误：完全退出并重启 Obsidian 可清除。
- 外部工具导致换行不同：插件已统一移除 BOM 并将行尾归一为 `LF`，避免匹配失败。

安装说明：
- 在社区插件中启用 `Centralized Edit History`。
- 历史文件扩展名为 `.ceh`，集中目录为 `/.obsidian/centralized-edit-history`。

——

English:
- This is a local fork of `Edit History` to avoid marketplace updates overwriting local settings, and to centralize all history files `.ceh` under `/.obsidian/centralized-edit-history`.
- UI language is selectable: Chinese / English / French (in Settings).
- Default language: Chinese.

Key changes:
- Plugin `id`: `centralized-edit-history`; name: `Centralized Edit History`; version: `1.0.0-local`.
- `data.json` sets `editHistoryRootFolder` to `/.obsidian/centralized-edit-history`; history file extension is `.ceh`.
- Old `.edtz` files were migrated and renamed to `.ceh` in the new folder.

Enhancements & fixes:
- Hover effect & link style: setting `controlStyle` supports `button` / `link`; `mod-cta` buttons have lightweight hover animations.
- Diff navigation fix: removed duplicate click handlers and syntax error; unified `diffInfo.textContent`.
- Compatibility fixes: replaced unsupported `trigger(...)` with native `dispatchEvent("change")` and `click()`; replaced `.toggle()` with `style.display`.
- Rename/move retention: on Obsidian rename/move, history files follow automatically; for non-`TFile` histories, adapter-level copy to the new path.
- New commands:
  - `Clean orphan edit histories`: move non-matching `.ceh` files to `/_ORPHAN`.
  - `Adopt orphan history for active file`: match by basename and adopt the most recent orphan for the active note.
- Background auto-adopt: every 10 minutes, scan latest 100 orphan histories and latest 100 notes; compare latest raw content (length + quick hash + full text) and attach on exact match; archive original to `/_ORPHAN/_ADOPTED`.
- Adopt on open: when opening a note without history, immediately clean and normalize orphans (store by 128-bit hash of latest raw to `/_ORPHAN/<hash>.ceh`), then hash current note and auto-adopt matching history; keep latest 100 orphans and archive older ones to `/_ORPHAN/_ARCHIVE`.

Usage & Notes:
- Enable `Centralized Edit History` in community plugins list.
- If you need further migration or cleanup, let me know.

——

Français :
- Il s’agit d’un fork local de `Edit History` pour éviter que les mises à jour du marketplace n’écrasent la configuration locale, et pour centraliser tous les fichiers d’historique `.ceh` dans `/.obsidian/centralized-edit-history`.
- Langue de l’interface sélectionnable : Chinois / Anglais / Français (dans Paramètres).
- Langue par défaut : Chinois.

Modifications clés :
- `id` du plugin : `centralized-edit-history` ; nom : `Centralized Edit History` ; version : `1.0.0-local`.
- `editHistoryRootFolder` est défini à `/.obsidian/centralized-edit-history` dans `data.json` ; l’extension d’historique est `.ceh`.
- Les anciens fichiers `.edtz` ont été migrés et renommés en `.ceh` dans le nouveau dossier.

Améliorations & correctifs :
- Effet de survol et style de lien : `controlStyle` supporte `button` / `link` ; animations de survol légères sur les boutons `mod-cta`.
- Navigation des diffs corrigée : gestionnaires dupliqués supprimés et erreur de syntaxe corrigée ; `diffInfo.textContent` unifié.
- Correctifs de compatibilité : `trigger(...)` remplacé par `dispatchEvent("change")` et `click()` natifs ; `.toggle()` remplacé par `style.display`.
- Rétention lors des renommages/déplacements : dans Obsidian, les historiques suivent automatiquement ; pour les historiques non `TFile`, copie via l’adaptateur vers le nouveau chemin.
- Nouvelles commandes :
  - `Clean orphan edit histories` : déplace les `.ceh` sans note correspondante vers `/_ORPHAN`.
  - `Adopt orphan history for active file` : associe par le nom de base et adopte l’orphan le plus récent pour la note active.
- Adoption automatique en arrière-plan : toutes les 10 minutes, analyse les 100 historiques orphelins les plus récents et les 100 notes les plus récentes ; compare le dernier contenu brut (longueur + hachage rapide + texte complet) et attache en cas d’égalité ; archive l’original vers `/_ORPHAN/_ADOPTED`.
- Adoption à l’ouverture : à l’ouverture d’une note sans historique, nettoyage et normalisation immédiats des orphelins (stockage par hachage 128 bits du dernier contenu brut dans `/_ORPHAN/<hash>.ceh`), puis hachage de la note courante et adoption automatique si correspondance ; seuls les 100 orphelins les plus récents sont conservés, les plus anciens archivés dans `/_ORPHAN/_ARCHIVE`.

Utilisation & Remarques :
- Activer `Centralized Edit History` dans la liste des plugins communautaires.
- En cas de besoin de migration supplémentaire ou de nettoyage, dites-le moi.