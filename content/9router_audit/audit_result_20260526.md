🔄 開始解析 9Router 戰情資料... (過濾條件: 過去 24 小時內)

### 📊 9Router 戰情報告 (近期數據)

**分析區間**: 過去 24 小時
**總請求數 (Total Requests)**: 72
**成功率 (Success Rate)**: 48.61%
**平均延遲 (Avg Latency)**: 9540 ms
**總估算成本 (Total Cost)**: $0.0000 USD

#### 🤖 系統模型配置現況 (Who Uses What)
當前 `openclaw.json` 中配置的模型與其綁定對象：

- **`9router/combo3`**
  - 🎯 Default (Primary)
  - 🎯 Agent: 蝦仁 (Fallback 1)
  - 🎯 Agent: 蝦餅 (Primary)
- **`google/gemini-2.5-flash`**
  - 🎯 Default (Fallback 1)
- **`google-vertex/gemini-2.5-flash`**
  - 🎯 Agent: 蝦仁 (Primary)
- **`9router/combo2`**
  - 🎯 Agent: 蝦皮 (Primary)
  - 🎯 Agent: 蝦捲 (Primary)
- **`9router/combo1`**
  - 🎯 Agent: 蝦米 (Primary)

#### 📉 實際消耗統計 (Real Usage from 9Router)
| 模型 (Provider/Model) | 請求數 | Input Tokens | Output Tokens | 估算成本 | 綁定狀況 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| openrouter/nemotron-3-nano-30b-a3b:free | 157 | 265795 | 639827 | $0.0000 | ⚠️ 未知/過時 (Orphan) |
| gemini/gemma-4-31b-it | 4 | 8 | 56 | $0.0000 | ⚠️ 未知/過時 (Orphan) |

#### ⚠️ 異常狀態統計 (Error Stats)
| 錯誤類型 / 狀態 | 發生次數 |
| :--- | :--- |
| error | 37 |
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1:20128...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* Connected to 127.0.0.1 (127.0.0.1) port 20128 (#0)
> POST /v1/chat/completions HTTP/1.1
> Host: 127.0.0.1:20128
> User-Agent: curl/7.81.0
> Accept: */*
> Content-Type: application/json
> Authorization: Bearer sk-9router
> Content-Length: 96
> 
} [96 bytes data]
100    96    0     0  100    96      0     79  0:00:01  0:00:01 --:--:--    79* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< vary: rsc, next-router-state-tree, next-router-prefetch, next-router-segment-prefetch
< access-control-allow-origin: *
< cache-control: no-cache
< connection: keep-alive
< content-type: text/event-stream
< Date: Tue, 26 May 2026 21:56:53 GMT
< Transfer-Encoding: chunked
< 
{ [793 bytes data]
100   884    0   788  100    96    600     73  0:00:01  0:00:01 --:--:--   675
* Connection #0 to host 127.0.0.1 left intact
data: {"id":"chatcmpl-JBcWavWMFbzR-8YPpPT52Ao","object":"chat.completion.chunk","created":1779832613,"model":"gemma-4-31b-it","choices":[{"index":0,"delta":{"role":"assistant"},"finish_reason":null}]}

data: {"id":"chatcmpl-JBcWavWMFbzR-8YPpPT52Ao","object":"chat.completion.chunk","created":1779832613,"model":"gemma-4-31b-it","choices":[{"index":0,"delta":{"content":"\"Latency check\"\nThe user wants to know if the system is"},"finish_reason":null}]}

data: {"id":"chatcmpl-JBcWavWMFbzR-8YPpPT52Ao","object":"chat.completion.chunk","created":1779832613,"model":"gemma-4-31b-it","choices":[{"index":0,"delta":{},"finish_reason":"max_tokens"}],"usage":{"prompt_tokens":2003,"completion_tokens":14,"total_tokens":2017,"completion_tokens_details":{"reasoning_tokens":14}}}

data: [DONE]

