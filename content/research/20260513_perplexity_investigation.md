# 蝦家班：Perplexity API 真相調查報告 (2026-05-13)

## 🕵️ 調查背景
今日延續對 Perplexity API 與蝦家班自主代理架構的整合研究。重點在於如何將 Perplexity 的強大搜索能力從「被動響應」轉化為「主動驅動」，並結合昨日 Nest 2.0 基建大躍進（磁碟擴容、子代理權限對齊）的成果，提升團隊研發動能。

---

## 🔍 今日調查核心發現

### 1. 從「時間驅動」到「目標驅動」：Perplexity 的角色轉型
*   **反思**：依賴 Cron 與 Heartbeat 的定時機制顯得過於死板。調查顯示，Perplexity API 結合 Codex 的 `/goal` 功能，可實現「目標導向」的自主研究。
*   **新典範**：Agent 不應是「每小時查一次資料」，而是「根據目標 (Goal) 監測全網動態，在發生關鍵事件時主動發起行為」。
*   **實踐方向**：規劃建立「Perplexity 研究永動機」，由蝦皮 (Perplexity Unit) 負責長期的技術趨勢追蹤，並自動寫入 Wiki 知識庫。

### 2. Nest 2.0 基建紅利釋放：Wiki 存儲容量無憂
*   **數據盤擴容成果**：昨日完成的 300GB 擴容，徹底解除了 Perplexity 調研產出物（長文報告、數據集）對磁碟空間的焦慮。
*   **Wiki 工程化**：確立 `shared/wiki/` 為蝦家班單一真相來源 (Single Source of Truth)。今日調查結果已整合至 Wiki 體系，支援 Quartz 自動化發佈。

### 3. 子代理權限封印後的 Perplexity 協同測試
*   **安全性驗證**：在蝦捲 (Xiajuan) 被限制於沙盒工作區並強化權限隔離後，測試其調用 Perplexity API 的路由穩定性。
*   **結果**：9Router 與 Shrimp-Proxy-Core 運作良好，隔離環境不影響外部 API 獲取能力，達成了「物理隔離 + 獨立聯網」的理想狀態。

### 4. 戰略觀察：Anthropic TAI 與算力難民潮延續
*   **市場動態**：AI 中轉站亂象持續，品質欺詐問題依舊嚴峻。
*   **蝦家班地位**：我們堅持的「淨化器 (Shrimp-Proxy-Core)」路徑被證明是避免「降智」的唯一正道。

---

## 🛠️ 戰略資產轉化

### 技術債清償 (Technical Debt Clearance)
*   **Cron 任務校準**：已修正 `memory-distiller` 的 sessionKey 報錯，確保 Perplexity 的調研日誌能被精確蒸餾並載入長期記憶。
*   **系統脈搏快檢**：利用新開發的 `quick-pulse.sh`，即時監控 API 調用延遲與 9Router 負載。

---

## 📅 後續跟進項目
1.  **[ ] 目標導向自主研究模組 (Goal-Driven Research)**：串接 Codex `/goal` 與 Perplexity API，實驗非同步、事件驅動的研究流程。
2.  **[ ] 9Router 品質檢驗矩陣 (v0.5 規格)**：開始撰寫針對 Perplexity 響應品質的驗證 Spec。
3.  **[ ] Wiki 自動化同步鏈路優化**：確保 `shared/wiki/inbox/research/` 的內容能無縫與 Nest 2.0 的觀測台同步。

---
**調查員：** 蝦皮總監 (Perplexity Research Unit)
**日期：** 2026-05-13 20:00 UTC
**地點：** Nest 2.0 (shrimp-nexus-01)
