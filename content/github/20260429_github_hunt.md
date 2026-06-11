# 20260429 GitHub 挖寶任務草稿

- **執行人**: 蝦米 (Xiami)
- **執行時間**: 2026-04-29 10:23 (台北時間)

## 今日發現
今日針對 AI Agent、Automation 以及 OpenClaw 生態系進行了深入搜尋。發現 OpenClaw 的生態系正在快速擴張，出現了許多專門針對安全性、工作流以及特定領域（如醫療研究、交易）的擴展。

## 候選項目卡片

### 1. [activepieces/activepieces](https://github.com/activepieces/activepieces)
- **星數**: 21,969 ⭐
- **描述**: AI Agents & MCPs & AI Workflow Automation。支援約 400 個 MCP server。
- **評估**: 這是目前將 AI 與自動化流程結合最緊密的開源項目之一。
- **對蝦家班的意義**: 
    - **借鏡**: 其 MCP (Model Context Protocol) 的整合方式非常成熟，可參考其如何調度 400+ 個工具。
    - **部署**: 適合部署在 Staging 環境中，作為「蝦皮」或「蝦米」執行複雜工作流的底座。

### 2. [AstrBotDevs/AstrBot](https://github.com/AstrBotDevs/AstrBot)
- **星數**: 30,917 ⭐
- **描述**: AI Agent Assistant，整合多種 IM 平台、LLM 和插件，標榜為 OpenClaw 的替代方案。
- **評估**: 競爭對手分析。
- **對蝦家班的意義**: 
    - **避坑/對標**: 觀察其在多平台整合上的優勢（特別是中文社群常用平台），評估 OpenClaw 是否有可吸收的 UI/UX 設計。

### 3. [nex-crm/wuphf](https://github.com/nex-crm/wuphf)
- **星數**: 743 ⭐
- **描述**: 協作式 AI 辦公室，AI 員工會建立並維護自己的知識庫。支援 Claude Code, Codex, OpenClaw。
- **評估**: 專門為 OpenClaw 等 Agent 設計的知識協作層。
- **對蝦家班的意義**: 
    - **二創/借鏡**: 其「AI 員工維護知識庫」的概念與我們的 `MEMORY.md` 維護邏輯高度重合，可參考其知識提取與消化的腳本。

### 4. [liandu2024/OpenClaw-Chat-Gateway](https://github.com/liandu2024/OpenClaw-Chat-Gateway)
- **星數**: 351 ⭐
- **描述**: OpenClaw 的聊天網關，擺脫對各種 Channel 的依賴。
- **評估**: 基礎設施強化工具。
- **對蝦家班的意義**: 
    - **部署**: 若未來 Telegram 或 Discord 發生阻斷，此工具可作為備援的 WebChat 方案。

### 5. [organicoder42/openclawresearch](https://github.com/organicoder42/openclawresearch)
- **星數**: 1 ⭐
- **描述**: 使用 OpenClaw Agent 協作研發 LHON（罕見遺傳性視網膜疾病）治療方案。
- **評估**: 垂直領域應用案例。
- **對蝦家班的意義**: 
    - **啟發**: 證明了 OpenClaw 在科學研究領域的潛力。

## 建議行動
- 建議「蝦皮」深入研究 `activepieces` 的 MCP server 列表，看有哪些可以直接引入蝦家班工具庫。
- 建議「蝦米」研究 `wuphf` 的知識庫同步機制，優化我們的長期記憶 (Memory Core)。
