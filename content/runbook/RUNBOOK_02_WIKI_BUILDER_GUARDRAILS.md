# RUNBOOK_02_WIKI_BUILDER_GUARDRAILS.md

> Nest 2.0 / P3.8
> Wiki Builder 護欄規範

## 0. 核心職責
- 掃描 `shared/wiki/inbox/` 內草稿
- 驗證 metadata、去重、摘要整編
- 依 `merge_hint` 合併至正式 `wiki/`
- 失敗時保留草稿、不覆寫主檔

## 1. 處理流程
1. **驗證**：metadata 齊全？
2. **去重**：同日同 topic 是否已有重複？
3. **整編**：依 `merge_hint` (direct/summarize/split/hold/archive) 執行。
4. **後置**：成功併入後，將草稿移至 `shared/wiki/processed/`。

## 2. 失敗處理
- 無 metadata 或格式錯誤：跳過 + 記錄。
- 主 Wiki 寫入失敗：回滾 + 保留原草稿 + Telegram 告警。
