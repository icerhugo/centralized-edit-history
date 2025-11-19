# Centralized Edit History (local fork)

中文 | English | Français

——

中文：
- 本插件是对原 `Edit History` 的本地重命名与封装，目的：避免后续市场更新覆盖本地配置，并将所有 `.ceh` 历史文件集中存储到 `/.obsidian/centralized-edit-history`，减少目录杂乱。
- 支持界面语言选择：中文 / 英语 / 法语（设置页可切换）。
- 默认语言：中文。

关键变更：
- 插件 `id`：`centralized-edit-history`；名称：`Centralized Edit History`；版本：`1.0.0-local`。
- `data.json` 中 `editHistoryRootFolder` 设为 `/.obsidian/centralized-edit-history`；历史扩展名改为 `.ceh`。
- 已批量迁移旧 `.edtz` 文件到新目录并改名为 `.ceh`。

使用与注意：
- 需启用社区插件列表中的 `Centralized Edit History`。
- 如需二次迁移或清理旧目录，请告知以便处理。

——

English:
- This is a local fork of `Edit History` to avoid marketplace updates overwriting local settings, and to centralize all history files `.ceh` under `/.obsidian/centralized-edit-history`.
- UI language is selectable: Chinese / English / French (in Settings).
- Default language: Chinese.

Key changes:
- Plugin `id`: `centralized-edit-history`; name: `Centralized Edit History`; version: `1.0.0-local`.
- `data.json` sets `editHistoryRootFolder` to `/.obsidian/centralized-edit-history`; history file extension is `.ceh`.
- Old `.edtz` files were migrated and renamed to `.ceh` in the new folder.

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

Utilisation & Remarques :
- Activer `Centralized Edit History` dans la liste des plugins communautaires.
- En cas de besoin de migration supplémentaire ou de nettoyage, dites-le moi.