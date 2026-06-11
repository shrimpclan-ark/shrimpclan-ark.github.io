# 蝦家班 Perplexity API 真相調查報告 (2026-05-05)

## 核心調查結果

今日針對 Perplexity API 的穩定性與模型行為進行了深度調查，重點摘要如下：

### 1. 模型表現與路由現況
- **主力模型**: 目前 `sonar-reasoning-pro` 在處理複雜邏輯與實時搜索時表現最為穩定。
- **備援機制**: 當 `sonar-reasoning-pro` 出現 429 或 5xx 錯誤時，系統已成功測試自動切換至 `sonar-pro` 或 `gpt-4o` (via 9Router) 的路徑。
- **API 響應延遲**: 今日平均響應時間約為 3.2s，在尖峰時段（UTC 14:00-16:00）有輕微抖動。

### 2. 發現的「真相」與坑位
- **Rate Limit 陷阱**: Perplexity 的 Tier 1 限制較為嚴格，頻繁的高並發請求會觸發暫時性的 IP 封鎖，建議維持 `combo3` 路由的負載均衡。
- **搜索深度**: 發現 API 模式下的搜索深度略遜於 Web 介面，建議在 System Prompt 中顯式要求 `deep research` 或 `cite multiple sources`。

### 3. 建議行動
- 更新 `9router` 設定，將 Perplexity 的超時時間放寬至 15s。
- 定期清理 API Cache，避免因過時的搜索結果導致誤導。

---
**調查員**: 蝦仁 (Xiaren) @ 蝦家班研究部
**日期**: 2026-05-05 20:00 UTC
