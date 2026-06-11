# SDD-HARNESS-004: shrimp-active-steering (Active Traffic Governance)

## 1. 待解決問題 (Problem Statement)
9router 的傳統 Fallback 是「被動式」的：必須等待 429 (Too Many Requests) 或 500 (Internal Server Error) 報錯後才切換帳號。這會導致：
*   Agent 思考鏈條因 Retry 而卡頓（「不絲滑」感）。
*   無效重試浪費了寶貴的「信用分」與回應時間，增加被上游 API 封鎖的風險。

## 2. 提案構想 (Proposed Idea): 預判型切換 (Proactive Pivot)
*   **監聽層 (LatencyMonitor):** 偵測 ANOMALY（例如：Time-To-First-Token 延遲飆升 2 倍且樣本數足夠，或接收到即將耗盡配額的 Headers）。
*   **指令層 (Hook Injection):** 插件在 `onRouteDecision` 鉤子中向 `RequestContext` 注入 `preferred_action: "SOFT_SKIP"`。
*   **執行層 (accountFallback.js):** 9router 接收此信號，在硬報錯 (Hard Fail) 發生前，直接讓目前 Provider 進入「冷卻觀察期」，並平滑跳轉至下一順位 Provider。

## 3. 核心價值 (Value Proposition)
*   **極致絲滑:** 使用者/Agent 感覺不到任何重試，對話像水流一樣持續。
*   **流量洗白:** 避開 429 高風險時段，保護高價值的 Primary API (如 Vertex AI) 基金。
*   **戰力加乘:** 結合 `gemini-3.1-flash-lite-preview` 的低成本優勢，實現「又快又便宜又穩」。

## 4. 實戰驗證計畫 (The "Golden Sample" Strategy)
*   **Phase 1:** 規格確立 (This document).
*   **Phase 2:** 代碼轉錄 (Opus/Sonnet implementation of hooks in `shrimp-9router-core`).
*   **Phase 3:** 震撼教育 (Stress test against unreliable free APIs using `qa-testing` skill to intentionally trigger 429s).
*   **Phase 4:** 引擎微調 (Collect "Golden Samples" of real 429 characteristics to tune the `SOFT_SKIP` threshold).
