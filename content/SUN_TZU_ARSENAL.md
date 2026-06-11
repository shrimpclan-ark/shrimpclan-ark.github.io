# ⚔️ 認知之核：兵器庫全陣圖 (孫子 Feedback)

> *「多算勝，少算不勝。」——孫子・始計篇*
> 
> 激情是燃料，但孫子不打無準備之仗。揚帆前，先繪海圖——以下是「認知之核」的完整兵器陣列，附帶真實基準數據，供你精算後再出征。

## 嵌入層兵器選擇 (Embedding Layer)

| 模型 | Top-5 命中率 | 查詢延遲 | 推薦場景 |
|---|---|---|---|
| MiniLM-L6-v2 | 78.1% | 68ms | 快速原型、資源極度受限 |
| E5-Base-v2 | 83.5% | 79ms | 平衡型、英文RAG |
| BGE-Base-v1.5 | 84.7% | 82ms | 多語言、可微調 |
| **nomic-embed-text-v1** | **86.2%** | **110ms** | **長文本、語意深度最佳 (推薦)** |

**蝦家班關鍵建議**：認知失調偵測需要語意深度，優先選 `nomic-embed-text-v1`。若有繁體中文語料，`BGE-M3` 更適合在地化場景。

## 推理引擎 (Inference Engine)：2026 零成本 LLM 完整清單

**LLaMA-2-7B-Chat 已是過時武器，放下它！**

*   **OpenRouter**：`meta-llama/llama-3.3-70b-instruct:free` ($0/百萬 tokens)
*   **Together.ai**：Llama 3.3 70B 免費端點
*   **SambaNova**：Llama 3.3 70B + Qwen 2.5 72B (永久免費層)
*   **DeepSeek API**：DeepSeek V3/R1 (極低成本)

## 向量資料庫 (Vector DB)：LanceDB 本地要塞

LanceDB OSS 以 embedded 模式運行，零伺服器成本、閒置時資源歸零。`nomic-embed-text-v1` 基礎版在 RTX 3090 上推理僅需 12ms，模型體積 320MB。

## 完整零成本技術棧 (The Zero-Cost Stack)

```
認知之核架構
───────────────────────────────────────────────
[輸入層] 團隊筆記 / Markdown / 對話紀錄
 ↓
[嵌入層] nomic-embed-text-v1 (本地運行, 免費)
 ↓
[儲存層] LanceDB OSS embedded mode (本地, 免費)
 ↓
[檢索層] Hybrid Search: Dense + BM25 稀疏檢索
 ↓
[推理層] OpenRouter Llama 3.3 70B (免費 API)
 └─ 備援: SambaNova / DeepSeek
 ↓
[輸出層] 認知失調偵測報告 / 靈感共鳴圖譜
───────────────────────────────────────────────
月成本估計：$0 ~ $1.5 美元
```

## 孫子的一記冷水 (The Cold Truth)

1.  **力分則弱**：不要急著散佈「全宇宙」。先讓核心在團隊內部跑通，產生真實有用的洞察。
2.  **放下舊刀**：LLaMA-2 是舊刀，優先使用 OpenRouter 免費的 Llama 3.3 70B 雲端推理，而非本地小模型。
3.  **建核需慢，散佈需快**：先花三天把認知之核跑起來，再花一天把結果截圖發出去。

**今日行動**：在本地安裝 `nomic-embed-text-v1` + `LanceDB`，驗證「認知失調偵測」的召回率。