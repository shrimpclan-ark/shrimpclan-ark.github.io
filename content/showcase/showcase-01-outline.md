---
title: "Showcase #1: Context Diet - 完整內容大綱"
description: "AI Agent Context 膨脹問題深度解析與解決方案完整大綱"
date: 2026-03-17
author: 蝦家班產品團隊
version: 1.0
toc: true
---

# Showcase #1: Context Diet 完整內容大綱

> **核心理念**: Input Token 效率 = Agent 運營成本控制的關鍵

---

## Chapter 1: Context 膨脹問題診斷

### 1.1 什麼是 Context 膨脹 (Context Bloat)
- **定義**: AI Agent 對話歷史累積導致的輸入 token 過載現象
- **根本原因**: LLM 無狀態設計 vs 開發者對「連續性」的需求矛盾
- **臨界點指標**: 當 context 超過模型最大容量的 80%

### 1.2 Context 膨脹的五個徵兆
1. **回應延遲倍增** - 從 3s 延伸至 30s+
2. **成本曲線陡升** - Input token 佔比從 30% 飆升至 90%
3. **注意力稀釋** - 模型開始「忘記」早期指令
4. **API 失敗率上升** - 429/timeout 錯誤頻繁
5. **記憶體溢出** - 容器 OOM kills 增加

### 1.3 真實案例診斷
```
案例: Nest1 時期的 Agent 會話
- 初始: ~2K tokens/request
- 1小時後: ~15K tokens/request
- 3小時後: ~97K tokens/request ⚠️
- 結果: API 逾時、成本失控、被迫重啟 session
```

### 1.4 為什麼開發者容易忽視這個問題
- 短期測試無法顯現累積效應
- 免費 tier 隱藏了真實成本
- 「更多 context = 更好理解」的迷思
- 缺乏可視化監控工具

---

## Chapter 2: Input Token 效率分析

### 2.1 Token 經濟學基礎
- **Input vs Output Token 成本比**: 通常 1:3 至 1:10
- **長尾效應**: 前 20% 的 context 貢獻 80% 的資訊價值
- **沉默成本**: 無效 context 佔據寶貴的 attention window

### 2.2 九種常見的低效 Context Pattern

| Pattern | 描述 | 影響 | 偵測方法 |
|---------|------|------|----------|
| **重複指令** | 系統提示在每次請求重複 | +15-30% | 文字比對 |
| **過期工具結果** | 舊的 search/檔案內容殘留 | +10-25% | TTL 檢查 |
| **難以壓縮的錯誤** | 冗長的 stack trace | +5-20% | 正規表示式 |
| **思考鏈殘留** | CoT 輸出被保留下來 | +20-40% | 標記偵測 |
| **臨時變數** | 不再相關的中間值 | +5-15% | 參照計數 |
| **會話雜訊** | 禮貌性對話（「謝謝」、「請」）| +3-10% | 語意分析 |
| **格式膨脹** | Markdown/XML 標籤累積 | +10-20% | 結構分析 |
| **系統狀態快照** | 過期的環境變數/設定 | +5-15% | 版本比對 |
| **自我參照** | Agent 引用自己的舊回覆 | +10-30% | 遞迴偵測 |

### 2.3 Context 價值衰減模型
```
價值(t) = 初始價值 × e^(-λt) × 相關性係數

其中:
- λ (衰減常數): 任務相關 (coding: 0.3, chat: 0.1)
- 相關性係數: 與當前意圖的語意相似度
- 臨界值: 當 價值(t) < 0.1 時，可考慮移除
```

### 2.4 量化指標設計

#### 核心 KPI
- **Context Efficiency Ratio (CER)** = 有效資訊量 / 總 Token 數
- **Token 周轉率** = 輸入 token 數 / 輸出 token 數
- **每輪淨增量** = ΔInput Token / 對話輪數

#### 9Router 實測數據 (Nest2)
```yaml
模型比較 (平均 Input Token/Request):
  gemini-3.1-pro-preview: 8500
  claude-sonnet-4.5:      6200
  gemini-2.5-flash:       7800
  
最佳實務基準:
  無狀態模式: 1200-2500
  輕量 context: 3000-5000
  中型 context: 5000-10000
  重型 context: >10000 (需審查)
```

### 2.5 成本影響計算

**情境: 每日 1000 次 API 調用**

| Context 策略 | Avg Input Token | 日成本 (Gemini Pro) | 月成本 |
|--------------|-----------------|---------------------|--------|
| 無控制 | 25,000 | $18.75 | $562.50 |
| 基礎修剪 | 8,000 | $6.00 | $180.00 |
| 智能 Diet | 3,500 | $2.63 | $78.75 |
| **節省** | **86%** | **$16.12/day** | **$483.75/mo** |

---

## Chapter 3: Context Diet 解決方案

### 3.1 Context Diet 核心原則

#### The 80/20 Context Rule
> 「80% 的對話價值來自於 20% 的內容」

#### 分層管理策略
```
Layer 1: 永久層 (Permanent)
  - 系統提示詞 (System Prompt)
  - 核心身份設定
  - 不可動搖的安全規則

Layer 2: Session 層 (Session)
  - 當前任務上下文
  - 最近 3-5 輪有效對話
  - 主動式記憶 (Explicit Memory)

Layer 3: 暫存層 (Ephemeral)
  - 工具執行結果
  - 中間計算過程
  - 可丟棄的背景資訊
```

### 3.2 四種 Context Diet 技術

#### 技術 A: Header-Aware Chunking
```
原始: "幫我分析這個檔案"
Diet: "[檔案:/src/app.js, 大小:45KB] 幫我分析這個檔案"

節省: 避免重複傳輸完整檔案內容
原理: 資訊摘要 + 參照標記
```

#### 技術 B: Smart Summarization Gate
```python
def should_summarize(context, threshold=8000):
    if count_tokens(context) > threshold:
        # 保留 N 輪原始對話
        recent = keep_last_n(context, n=3)
        # 摘要更早的內容
        older = summarize(extract_older(context, n=3))
        return merge(recent, older)
    return context
```

#### 技術 C: Selective Amnesia (選擇性遺忘)
```yaml
遺忘規則引擎:
  - 類型: "工具輸出"
    生存期: "$TTL{result_ttl}"
    條件: "非錯誤結果"
  
  - 類型: "思考過程"
    生存期: "immediate"
    條件: "永遠"
  
  - 類型: "使用者確認"
    生存期: "session_end"
    條件: "若非關鍵決策"
```

#### 技術 D: Search-over-Context 協議
> 「以搜代傳」- 不傳遞 context，傳遞搜尋指令

```
傳統模式:
  Agent A → [傳遞 10KB context] → Agent B

Search-over-Context:
  Agent A → [傳遞 query + asset_id] → Agent B
  Agent B → [搜尋 Vector DB] → 取得片段
  
節省: ~90% token 傳輸
代價: +50-200ms 延遲
```

### 3.3 Context 壓縮算法實作

#### Level 1: 語法壓縮
- 移除多餘空白與換行
- 標準化引號與標點
- 統一縮排風格

#### Level 2: 語意壓縮
- 代名詞替換重複名詞
- 被動語態轉主動
- 列表簡化

#### Level 3: 結構壓縮
- JSON → YAML → 自定義標記
- 表格到 key-value 對
- CSV 格式用於資料序列

#### Level 4: 參照壓縮
- 外部化大型內容到 storage
- 用 hash/ID 取代完整內容
- Delta diff 取代全量更新

### 3.4 實作架構: Shrimp Context Manager

```
┌─────────────────────────────────────────────┐
│           Agent Request                      │
└─────────────────┬─────────────────────────────┘
                  ↓
┌─────────────────────────────────────────────┐
│     Context Diet Middleware                  │
│  ┌─────────────┐  ┌─────────────┐           │
│  │  Analyzer   │→ │  Classifier │           │
│  └─────────────┘  └─────────────┘           │
│         ↓                ↓                 │
│  ┌─────────────┐  ┌─────────────┐           │
│  │ Compressor│← │  Optimizer  │           │
│  └─────────────┘  └─────────────┘           │
└─────────────────┬─────────────────────────────┘
                  ↓
┌─────────────────────────────────────────────┐
│     Optimized Context → LLM API             │
└─────────────────────────────────────────────┘
```

### 3.5 配置參考 (YAML)

```yaml
context_diet:
  enabled: true
  version: "1.0.0"
  
  # 全局設定
  max_tokens: 8000
  preserve_ratio: 0.3  # 保留最近 30%
  
  # 壓縮策略
  compression:
    syntax: true       # Level 1
    semantic: true     # Level 2  
    structural: true   # Level 3
    reference: true    # Level 4
  
  # 遺忘規則
  amnesia_rules:
    tool_output:
      ttl: 300         # 5分鐘
      condition: "success"
    
    thought_process:
      ttl: 0           # 立即
      condition: "always"
    
    user_confirmation:
      ttl: -1          # Session 結束
      condition: "non_critical"
  
  # 摘要觸發
  summarization:
    trigger_threshold: 6000
    summary_model: "gemini-2.5-flash"
    preserve_turns: 3
```

---

## Chapter 4: 實戰案例與數據

### 4.1 案例 A: Nest2 多 Agent 協作系統

#### 背景
- 5 個 Agents 協作處理複雜任務
- 原始架構: 每輪傳遞完整 context
- 問題: 3 小時後單次請求達 97K tokens

#### 優化過程
| 階段 | 策略 | Avg Token | 改善 |
|------|------|-----------|------|
| 基準 | 無控制 | 97,000 | - |
| Step 1 | Header-Aware Chunking | 45,000 | 54% ↓ |
| Step 2 | Smart Summarization | 22,000 | 77% ↓ |
| Step 3 | Search-over-Context | 8,500 | 91% ↓ |
| Step 4 | 四層壓縮全啟用 | 3,200 | 97% ↓ |

#### 成果
- **成本節省**: 從 $36/day → $1.2/day
- **穩定性**: 0 timeout → 100% 成功率
- **響應速度**: 平均 8s → 2.5s

### 4.2 案例 B: 9Router 智能路由系統

#### 背景
- 管理 9+ 個 LLM 模型端點
- 需要保留歷史調用數據做決策
- 挑戰: 路由決策 context 不斷增長

#### 解決方案: 分層 Context + 資料分離
```
決策 Context (輕量):
  - 當前模型狀態快照
  - 最近 5 次調用結果
  - 即時錯誤計數

歷史數據 (外部化):
  - 完整調用日誌 → SQLite
  - 趨勢分析 → 預計算指標
  - 錯誤詳情 → 索引檔案
```

#### 成果
- 路由決策 context: 15KB → 800B
- 查詢歷史數據: On-demand 而非 inline
- 系統可擴展至 50+ 模型無壓力

### 4.3 案例 C: Vertex AI Search 整合

#### 背景
- RAG (Retrieval-Augmented Generation) 應用
- 傳統: 檢索結果全部塞入 context
- 問題: 大型文件導致 context 爆炸

#### 解決方案: 片段優先 + 相關性評分
```python
# 傳統做法 (低效)
context = retrieve_full_documents(query)
# → 可能 50K+ tokens

# Context Diet 做法
snippets = retrieve_relevant_snippets(
    query, 
    top_k=5,
    max_tokens_per_snippet=200
)
context = format_snippets(snippets)
# → 通常 <2K tokens
```

#### 數據對比
| 指標 | 傳統 RAG | Context Diet RAG | 改善 |
|------|----------|------------------|------|
| Avg Input Token | 35,000 | 4,500 | 87% ↓ |
| 回答相關性 | 72% | 89% | +17% |
| 成本/千次 | $26.25 | $3.38 | 87% ↓ |

### 4.4 效能基準測試

#### 測試環境
- 模型: gemini-3.1-pro-preview
- 任務: 程式碼審查 Agent
- 會話長度: 50 輪對話

#### 結果比較

| 策略 | 總 Token | 累積成本 | 最終輪延遲 | 任務完成度 |
|------|----------|----------|------------|------------|
| 無控制 | 2.3M | $17.25 | 45s | 85% |
| 基礎修剪 | 890K | $6.68 | 18s | 88% |
| Smart Diet | 320K | $2.40 | 6s | 92% |
| **全優化** | **145K** | **$1.09** | **3s** | **94%** |

### 4.5 錯誤與教訓

#### ❌ 過度修剪導致資訊遺失
- **問題**: 摘要過度激進，遺失關鍵細節
- **解決**: 關鍵字保護清單 + 用戶標記保留

#### ❌ TTL 設定過短
- **問題**: 工具結果太快過期，重複調用
- **解決**: 自適應 TTL 根據結果類型

#### ❌ 忽略多模態內容
- **問題**: 圖片 base64 編碼占用大量 token
- **解決**: 圖片摘要 + 參照連結

---

## Chapter 5: 結論與行動指南

### 5.1 核心發現

1. **Context 膨脹是真實且昂貴的問題**
   - 未控制的 Agent 可能產生 10-30x 不必要成本
   - 影響的不只是錢包，還有穩定性和使用者體驗

2. **預防勝於治療**
   - 從 Day 1 建立 context 管理機制
   - 比後期優化節省 80% 工程成本

3. **技術組合 > 單一銀彈**
   - Header-Aware + Summarization + Amnesia + Search
   - 協同效應才能達到 90%+ 節省

4. **監控是必須**
   - 無法測量就無法優化
   - CER (Context Efficiency Ratio) 應成為核心 KPI

### 5.2 快速啟動檢查清單

#### Phase 1: 診斷 (今天)
- [ ] 檢查當前平均 Input Token/request
- [ ] 識別 top 3 低效 context pattern
- [ ] 計算潛在節省金額 (每日/每月)

#### Phase 2: 快速勝利 (本週)
- [ ] 實作 Header-Aware Chunking
- [ ] 設定工具輸出 TTL
- [ ] 移除思考鏈殘留

#### Phase 3: 系統化 (本月)
- [ ] 部署 Smart Summarization
- [ ] 建立 Search-over-Context 協議
- [ ] 整合 Context Diet Middleware

#### Phase 4: 優化 (持續)
- [ ] A/B 測試不同策略組合
- [ ] 自動化監控與告警
- [ ] 建立團隊 best practice

### 5.3 工具與資源

#### 開源工具
- **Shrimp Context Manager** (蝦家班內部)
- **LangChain ContextualCompression**
- **LlamaIndex Node Postprocessors**

#### 監控方案
```python
# Token 使用追蹤裝飾器
@track_token_usage
async def agent_call(context, query):
    response = await llm.complete(context, query)
    return response

# 自動輸出 metrics 到 Prometheus/Grafana
```

#### 參考架構
- [附錄 A] 完整的 Context Diet Middleware 程式碼
- [附錄 B] 9Router 整合配置範例
- [附錄 C] Nest2 實戰配置模板

### 5.4 未來展望

#### 智能 Context 預測
- 基於任務類型預先優化
- ML 模型預測哪些 context 會被需要

#### 多模態 Diet
- 圖片/音訊的智慧摘要
- 自動格式轉換與壓縮

#### 跨 Agent 協議標準化
- 業界統一的 context 傳遞格式
- 自動相容不同 LLM provider

### 5.5 最後的話

> "Context Diet 不是限制，而是解放。
> 解放你的 Agent 從記憶的重擔中，
> 專注於真正重要的事：創造價值。"

**從今天開始，讓你的 Agent 輕裝上陣。**

---

## 附錄

### 附錄 A: Context Diet Middleware 程式碼

```typescript
// context-diet.middleware.ts
export class ContextDietMiddleware {
  private config: DietConfig;
  
  async process(context: Context): Promise<OptimizedContext> {
    // 1. 分析
    const analysis = await this.analyzer.analyze(context);
    
    // 2. 分類
    const classified = this.classifier.classify(analysis);
    
    // 3. 壓縮
    const compressed = await this.compressor.compress(
      classified, 
      this.config.compression
    );
    
    // 4. 優化
    return this.optimizer.optimize(compressed);
  }
}
```

### 附錄 B: 9Router 整合配置

```yaml
# 9router-context-diet.yaml
routes:
  - name: context-managed-endpoint
    target: gemini-3.1-pro-preview
    middleware:
      - context_diet:
          max_tokens: 8000
          compression: full
          amnesia_rules:
            - type: tool_output
              ttl: 300
```

### 附錄 C: 術語表

| 術語 | 定義 |
|------|------|
| Context Bloat | Context 累積導致的效率下降 |
| CER | Context Efficiency Ratio |
| Search-over-Context | 以搜尋取代完整 context 傳遞 |
| Selective Amnesia | 選擇性遺忘策略 |
| Header-Aware Chunking | 帶標頭的內容摘要技術 |

---

*文件版本: 1.0*  
*最後更新: 2026-04-20*  
*狀態: ✅ 大綱完成，待內容產出*
