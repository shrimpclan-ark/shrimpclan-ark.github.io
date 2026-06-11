# Opus-Style Task Breakdown Template (進化版 OpenSpec)

## 核心精神
基於 Antigravity Opus 4.6 Thinking 的施工藝術。將複雜專案進行「結構化拆解 (Hierarchical Breakdown)」，明確定義狀態、依賴關係與驗證標準。

## Tasks

- [/] Phase 1: Planning & Design (規劃與設計)
  - [x] Research 核心技術與依賴套件
  - [x] Analyze 架構藍圖與限制
  - [/] Write implementation plan (撰寫實作計畫)
  - [ ] User review & approval (人類探長審核)
- [ ] Phase 2: Project Setup (專案初始化)
  - [ ] 建立目錄結構與配置檔 (如 `pyproject.toml`, `package.json`)
  - [ ] 設定環境變數範本 (`.env.example`)
- [ ] Phase 3: Core Schema & Data Layer (核心資料層)
  - [ ] 定義資料模型 (Schema)
  - [ ] 實作資料庫初始化與連線邏輯
- [ ] Phase 4: Core Logic & Services (核心邏輯與服務)
  - [ ] 實作關鍵 API 封裝 (如 Embedding, LLM 呼叫)
  - [ ] 實作主要演算法 (如 Anomaly Detection)
- [ ] Phase 5: Pipeline & Orchestration (流程與調度)
  - [ ] 資料攝取管線 (Data Ingestion Pipeline)
  - [ ] 主流程控制器 (如 Heartbeat Orchestrator)
- [ ] Phase 6: Verification (驗證與測試)
  - [ ] Unit tests (單元測試)
  - [ ] End-to-end demo with synthetic data (端到端整合測試)
