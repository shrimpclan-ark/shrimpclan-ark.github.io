# OpenClaw System Architecture (v2.13+)

> Based on source code analysis of `OpenClaw_repo` (v2026.2.13/17).
> Last Updated: 2026-02-24

## 系統架構與資料流向 (System Overview & Data Flow)

```mermaid
graph TD
    %% 外部通訊頻道 (Channels)
    subgraph Channels [外部通訊頻道 (Inbound/Outbound DMs & Groups)]
      WhatsApp[WhatsApp]
      Telegram[Telegram]
      Slack[Slack]
      Discord[Discord]
      Signal[Signal]
      Other[其他: iMessage, WebChat...]
    end

    %% Gateway 控制層
    subgraph ControlPlane [Gateway 核心控制層 (ws://127.0.0.1:18789)]
      Gateway((Gateway Daemon))
      Router{多代理路由<br/>Multi-agent Routing}
      SessionMgr[會話與上下文管理<br/>Session & Memory]
      Auth[安全與驗證<br/>Security & Pairing]
    end

    %% Agent 執行層
    subgraph Agents [Agent 運算層 (LLM & Logic)]
      PiAgent[Pi Agent (RPC模式)<br/>任務與工具調用]
      Cron[排程與喚醒<br/>Cron & Wakeups]
    end

    %% 終端與節點層
    subgraph Nodes [客戶端與設備節點層 (Clients & Nodes)]
      CLI[OpenClaw CLI]
      WebUI[Control UI / WebChat]
      macOS[macOS App / Canvas]
      Mobile[iOS / Android Nodes<br/>Camera, Voice, PTT]
    end

    %% 資料流程線
    WhatsApp -.->|Webhook/API| Gateway
    Telegram -.->|Webhook/API| Gateway
    Slack -.->|Webhook/API| Gateway
    Discord -.->|Webhook/API| Gateway
    Signal -.->|Webhook/API| Gateway
    Other -.->|Webhook/API| Gateway

    Gateway -->|1. 接收與驗證| Auth
    Auth -->|2. 建立/恢復會話| SessionMgr
    SessionMgr -->|3. 分發任務| Router
    Router ===>|4. RPC 請求| PiAgent
    PiAgent -->|5. 調用工具 (Browser/Files)| Gateway
    Gateway -->|6. 觸發設備功能| Nodes

    CLI <-->|WebSocket/API| Gateway
    WebUI <-->|WebSocket/API| Gateway
    macOS <-->|WebSocket/API| Gateway
    Mobile <-->|WebSocket/API| Gateway

    Cron -->|定時觸發| Router
```

## 重點解析 (Key Components)

1.  **統一入口 (Gateway Control Plane)**：
    所有的外部訊息（Telegram、Discord 等）都會統一匯集到本機的 Gateway（透過 WebSocket 或 Webhook 機制）。

2.  **安全與會話 (Security & Session)**：
    Gateway 接收到訊息後，會先經過 DM Pairing 驗證（擋掉未知的私訊），然後提取並恢復對應的 Session 記憶。
    *   *Issue Note (2026-02-24)*: 在雲端/Docker環境內部自回環調用時，需注意 Pairing/Auth 策略可能導致 `1008 Policy Violation`。

3.  **運算核心 (Pi Agent)**：
    經過路由分配後，實際的 LLM 推理與工具調用（例如讀檔、上網）是在 Pi Agent 執行，透過 RPC 模式與 Gateway 溝通。

4.  **設備連動 (Nodes)**：
    當 Agent 需要看畫面、說話、或是操作 Canvas 時，會透過 Gateway 將指令下發到 macOS、iOS 或 Android 節點上。
