# 嵌入

[跳至主要內容](#main-content)

*   [Gemini API](https://ai.google.dev/gemini-api/docs)
    *   [文件](https://ai.google.dev/gemini-api/docs)
    *   [API 參考資料](https://ai.google.dev/api)
*   [取得 API 金鑰](https://aistudio.google.com/apikey)
*   [教戰手冊](https://github.com/google-gemini/cookbook)
*   [Community](https://discuss.ai.google.dev/c/gemini-api/)

*   開始使用
    
*   [總覽](https://ai.google.dev/gemini-api/docs)
*   [快速入門導覽課程](https://ai.google.dev/gemini-api/docs/quickstart)
*   [API 金鑰](https://ai.google.dev/gemini-api/docs/api-key)
*   [程式庫](https://ai.google.dev/gemini-api/docs/libraries)
*   [定價](https://ai.google.dev/gemini-api/docs/pricing)
*   [Interactions API](https://ai.google.dev/gemini-api/docs/interactions)
*   模型
    
*   [所有模型](https://ai.google.dev/gemini-api/docs/models)
*   [Gemini 3](https://ai.google.dev/gemini-api/docs/gemini-3)
*   [Nano Banana](https://ai.google.dev/gemini-api/docs/image-generation)
*   [Veo](https://ai.google.dev/gemini-api/docs/video)
*   [Lyria](https://ai.google.dev/gemini-api/docs/music-generation)
*   [Imagen](https://ai.google.dev/gemini-api/docs/imagen)
*   [文字轉語音](https://ai.google.dev/gemini-api/docs/speech-generation)
*   [嵌入](https://ai.google.dev/gemini-api/docs/embeddings)
*   [機器人工學](https://ai.google.dev/gemini-api/docs/robotics-overview)
*   核心功能
    
*   [文字](https://ai.google.dev/gemini-api/docs/text-generation)

*   [文件](https://ai.google.dev/gemini-api/docs/document-processing)

*   [結構化輸出內容](https://ai.google.dev/gemini-api/docs/structured-output)
*   [函式呼叫](https://ai.google.dev/gemini-api/docs/function-calling)
*   [詳細背景資訊](https://ai.google.dev/gemini-api/docs/long-context)
*   工具和代理程式
    
*   [總覽](https://ai.google.dev/gemini-api/docs/tools)
*   [Deep Research](https://ai.google.dev/gemini-api/docs/deep-research)
*   [Google Search](https://ai.google.dev/gemini-api/docs/google-search)
*   [Google Maps](https://ai.google.dev/gemini-api/docs/maps-grounding)
*   [執行程式碼](https://ai.google.dev/gemini-api/docs/code-execution)
*   [網址背景資訊](https://ai.google.dev/gemini-api/docs/url-context)
*   [電腦使用](https://ai.google.dev/gemini-api/docs/computer-use)
*   [檔案搜尋](https://ai.google.dev/gemini-api/docs/file-search)
*   Live API
    
*   [總覽](https://ai.google.dev/gemini-api/docs/live-api)

*   [功能](https://ai.google.dev/gemini-api/docs/live-api/capabilities)
*   [使用工具](https://ai.google.dev/gemini-api/docs/live-api/tools)
*   [工作階段管理](https://ai.google.dev/gemini-api/docs/live-api/session-management)
*   [暫時性權杖](https://ai.google.dev/gemini-api/docs/live-api/ephemeral-tokens)
*   [最佳做法](https://ai.google.dev/gemini-api/docs/live-api/best-practices)
*   指南
    
*   [程式設計代理程式技能](https://ai.google.dev/gemini-api/docs/coding-agents)
*   [Batch API](https://ai.google.dev/gemini-api/docs/batch-api)

*   [內容快取](https://ai.google.dev/gemini-api/docs/caching)
*   [OpenAI 相容性](https://ai.google.dev/gemini-api/docs/openai)
*   [媒體解析度](https://ai.google.dev/gemini-api/docs/media-resolution)
*   [符記計數](https://ai.google.dev/gemini-api/docs/tokens)
*   [提示工程](https://ai.google.dev/gemini-api/docs/prompting-strategies)

*   架構
    
    *   [LangChain 和 LangGraph](https://ai.google.dev/gemini-api/docs/langgraph-example)
    *   [CrewAI](https://ai.google.dev/gemini-api/docs/crewai-example)
    *   [LlamaIndex](https://ai.google.dev/gemini-api/docs/llama-index)
    *   [Vercel AI SDK](https://ai.google.dev/gemini-api/docs/vercel-ai-sdk-example)
    *   [暫時](https://ai.google.dev/gemini-api/docs/temporal-example)
    
*   資源
    
*   [版本資訊](https://ai.google.dev/gemini-api/docs/changelog)
*   [淘汰項目](https://ai.google.dev/gemini-api/docs/deprecations)
*   [頻率限制](https://ai.google.dev/gemini-api/docs/rate-limits)
*   [帳單資訊](https://ai.google.dev/gemini-api/docs/billing)
*   [遷移至 Gen AI SDK](https://ai.google.dev/gemini-api/docs/migrate)
*   [API 疑難排解](https://ai.google.dev/gemini-api/docs/troubleshooting)
*   [合作夥伴和程式庫整合](https://ai.google.dev/gemini-api/docs/partner-integration)

*   政策
    
*   [服務條款](https://ai.google.dev/gemini-api/terms)
*   [可用地區](https://ai.google.dev/gemini-api/docs/available-regions)
*   [濫用行為監控](https://ai.google.dev/gemini-api/docs/usage-policies)
*   [意見回饋資訊](https://ai.google.dev/gemini-api/docs/feedback-policies)

## 嵌入

*   這個頁面中的內容
*   [生成嵌入](#generate-embeddings)
*   [指定要提升成效的工作類型](#task-types)
    *   [支援的工作類型](#supported-task-types)
*   [控制嵌入大小](#control-embedding-size)
*   [確保較小尺寸的品質](#quality-for-smaller-dimensions)
*   [多模態嵌入](#multimodal)
    *   [支援的模態和限制](#supported-modalities)
    *   [嵌入圖片](#embed-images)
    *   [嵌入匯總](#embedding-aggregation)
    *   [嵌入音訊](#embed-audio)
    *   [嵌入影片](#embed-video)
    *   [嵌入文件](#embed-documents)
*   [用途](#common-use-cases)
*   [儲存嵌入](#store-embeddings)
*   [模型版本](#model-versions)
*   [從 gemini-embedding-001 遷移](#migration)
*   [批次嵌入](#batch-embedding)
*   [負責任的使用方式通知](#responsible-use-notice)
*   [開始使用嵌入建構內容](#start-building)

Gemini API 提供嵌入模型，可為文字、圖片、影片和其他內容生成嵌入內容。這些產生的嵌入內容可用於語意搜尋、分類和叢集等工作，與關鍵字方法相比，可提供更準確、符合情境的結果。

最新模型 `gemini-embedding-2-preview` 是 Gemini API 中的第一個多模態嵌入模型。這項技術會將文字、圖片、影片、音訊和文件對應到統一的嵌入空間，支援超過 100 種語言的跨模態搜尋、分類和叢集。詳情請參閱[多模態嵌入部分](#multimodal)。如要處理純文字內容，仍可使用 `gemini-embedding-001`。

建構檢索增強生成 (RAG) 系統是 AI 產品的常見用途。嵌入在大幅提升模型輸出內容方面扮演關鍵角色，可提高事實準確度、連貫性和情境豐富度。如要使用代管型 RAG 解決方案，我們打造了 [File Search](https://ai.google.dev/gemini-api/docs/file-search?hl=zh-tw) 工具，讓您更輕鬆管理 RAG，並提高成本效益。

## 生成嵌入

使用 `embedContent` 方法生成文字嵌入：

```
from google import genai

client = genai.Client()

result = client.models.embed_content(
        model="gemini-embedding-001",
        contents="What is the meaning of life?"
)

print(result.embeddings)
```

```
import { GoogleGenAI } from "@google/genai";

async function main() {

    const ai = new GoogleGenAI({});

    const response = await ai.models.embedContent({
        model: 'gemini-embedding-001',
        contents: 'What is the meaning of life?',
    });

    console.log(response.embeddings);
}

main();
```

```
package main

import (
    "context"
    "encoding/json"
    "fmt"
    "log"

    "google.golang.org/genai"
)

func main() {
    ctx := context.Background()
    client, err := genai.NewClient(ctx, nil)
    if err != nil {
        log.Fatal(err)
    }

    contents := []*genai.Content{
        genai.NewContentFromText("What is the meaning of life?", genai.RoleUser),
    }
    result, err := client.Models.EmbedContent(ctx,
        "gemini-embedding-001",
        contents,
        nil,
    )
    if err != nil {
        log.Fatal(err)
    }

    embeddings, err := json.MarshalIndent(result.Embeddings, "", "  ")
    if err != nil {
        log.Fatal(err)
    }
    fmt.Println(string(embeddings))
}
```

```
curl "https://generativelanguage.googleapis.com/v1beta/models/gemini-embedding-001:embedContent" \
    -H "Content-Type: application/json" \
    -H "x-goog-api-key: ${GEMINI_API_KEY}" \
    -d '{
        "model": "models/gemini-embedding-001",
        "content": {
        "parts": [{
            "text": "What is the meaning of life?"
        }]
        }
    }'
```

您也可以將多個區塊以字串清單的形式傳遞，一次產生多個區塊的嵌入內容。

```
from google import genai

client = genai.Client()

result = client.models.embed_content(
        model="gemini-embedding-001",
        contents= [
            "What is the meaning of life?",
            "What is the purpose of existence?",
            "How do I bake a cake?"
        ]
)

for embedding in result.embeddings:
    print(embedding)
```

```
import { GoogleGenAI } from "@google/genai";

async function main() {

    const ai = new GoogleGenAI({});

    const response = await ai.models.embedContent({
        model: 'gemini-embedding-001',
        contents: [
            'What is the meaning of life?',
            'What is the purpose of existence?',
            'How do I bake a cake?'
        ],
    });

    console.log(response.embeddings);
}

main();
```

```
package main

import (
    "context"
    "encoding/json"
    "fmt"
    "log"

    "google.golang.org/genai"
)

func main() {
    ctx := context.Background()
    client, err := genai.NewClient(ctx, nil)
    if err != nil {
        log.Fatal(err)
    }

    contents := []*genai.Content{
        genai.NewContentFromText("What is the meaning of life?"),
        genai.NewContentFromText("How does photosynthesis work?"),
        genai.NewContentFromText("Tell me about the history of the internet."),
    }
    result, err := client.Models.EmbedContent(ctx,
        "gemini-embedding-001",
        contents,
        nil,
    )
    if err != nil {
        log.Fatal(err)
    }

    embeddings, err := json.MarshalIndent(result.Embeddings, "", "  ")
    if err != nil {
        log.Fatal(err)
    }
    fmt.Println(string(embeddings))
}
```

```
curl "https://generativelanguage.googleapis.com/v1beta/models/gemini-embedding-001:embedContent" \
    -H "Content-Type: application/json" \
    -H "x-goog-api-key: $GEMINI_API_KEY" \
    -d '{
    "content": {
        "parts": [
        {
            "text": "What is the meaning of life?"
        },
        {
            "text": "How much wood would a woodchuck chuck?"
        },
        {
            "text": "How does the brain work?"
        }
        ]
    },
    "taskType": "SEMANTIC_SIMILARITY"
    }'
```

## 指定要提升成效的工作類型

您可以將嵌入項目用於各種工作，從分類到文件搜尋皆可。指定正確的任務類型有助於針對預期關係最佳化嵌入項目，盡可能提高準確度和效率。如需支援的完整工作類型清單，請參閱「[支援的工作類型](#supported-task-types)」表格。

以下範例說明如何使用 `SEMANTIC_SIMILARITY` 檢查文字字串的意義相似程度。

```
from google import genai
from google.genai import types
import pandas as pd
from sklearn.metrics.pairwise import cosine_similarity

client = genai.Client()

texts = [
    "What is the meaning of life?",
    "What is the purpose of existence?",
    "How do I bake a cake?",
]

result = client.models.embed_content(
    model="gemini-embedding-001",
    contents=texts,
    config=types.EmbedContentConfig(task_type="SEMANTIC_SIMILARITY")
)

# Create a 3x3 table to show the similarity matrix
df = pd.DataFrame(
    cosine_similarity([e.values for e in result.embeddings]),
    index=texts,
    columns=texts,
)

print(df)
```

```
import { GoogleGenAI } from "@google/genai";
import * as cosineSimilarity from "compute-cosine-similarity";

async function main() {
    const ai = new GoogleGenAI({});

    const texts = [
        "What is the meaning of life?",
        "What is the purpose of existence?",
        "How do I bake a cake?",
    ];

    const response = await ai.models.embedContent({
        model: 'gemini-embedding-001',
        contents: texts,
        taskType: 'SEMANTIC_SIMILARITY'
    });

    const embeddings = response.embeddings.map(e => e.values);

    for (let i = 0; i < texts.length; i++) {
        for (let j = i + 1; j < texts.length; j++) {
            const text1 = texts[i];
            const text2 = texts[j];
            const similarity = cosineSimilarity(embeddings[i], embeddings[j]);
            console.log(`Similarity between '${text1}' and '${text2}': ${similarity.toFixed(4)}`);
        }
    }
}

main();
```

```
package main

import (
    "context"
    "fmt"
    "log"
    "math"

    "google.golang.org/genai"
)

// cosineSimilarity calculates the similarity between two vectors.
func cosineSimilarity(a, b []float32) (float64, error) {
    if len(a) != len(b) {
        return 0, fmt.Errorf("vectors must have the same length")
    }

    var dotProduct, aMagnitude, bMagnitude float64
    for i := 0; i < len(a); i++ {
        dotProduct += float64(a[i] * b[i])
        aMagnitude += float64(a[i] * a[i])
        bMagnitude += float64(b[i] * b[i])
    }

    if aMagnitude == 0 || bMagnitude == 0 {
        return 0, nil
    }

    return dotProduct / (math.Sqrt(aMagnitude) * math.Sqrt(bMagnitude)), nil
}

func main() {
    ctx := context.Background()
    client, _ := genai.NewClient(ctx, nil)
    defer client.Close()

    texts := []string{
        "What is the meaning of life?",
        "What is the purpose of existence?",
        "How do I bake a cake?",
    }

    var contents []*genai.Content
    for _, text := range texts {
        contents = append(contents, genai.NewContentFromText(text, genai.RoleUser))
    }

    result, _ := client.Models.EmbedContent(ctx,
        "gemini-embedding-001",
        contents,
        &genai.EmbedContentRequest{TaskType: genai.TaskTypeSemanticSimilarity},
    )

    embeddings := result.Embeddings

    for i := 0; i < len(texts); i++ {
        for j := i + 1; j < len(texts); j++ {
            similarity, _ := cosineSimilarity(embeddings[i].Values, embeddings[j].Values)
            fmt.Printf("Similarity between '%s' and '%s': %.4f\n", texts[i], texts[j], similarity)
        }
    }
}
```

```
curl "https://generativelanguage.googleapis.com/v1beta/models/gemini-embedding-001:embedContent" \
    -H "Content-Type: application/json" \
    -H "x-goog-api-key: $GEMINI_API_KEY" \
    -d '{
    "taskType": "SEMANTIC_SIMILARITY",
    "content": {
        "parts": [
        {
            "text": "What is the meaning of life?"
        },
        {
            "text": "How much wood would a woodchuck chuck?"
        },
        {
            "text": "How does the brain work?"
        }
        ]
    }
    }'
```

執行程式碼片段後，您會看到不同文字區塊的相似程度。

### 支援的工作類型

工作類型

說明

範例

**SEMANTIC\_SIMILARITY**

經過最佳化處理的嵌入，可評估文字相似度。

推薦系統、重複內容偵測

**分類**

經過最佳化調整的嵌入模型，可根據預設標籤分類文字。

情緒分析、垃圾訊息偵測

**分群**

經過最佳化，可根據相似度將文字分組。

文件整理、市場調查、異常偵測

**RETRIEVAL\_DOCUMENT**

針對文件搜尋最佳化的嵌入內容。

為文章、書籍或網頁建立索引，方便搜尋。

**RETRIEVAL\_QUERY**

針對一般搜尋查詢最佳化的嵌入內容。 查詢時使用 `RETRIEVAL_QUERY`，擷取文件時使用 `RETRIEVAL_DOCUMENT`。

自訂搜尋

**CODE\_RETRIEVAL\_QUERY**

經過最佳化調整的嵌入，可根據自然語言查詢擷取程式碼區塊。 使用 `CODE_RETRIEVAL_QUERY` 查詢；使用 `RETRIEVAL_DOCUMENT` 擷取程式碼區塊。

程式碼建議和搜尋

**QUESTION\_ANSWERING**

問答系統中的問題嵌入，經過最佳化處理，可找出回答問題的文件。 使用 `QUESTION_ANSWERING` 提問；使用 `RETRIEVAL_DOCUMENT` 擷取文件。

Chatbox

**FACT\_VERIFICATION**

需要驗證的陳述內容的嵌入內容，經過最佳化處理，可擷取含有佐證或反駁陳述內容的文件。 使用 `FACT_VERIFICATION` 做為目標文字；使用 `RETRIEVAL_DOCUMENT` 做為要擷取的檔案

自動事實查核系統

## 控制嵌入大小

`gemini-embedding-001` 和 `gemini-embedding-2-preview` 都是使用 Matryoshka Representation Learning (MRL) 技術訓練而成，這項技術可讓模型學習高維度嵌入，這些嵌入具有初始區段 (或前置字元)，也是相同資料的實用簡化版本。

使用 `output_dimensionality` 參數控制輸出嵌入向量的大小。選取較小的輸出維度可節省儲存空間，並提高下游應用程式的運算效率，同時不會犧牲太多品質。這兩個模型預設都會輸出 3072 維度的嵌入內容，但您可以將其截斷為較小的尺寸，以節省儲存空間，且不會降低品質。建議使用 768、1536 或 3072 的輸出維度。

```
from google import genai
from google.genai import types

client = genai.Client()

result = client.models.embed_content(
    model="gemini-embedding-001",
    contents="What is the meaning of life?",
    config=types.EmbedContentConfig(output_dimensionality=768)
)

[embedding_obj] = result.embeddings
embedding_length = len(embedding_obj.values)

print(f"Length of embedding: {embedding_length}")
```

```
import { GoogleGenAI } from "@google/genai";

async function main() {
    const ai = new GoogleGenAI({});

    const response = await ai.models.embedContent({
        model: 'gemini-embedding-001',
        content: 'What is the meaning of life?',
        outputDimensionality: 768,
    });

    const embeddingLength = response.embedding.values.length;
    console.log(`Length of embedding: ${embeddingLength}`);
}

main();
```

```
package main

import (
    "context"
    "fmt"
    "log"

    "google.golang.org/genai"
)

func main() {
    ctx := context.Background()
    // The client uses Application Default Credentials.
    // Authenticate with 'gcloud auth application-default login'.
    client, err := genai.NewClient(ctx, nil)
    if err != nil {
        log.Fatal(err)
    }
    defer client.Close()

    contents := []*genai.Content{
        genai.NewContentFromText("What is the meaning of life?", genai.RoleUser),
    }

    result, err := client.Models.EmbedContent(ctx,
        "gemini-embedding-001",
        contents,
        &genai.EmbedContentRequest{OutputDimensionality: 768},
    )
    if err != nil {
        log.Fatal(err)
    }

    embedding := result.Embeddings[0]
    embeddingLength := len(embedding.Values)
    fmt.Printf("Length of embedding: %d\n", embeddingLength)
}
```

```
curl -X POST "https://generativelanguage.googleapis.com/v1beta/models/gemini-embedding-001:embedContent" \
    -H 'Content-Type: application/json' \
    -H "x-goog-api-key: $GEMINI_API_KEY" \
    -d '{
        "content": {"parts":[{ "text": "What is the meaning of life?"}]},
        "output_dimensionality": 768
    }'
```

程式碼片段的輸出範例如下：

```
Length of embedding: 768
```

## 確保較小尺寸的品質

3072 維度嵌入項目已正規化。正規化嵌入會比較向量方向 (而非大小)，因此可產生更準確的語意相似度。如為其他維度 (包括 768 和 1536)，您需要按照下列方式將嵌入內容正規化：

```
import numpy as np
from numpy.linalg import norm

embedding_values_np = np.array(embedding_obj.values)
normed_embedding = embedding_values_np / np.linalg.norm(embedding_values_np)

print(f"Normed embedding length: {len(normed_embedding)}")
print(f"Norm of normed embedding: {np.linalg.norm(normed_embedding):.6f}") # Should be very close to 1
```

這個程式碼片段的輸出範例如下：

```
Normed embedding length: 768
Norm of normed embedding: 1.000000
```

下表顯示不同維度的 MTEB 分數，這是常用的嵌入內容基準。值得注意的是，結果顯示效能並非與嵌入維度大小嚴格相關，較低的維度可達到與較高維度相當的分數。

MRL Dimension

MTEB 分數

2048

68.16

1536

68.17

768

67.99

512

67.55

256

66.19

128

63.31

## 多模態嵌入

`gemini-embedding-2-preview` 模型支援多模態輸入，可讓您在文字中嵌入圖片、影片、音訊和文件內容。所有模態都會對應到相同的嵌入空間，因此可以進行跨模態搜尋和比較。

### 支援的模態和限制

輸入權杖總數上限為 8192 個。

模態

規格和限制

**Text**

最多支援 8,192 個權杖。

**圖片**

每個要求最多可包含 6 張圖片。支援的格式：PNG、JPEG。

**音訊**

時間長度上限為 80 秒。支援的格式：MP3、WAV。

**影片**

時間長度上限為 128 秒。支援的格式：MP4、MOV。支援的轉碼器：H264、H265、AV1、VP9

**文件 (PDF)**

最多 6 頁。

### 嵌入圖片

以下範例說明如何使用 `gemini-embedding-2-preview` 內嵌圖片。

圖片可以內嵌資料的形式提供，也可以透過 [Files API](https://ai.google.dev/gemini-api/docs/files?hl=zh-tw) 上傳檔案。

```
from google import genai
from google.genai import types

with open('example.png', 'rb') as f:
    image_bytes = f.read()

client = genai.Client()

result = client.models.embed_content(
    model='gemini-embedding-2-preview',
    contents=[
        types.Part.from_bytes(
            data=image_bytes,
            mime_type='image/png',
        ),
    ]
)

print(result.embeddings)
```

```
import { GoogleGenAI } from "@google/genai";
import * as fs from "node:fs";

async function main() {
    const ai = new GoogleGenAI({});

    const imgBase64 = fs.readFileSync("example.png", { encoding: "base64" });

    const response = await ai.models.embedContent({
        model: 'gemini-embedding-2-preview',
        contents: [{
            inlineData: {
                mimeType: 'image/png',
                data: imgBase64,
            },
        }],
    });

    console.log(response.embeddings);
}

main();
```

```
IMG_PATH="/path/to/your/image.png"
IMG_BASE64=$(base64 -w0 "${IMG_PATH}")

curl "https://generativelanguage.googleapis.com/v1beta/models/gemini-embedding-2-preview:embedContent" \
    -H "Content-Type: application/json" \
    -H "x-goog-api-key: ${GEMINI_API_KEY}" \
    -d '{
        "content": {
            "parts": [{
                "inline_data": {
                    "mime_type": "image/png",
                    "data": "'"${IMG_BASE64}"'"
                }
            }]
        }
    }'
```

### 嵌入匯總

使用多模態內容時，輸入內容的結構會影響嵌入輸出內容：

*   **單一內容項目：**在單一內容項目中提交多個部分 (例如文字和圖片)，系統會為該項目中的所有模態產生一個匯總嵌入內容。
*   **多個項目：**在 `contents` 陣列中傳送多個項目，系統會為每個項目分別傳回嵌入內容。
*   **貼文層級表示法：**對於複雜的物件 (例如含有多個媒體項目的社群媒體貼文)，建議您匯總個別的嵌入 (例如取平均值)，建立連貫的貼文層級表示法。

以下範例說明如何為文字和圖片輸入內容建立一個匯總嵌入內容。 使用 `parts` 欄位合併多項輸入內容：

```
from google import genai
from google.genai import types

with open('dog.png', 'rb') as f:
    image_bytes = f.read()

result = client.models.embed_content(
    model='gemini-embedding-2-preview',
    contents=[
        types.Content(
            parts=[
                types.Part(text="An image of a dog"),
                types.Part.from_bytes(
                    data=image_bytes,
                    mime_type='image/png',
                )
            ]
        )
    ]
)

# This produces one embedding
for embedding in result.embeddings:
    print(embedding.values)
```

```
import { GoogleGenAI } from "@google/genai";
import * as fs from "node:fs";

async function main() {
    const ai = new GoogleGenAI({});

    const imgBase64 = fs.readFileSync("dog.png", { encoding: "base64" });

    const response = await ai.models.embedContent({
        model: 'gemini-embedding-2-preview',
        contents: {
            parts: [
                { text: 'An image of a dog' },
                { inlineData: { mimeType: 'image/png', data: imgBase64 } },
            ],
        },
    });

    console.log(response.embeddings);
}

main();
```

```
IMG_PATH="/path/to/your/dog.png"
IMG_BASE64=$(base64 -w0 "${IMG_PATH}")

curl "https://generativelanguage.googleapis.com/v1beta/models/gemini-embedding-2-preview:embedContent" \
    -H "Content-Type: application/json" \
    -H "x-goog-api-key: ${GEMINI_API_KEY}" \
    -d '{
        "content": {
            "parts": [
                {"text": "An image of a dog"},
                {
                    "inline_data": {
                        "mime_type": "image/png",
                        "data": "'"${IMG_BASE64}"'"
                    }
                }
            ]
        }
    }'
```

另一方面，這個範例會在一次嵌入呼叫中建立多個嵌入：

```
from google import genai
from google.genai import types

with open('dog.png', 'rb') as f:
    image_bytes = f.read()

result = client.models.embed_content(
    model='gemini-embedding-2-preview',
    contents=[
        "The dog is cute",
        types.Part.from_bytes(
            data=image_bytes,
            mime_type='image/png',
        ),
    ]
)

# This produces two embeddings
for embedding in result.embeddings:
    print(embedding.values)
```

```
import { GoogleGenAI } from "@google/genai";
import * as fs from "node:fs";

async function main() {
    const ai = new GoogleGenAI({});

    const imgBase64 = fs.readFileSync("dog.png", { encoding: "base64" });

    const response = await ai.models.embedContent({
        model: 'gemini-embedding-2-preview',
        contents: [
            'The dog is cute',
            {
                inlineData: {
                    mimeType: 'image/png',
                    data: imgBase64,
                },
            },
        ],
    });

    console.log(response.embeddings);
}

main();
```

```
IMG_PATH="/path/to/your/dog.png"
IMG_BASE64=$(base64 -w0 "${IMG_PATH}")

curl "https://generativelanguage.googleapis.com/v1beta/models/gemini-embedding-2-preview:batchEmbedContents" \
    -H "Content-Type: application/json" \
    -H "x-goog-api-key: ${GEMINI_API_KEY}" \
    -d '{
        "requests": [
            {
                "model": "models/gemini-embedding-2-preview",
                "content": {"parts": [{"text": "The dog is cute"}]}
            },
            {
                "model": "models/gemini-embedding-2-preview",
                "content": {"parts": [{"inline_data": {"mime_type": "image/png", "data": "'"${IMG_BASE64}"'"}}]}
            }
        ]
    }'
```

### 嵌入音訊

以下範例說明如何使用 `gemini-embedding-2-preview` 嵌入音訊檔案。

音訊檔案可以內嵌資料的形式提供，也可以透過 [Files API](https://ai.google.dev/gemini-api/docs/files?hl=zh-tw) 上傳。

```
from google import genai
from google.genai import types

with open('example.mp3', 'rb') as f:
    audio_bytes = f.read()

client = genai.Client()

result = client.models.embed_content(
    model='gemini-embedding-2-preview',
    contents=[
        types.Part.from_bytes(
            data=audio_bytes,
            mime_type='audio/mpeg',
        ),
    ]
)

print(result.embeddings)
```

```
import { GoogleGenAI } from "@google/genai";
import * as fs from "node:fs";

async function main() {
    const ai = new GoogleGenAI({});

    const audioBase64 = fs.readFileSync("example.mp3", { encoding: "base64" });

    const response = await ai.models.embedContent({
        model: 'gemini-embedding-2-preview',
        contents: [{
            inlineData: {
                mimeType: 'audio/mpeg',
                data: audioBase64,
            },
        }],
    });

    console.log(response.embeddings);
}

main();
```

```
AUDIO_PATH="/path/to/your/example.mp3"
AUDIO_BASE64=$(base64 -w0 "${AUDIO_PATH}")

curl "https://generativelanguage.googleapis.com/v1beta/models/gemini-embedding-2-preview:embedContent" \
    -H "Content-Type: application/json" \
    -H "x-goog-api-key: ${GEMINI_API_KEY}" \
    -d '{
        "content": {
            "parts": [{
                "inline_data": {
                    "mime_type": "audio/mpeg",
                    "data": "'"${AUDIO_BASE64}"'"
                }
            }]
        }
    }'
```

### 嵌入影片

以下範例說明如何使用 `gemini-embedding-2-preview` 嵌入影片。

影片可以內嵌資料的形式提供，也可以透過 [Files API](https://ai.google.dev/gemini-api/docs/files?hl=zh-tw) 上傳檔案。

```
from google import genai
from google.genai import types

client = genai.Client()

with open('example.mp4', 'rb') as f:
    video_bytes = f.read()

result = client.models.embed_content(
    model='gemini-embedding-2-preview',
    contents=[
        types.Part.from_bytes(
            data=video_bytes,
            mime_type='video/mp4',
        ),
    ]
)

print(result.embeddings[0].values)
```

```
import { GoogleGenAI } from "@google/genai";
import * as fs from "node:fs";

async function main() {
    const ai = new GoogleGenAI({});

    const videoBase64 = fs.readFileSync("example.mp4", { encoding: "base64" });

    const response = await ai.models.embedContent({
        model: 'gemini-embedding-2-preview',
        contents: [{
            inlineData: {
                mimeType: 'video/mp4',
                data: videoBase64,
            },
        }],
    });

    console.log(response.embeddings);
}

main();
```

```
VIDEO_PATH="/path/to/your/video.mp4"
VIDEO_BASE64=$(base64 -w0 "${VIDEO_PATH}")

curl "https://generativelanguage.googleapis.com/v1beta/models/gemini-embedding-2-preview:embedContent" \
    -H "Content-Type: application/json" \
    -H "x-goog-api-key: ${GEMINI_API_KEY}" \
    -d '{
        "content": {
            "parts": [{
                "inline_data": {
                    "mime_type": "video/mp4",
                    "data": "'"${VIDEO_BASE64}"'"
                }
            }]
        }
    }'
```

如要嵌入長度超過 128 秒的影片，可以將影片分成重疊的片段，然後個別嵌入這些片段。

### 嵌入文件

您可以直接嵌入 PDF 格式的文件。模型會處理每個網頁的圖片和文字內容。

你可以透過 [Files API](https://ai.google.dev/gemini-api/docs/files?hl=zh-tw)，以內嵌資料或上傳檔案的形式提供 PDF。

```
from google import genai
from google.genai import types

with open('example.pdf', 'rb') as f:
    pdf_bytes = f.read()

client = genai.Client()

result = client.models.embed_content(
    model='gemini-embedding-2-preview',
    contents=[
        types.Part.from_bytes(
            data=pdf_bytes,
            mime_type='application/pdf',
        ),
    ]
)

print(result.embeddings)
```

```
import { GoogleGenAI } from "@google/genai";
import * as fs from "node:fs";

async function main() {
    const ai = new GoogleGenAI({});

    const pdfBase64 = fs.readFileSync("example.pdf", { encoding: "base64" });

    const response = await ai.models.embedContent({
        model: 'gemini-embedding-2-preview',
        contents: [{
            inlineData: {
                mimeType: 'application/pdf',
                data: pdfBase64,
            },
        }],
    });

    console.log(response.embeddings);
}

main();
```

```
PDF_PATH="/path/to/your/example.pdf"
PDF_BASE64=$(base64 -w0 "${PDF_PATH}")

curl "https://generativelanguage.googleapis.com/v1beta/models/gemini-embedding-2-preview:embedContent" \
    -H "Content-Type: application/json" \
    -H "x-goog-api-key: ${GEMINI_API_KEY}" \
    -d '{
        "content": {
            "parts": [{
                "inline_data": {
                    "mime_type": "application/pdf",
                    "data": "'"${PDF_BASE64}"'"
                }
            }]
        }
    }'
```

## 用途

文字嵌入對於各種常見的 AI 用途至關重要，例如：

*   **檢索增強生成 (RAG)：**嵌入項目可擷取相關資訊並納入模型背景脈絡，提升生成文字的品質。
*   **資訊檢索：**根據輸入文字，搜尋語意最相似的文字或文件。
    
    [文件搜尋教學課程](https://github.com/google-gemini/cookbook/blob/main/examples/Talk_to_documents_with_embeddings.ipynb)
    
*   **搜尋結果重新排序**：根據查詢對初始結果進行語意評分，優先顯示最相關的項目。
    
    [搜尋重新排序教學課程](https://github.com/google-gemini/cookbook/blob/main/examples/Search_reranking_using_embeddings.ipynb)
    
*   **異常偵測：**比較嵌入群組有助於找出隱藏的趨勢或離群值。
    
    [異常偵測教學課程](https://github.com/google-gemini/cookbook/blob/main/examples/Anomaly_detection_with_embeddings.ipynb)
    
*   **分類：**根據內容自動分類文字，例如情緒分析或垃圾內容偵測
    
    [分類教學課程](https://github.com/google-gemini/cookbook/blob/main/examples/Classify_text_with_embeddings.ipynb)
    
*   **分群：**建立嵌入項目的叢集和視覺化內容，有效掌握複雜關係。
    
    [叢集視覺化教學課程](https://github.com/google-gemini/cookbook/blob/main/examples/clustering_with_embeddings.ipynb)
    

## 儲存嵌入

將嵌入投入實際應用時，通常會使用**向量資料庫**，有效率地儲存、建立索引及擷取高維度嵌入。Google Cloud 提供可供此用途的代管資料服務，包括 [BigQuery](https://cloud.google.com/bigquery/docs/introduction?hl=zh-tw)、[AlloyDB](https://cloud.google.com/alloydb/docs/overview?hl=zh-tw) 和 [Cloud SQL](https://cloud.google.com/sql/docs/postgres/introduction?hl=zh-tw)。

下列教學課程說明如何搭配 Gemini Embedding 使用其他第三方向量資料庫。

*   [ChromaDB 教學課程](https://docs.trychroma.com/integrations/embedding-models/google-gemini)
*   [QDrant 教學課程](https://qdrant.tech/documentation/embeddings/gemini/)
*   [Weaviate 教學課程](https://docs.weaviate.io/weaviate/model-providers/google)
*   [Pinecone 教學課程](https://github.com/google-gemini/cookbook/blob/main/examples/langchain/Gemini_LangChain_QA_Pinecone_WebLoad.ipynb)

## 模型版本

屬性

說明

模型代碼

**Gemini API**

`gemini-embedding-2-preview`

支援的資料類型

**輸入功率**

文字、圖片、影片、音訊、PDF

**輸出內容**

文字嵌入

代幣限制[\[\*\]](https://ai.google.dev/gemini-api/docs/tokens?hl=zh-tw)

**輸入權杖限制**

8,192

**輸出尺寸大小**

彈性，支援：128 - 3072，建議：768、1536、3072

個版本

如要瞭解詳情，請參閱[模型版本模式](https://ai.google.dev/gemini-api/docs/models/gemini?hl=zh-tw#model-versions)。

*   預覽：`gemini-embedding-2-preview`

最新更新

2025 年 11 月

屬性

說明

模型代碼

**Gemini API**

`gemini-embedding-001`

支援的資料類型

**輸入功率**

文字

**輸出內容**

文字嵌入

代幣限制[\[\*\]](https://ai.google.dev/gemini-api/docs/tokens?hl=zh-tw)

**輸入權杖限制**

2,048

**輸出尺寸大小**

彈性，支援：128 - 3072，建議：768、1536、3072

個版本

如要瞭解詳情，請參閱[模型版本模式](https://ai.google.dev/gemini-api/docs/models/gemini?hl=zh-tw#model-versions)。

*   穩定：`gemini-embedding-001`

最新更新

2025 年 6 月

如要瞭解已淘汰的 Embeddings 模型，請前往「[淘汰項目](https://ai.google.dev/gemini-api/docs/deprecations?hl=zh-tw)」頁面

## 從 gemini-embedding-001 遷移

`gemini-embedding-001` 和 `gemini-embedding-2-preview` 之間的嵌入空間**不相容**。也就是說，您無法直接比較不同模型產生的嵌入。如要升級至 `gemini-embedding-2-preview`，必須重新嵌入所有現有資料。

## 批次嵌入

如果延遲不是問題，請嘗試搭配[批次 API](https://ai.google.dev/gemini-api/docs/batch-api?hl=zh-tw#batch-embedding) 使用 Gemini Embeddings 模型。這項模型可讓您以預設 Embedding 價格的 50% 獲得更高的輸送量。如需入門範例，請參閱 [Batch API 食譜](https://github.com/google-gemini/cookbook/blob/main/quickstarts/Batch_mode.ipynb)。

## 負責任的使用方式通知

與生成新內容的生成式 AI 模型不同，Gemini Embedding 模型僅用於將輸入資料的格式轉換為數字表示法。Google 負責提供嵌入模型，將輸入資料的格式轉換為要求的數字格式，但使用者仍須全權負責輸入的資料和產生的嵌入內容。使用 Gemini Embedding 模型，即代表您確認自己具備必要權限，可使用上傳的一切內容。請勿生成會侵害他人智慧財產或隱私權的內容。使用這項服務時，請務必遵守《[使用限制政策](https://policies.google.com/terms/generative-ai/use-policy?hl=zh-tw)》和《[Google 服務條款](https://ai.google.dev/gemini-api/terms?hl=zh-tw)》。

## 開始使用嵌入建構內容

請參閱[嵌入快速入門筆記本](https://github.com/google-gemini/cookbook/blob/main/quickstarts/Embeddings.ipynb)，瞭解模型功能，以及如何自訂和視覺化呈現嵌入內容。

除非另有註明，否則本頁面中的內容是採用[創用 CC 姓名標示 4.0 授權](https://creativecommons.org/licenses/by/4.0/)，程式碼範例則為[阿帕契 2.0 授權](https://www.apache.org/licenses/LICENSE-2.0)。詳情請參閱《[Google Developers 網站政策](https://developers.google.com/site-policies?hl=zh-tw)》。Java 是 Oracle 和/或其關聯企業的註冊商標。

上次更新時間：2026-03-11 (世界標準時間)。