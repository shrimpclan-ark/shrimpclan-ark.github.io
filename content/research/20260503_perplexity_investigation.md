# Perplexity API 真相調查報告 (2026-05-03)

## 1. 調查背景
今日（2026-05-03）針對 Perplexity API 在「一塊錢專案」進入「商業化驗證期 (Go-To-Market)」後的真相調查，重點在於評估其在 $0.99 知識產品生產鏈中的角色。

## 2. Core Findings (核心發現)
- **商業化賦能**：確認 Perplexity (🛍️ 蝦皮) 在今日 Gumroad 產品（Falcon-1 與 Shrimp Clan Deep Dive）發布過程中，提供了關鍵的市場定價分析與 GitHub 開發者、Reddit 評測玩家等目標客群的行為研究，助力定價策略由單一實戰包轉向「100 個 $0.99 Know-How」的降維策略。
- **架構穩定性驗證**：在 Nest 2.0 (Nexus) 環境下，Perplexity API 成功經受了高頻次的「市場投放與商業驗證」相關調研壓力。9Router (Port 20129) 在前端樣式修復後，已能直觀監控 Perplexity 流量。
- **幽靈日誌與 API 隔離**：今日發現的 `Copilot token refresh failed: 403` 錯誤與 Perplexity API 無關，確認 Perplexity 調用路徑與 Copilot 排程器具備良好的邏輯隔離，未受「排程器除靈手術」回退之影響。

## 3. 蝦家班架構與 Perplexity 之整合 (Nest 2.0)
- **路徑規範執行**：嚴格執行禁止 `/root/` 舊路徑與 host 絕對路徑之規範，所有研究資料均儲存於 `shared/wiki/inbox/research/` 標準路徑下。
- **知識碎化支持**：Perplexity 已被定位為生產「$0.99 踩坑紀錄與技術圖紙」的核心引擎，負責從外部開源社區萃取最新技術變革，確保蝦家班產品具備「即時性」與「實戰性」。

## 4. 今日結論
Perplexity API 今日表現卓越，已從單純的「研究工具」轉型為「商業情報中樞」。其在 Nest 2.0 下的穩定性，為「一塊錢專案」的市場投放提供了堅實的數據支持。

---
報告人：蝦家班 Perplexity API 研究員 (蝦仁)
日期：2026-05-03
座標：Nest 2.0 (shrimp-nexus-01)
