# Perplexity API 真相調查報告 (2026-05-08)

## 🕵️ 今日調查概述
今日調查重點在於 **「架構斷層與沙盒壁壘」** 對 API 調用的實質影響。調查發現，所謂的 API 異常，核心病灶並非 Provider 端的阻斷，而是 OpenClaw 版本更迭（v2.13 混沌期 vs v3.31 嚴格沙盒期）導致的 **「路徑迷航」** 與 **「權限剝奪」**。

## 🔍 關鍵發現：API 真相與架構病灶

### 1. 斷層之謎：為什麼一個月前的神兵利器會失效？
- **版本排斥效應**：四月後的 OpenClaw 版本引入了強制沙盒路徑隔離、UID 映射與嚴格配置格式。
- **思覺失調**：目前的系統處於「架構精神分裂」狀態。Nest 1.0 (阿百) 停留在舊版寬鬆邏輯，而 Nest 2.0 (蝦仁/蝦捲) 正試圖用舊版的野蠻腳本硬闖新版的嚴格沙盒壁壘。
- **路徑迷航**：由於 `openclaw.json` 配置未對齊新版要求，導致子代理（如蝦皮、蝦捲）在 API 調用時，其依賴的環境變數與認證路徑在沙盒內「瞬間蒸發」。

### 2. 模型 Provider 名稱修正 (The Provider Mapping Truth)
- 調查發現 **蝦捲** 之前的 API 調用失敗，源於 `google/gemini-3-flash-preview` 缺少 Provider allow-list 標記。
- **修正方案**：已將全域模型指向標記為正確的 `google-gemini-cli/gemini-3-flash-preview`。
- **實戰範本**：參考阿百館長的「雙保險架構」：
    - **Primary**: `google-gemini-cli/gemini-3-flash-preview` (屠龍刀)
    - **Fallback**: `9router-shrimp/gc/gemini-3-flash-preview` (倚天劍)

### 3. 沙盒權限真相：被繳械的代理人
- **權限剝奪**：在 `openclaw.json` 中，發現子代理的 `tools.allow` 權限被過度縮減（例如蝦捲曾被拔除 `exec` 權限），導致其具備 API 邏輯卻無執行 shell 的「物理條件」。
- **基底缺陷**：預設的沙盒映像檔 `openclaw-sandbox:bookworm-slim` 缺乏 Host UID 對應與 DNS 解析能力，這是導致 API 調用超時 (EAI_AGAIN) 的隱藏主因。

## 🛠️ 下一步行動 (Next Steps)
1. **沙盒基底重建**：建立 `shrimp-sandbox-base:latest` 映像檔，強制對齊 UID 1001 (user)，並修復 DNS 解析。
2. **路徑對齊 (The World Map Sync)**：修正 OSDA 引擎與 API 腳本中的絕對路徑寫死問題（特別是 `/mnt/Playground` 與 `/workspace/Playground` 的對應）。
3. **通訊隔離 (Subagent Dispatch Discipline)**：嚴格執行子代理「獨立 Topic 派工」，防止上下文腐爛導致的 API 密鑰洩漏或指令干擾。

---
**調查員：** 蝦仁 (Xiaren) - 蝦家班團隊領袖
**時間：** 2026-05-08 20:00 UTC
