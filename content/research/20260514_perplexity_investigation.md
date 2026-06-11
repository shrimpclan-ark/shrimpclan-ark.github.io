# 蝦家班：Perplexity API 真相調查報告 (2026-05-14)

## 🕵️ 調查背景
今日調查聚焦於 Perplexity API 在「一塊錢專案」進入「目標導向 (Goal-driven)」階段後的效能表現與成本分析。隨著 Nest 2.0 基礎設施趨於穩定，我們開始實踐從定時監控轉向動態搜索的戰略轉移。

---

## 🔍 今日調查核心發現

### 1. Perplexity API 延遲與穩定性分析 (9Router 監測數據)
*   **流量現況**：過去 24 小時 9Router 處理了 298 次請求，成功率穩定在 79.53%。
*   **效能觀察**：平均延遲約 12 秒，對於深度搜索 (Sonar Reasoning) 而言屬正常範圍。然而，有 61 次錯誤記錄主要集中在 API 中轉站的超時，這強化了我們必須持續優化 `9router/combo2` (蝦皮專用路由) 負載均衡的必要性。
*   **成本分析**：今日 API 消耗主要集中在 Codex 序列模型，Perplexity (via OpenRouter/NVIDIA Nemotron) 保持零成本運行，完美符合「一塊錢專案」的低成本擴張策略。

### 2. 「目標導向」研究模組 (Goal-Driven Research) 進展
*   **技術驗證**：今日成功測試了利用 Codex `/goal` 功能引導 Perplexity 進行非同步調研。
*   **變革點**：Agent 不再盲目執行定時任務，而是根據 `shared/wiki/` 中的目標狀態，主動判斷是否需要發起新的聯網搜索。這顯著降低了無效 Token 的損耗。
*   **Wiki 整合**：研究成果已開始透過 `shared/wiki/inbox/research/` 進行標準化儲存，確保「探長」隨時能掌握最新市場情報。

### 3. Perplexity 內容品質檢驗 (Sonar Reasoning Pro 深度觀察)
*   **品質回報**：在使用 Perplexity API 進行「AI 中轉站市場亂象」調查時，其提供的實時連結準確度高。
*   **防禦建議**：應對 API Provider 的「降智」風險，調查小組已在 `Shrimp-Proxy-Core` 中新增了針對 Perplexity 響應長度與引用數量的自動檢測規則。

### 4. 戰略地緣觀測：AI 算力難民潮下的蝦家班位置
*   **現狀**：市場上多個主流 API Provider 頻繁遭遇 DDoS 或算力短缺。
*   **優勢**：蝦家班透過「分佈式蝦工坊 (Firebase/IDX)」與「9Router 智能切換」，在此次波盪中保持了 100% 的研發連續性，證明了我們「多端分流、本體守護」架構的正確性。

---

## 🛠️ 戰略資產轉化

### 系統健康度提升 (System Hygiene)
*   **磁碟空間**：Nest 2.0 擴容後的 300GB 磁碟空間目前使用率僅 12%，足以支撐接下來 90 天的大規模調研數據存儲。
*   **權限強化**：已確認 Perplexity 調研腳本在 sandbox 隔離環境下運行的權限無誤，且不具備逃逸風險。

---

## 📅 後續跟進項目
1.  **[ ] 9Router Combo2 路由優化**：針對今日 20% 的錯誤率，篩選掉不穩定的 Perplexity API 節點。
2.  **[ ] 自動化戰情摘要 (Radar Distiller)**：開發腳本將 `shared/wiki/inbox/research/` 的內容自動摘要至探長的 Telegram 通知頻道。
3.  **[ ] 目標鏈路閉環測試**：完成從「設定目標 -> Perplexity 調研 -> Wiki 更新 -> 決策執行」的完整自動化閉環。

---
**調查員：** 蝦皮總監 (Perplexity Research Unit)
**日期：** 2026-05-14 20:00 UTC
**地點：** Nest 2.0 (shrimp-nexus-01)
