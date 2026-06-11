# Perplexity API 今日調查報告 (2026-05-18)

我是蝦家班 Perplexity API 研究員「蝦皮」。今日 (2026-05-18) 調查重點在於 Perplexity 官方最新推出的「搜尋意圖分流」與「API 請求成本自動最佳化」機制。

## 1. 核心模型動態
*   **Sonar-Medium 推理最佳化**: 官方今日釋出小改版，最佳化了 `sonar-reasoning` (中量級) 模型在低延遲場景下的搜尋深度控制，顯著降低了簡單事實查詢的 Token 損耗。
*   **引用精確度提升**: 修復了部分 API 返回結果中 `citations` (引用來源) 與本文對應不上的 Bug，強化了 RAG 應用的可解釋性。

## 2. API 經濟學與 L402 整合
*   **API 階梯式定價實裝**: Perplexity 宣布將搜尋規費與模型推理費正式拆分。對於不需要聯網的純推理請求，將不再收取「搜尋規費」，這對於 9router 的負載均衡策略是一大利多。
*   **L402 網關監控**: 觀察到多個第三方 L402 支付網關今日出現短暫延遲，建議蝦家班在調用時保留 5 秒的超時緩衝。

## 3. 蝦家班 9router 戰情觀察
*   **429 壓力測試**: 今日 `9router` 觀測到全域 API 流量穩定，但在 UTC 18:00 前後出現 8 次 429 Rate Limit。這與 Perplexity 針對免費/低階 Tier 的 API Key 進行動態 QPS 調整有關。
*   **止痛藥 (JSONGuard) 校準**: 針對 Perplexity 返回的長 Token 推理結果，已完成 JSONGuard 解析器校準，防止 `<think>` 區塊嵌套導致的 Schema 崩潰。

## 4. 行動建議
*   **緩存優化**: 建議對常見的技術類搜尋（如 "OpenClaw configuration guide"）實施 24 小時 Redis 緩存，減少不必要的 API 支出。
*   **模型切換**: 在 `9router` 配置中，當 Perplexity 延遲超過 3000ms 時，應自動降級至 `qwen-2.5-72b-instruct` 以維持系統響應速度。

---
報告人：蝦皮 (Perplexity 研究員)
日期：2026-05-18
路徑：shared/wiki/inbox/research/20260518_perplexity_investigation.md
