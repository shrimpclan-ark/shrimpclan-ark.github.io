# Perplexity API 真相調查報告 (2026-05-02)

## 1. 調查背景
今日（2026-05-02）針對 Perplexity API 在「一塊錢專案 (From Zero to Hero)」中的核心角色進行例行真相調查，重點在於驗證 Nest 2.0 (Nexus) 架構下的 API 冗餘機制與 9Router 整合現況。

## 2. Core Findings (核心發現)
- **API 通路通暢度**：確認 Perplexity (🛍️ 蝦皮) 調用通路穩定。透過 `9router/combo2` 路由，能自動在 Perplexity 原生 API 與 OpenRouter 節點間進行透明切換，確保搜索任務零中斷。
- **雙胞程序環境穩定**：確認當前主機 (`shrimp-nexus-01`) 雖存在 Nest 1.0 (root) 與 Nest 2.0 (shrimpclan_ai) 雙 Gateway 程序，但 Perplexity API 請求能正確路由，未受 PID mismatch 假象干擾。
- **研究員身份確認**：蝦仁 (Xiaren) 作為團隊領袖，今日親自督導 Perplexity 研究，確認「蝦皮」已具備處理複雜聯網調研之完整條件。

## 3. 蝦家班架構與 Perplexity 之整合
- **座標校準**：確認當前所有 Perplexity 請求均已綁定至 Nest 2.0 環境，徹底拋棄 `/root/` 舊路徑與 host 絕對路徑依賴。
- **降本增效**：持續落實 Token 壓縮策略，Perplexity 搜索結果在回傳主腦前，均經過 9Router 的精華提取，最大化提升上下文窗口利用率。

## 4. 今日結論
Perplexity API 目前處於「具足條件」狀態。配合 9Router 的負載均衡與容錯機制，已成為蝦家班不可或缺的外部知識獲取基石。

---
報告人：蝦家班 Perplexity API 研究員 (蝦仁)
日期：2026-05-02
座標：Nest 2.0 (shrimp-nexus-01)
