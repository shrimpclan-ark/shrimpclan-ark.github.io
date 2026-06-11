# AGENTS.md - 9Router Development Guide

This file provides guidance for agentic coding agents working in this repository.

## Project Overview

9Router is a smart AI router that automatically routes requests across multiple AI providers with fallback support:
- **Main App**: Next.js 16 dashboard (React 19, Tailwind CSS 4)
- **open-sse**: Core SSE handling library
- **cloud**: Cloudflare Worker for cloud sync
- **tests**: Vitest unit tests

---

## Build, Lint, and Test Commands

### Main Application

```bash
# Install dependencies
npm install

# Development
npm run dev              # Next.js dev server on port 20128
npm run dev:bun          # Using Bun runtime

# Production build
npm run build            # Build Next.js app
npm run start            # Start production server
npm run build:bun        # Build with Bun
npm run start:bun        # Start standalone server

# Linting
npm run lint             # Run ESLint
```

### Tests (Vitest)

```bash
# Run all tests
cd tests && npm test

# Run tests in watch mode
cd tests && npm run test:watch

# Run a single test file
cd tests && npm test -- embeddingsCore.test.js

# Run a specific test
cd tests && npm test -- --grep "buildEmbeddingsBody"
```

### Cloud Worker

```bash
cd cloud && npm run dev      # Local dev with Wrangler
cd cloud && npm run deploy   # Deploy to Cloudflare
```

---

## Code Style Guidelines

### General

- **Language**: JavaScript (ESM modules). No TypeScript in this project.
- **Module system**: ESM (`import`/`export`, `.js` files with `"type": "module"`)
- **Path aliases** (in `jsconfig.json`):
  - `@/*` → `./src/*`
  - `open-sse` → `./open-sse`
  - `open-sse/*` → `./open-sse/*`

### Imports

```javascript
// Use path aliases
import { getSettings } from "@/lib/localDb";
import { handleEmbeddingsCore } from "open-sse/handlers/embeddingsCore.js";

// Relative imports with .js extension
import { errorResponse } from "../../utils/error.js";
```

### Naming Conventions

- **Files**: kebab-case for utilities (`apiKey.js`), PascalCase for components (`Button.js`)
- **Functions**: camelCase (`handleEmbeddings`, `getProviderCredentials`)
- **Constants**: SCREAMING_SNAKE_CASE (`HTTP_STATUS.BAD_REQUEST`)
- **Components**: PascalCase (`export default function Modal()`)

### React/Next.js Patterns

- Use **Next.js App Router** (file-based routing in `src/app/`)
- Route files: `route.js` for handlers, `page.js` for pages
- Client components: `"use client"` directive at top

### Error Handling

```javascript
import { errorResponse, unavailableResponse } from "open-sse/utils/error.js";
import { HTTP_STATUS } from "open-sse/config/runtimeConfig.js";

// Usage
return errorResponse(HTTP_STATUS.BAD_REQUEST, "Invalid model format");
return unavailableResponse(503, "Rate limited", retryAfter, retryAfterHuman);
```

### CORS Pattern

```javascript
const CORS_HEADERS = {
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Methods": "POST, OPTIONS",
  "Access-Control-Allow-Headers": "*"
};

export async function OPTIONS() {
  return new Response(null, { headers: CORS_HEADERS });
}
```

### Logging

```javascript
import * as log from "../utils/logger.js";

log.request("POST", "/api/v1/chat");
log.info("ROUTING", `Provider: ${provider}, Model: ${model}`);
log.debug("AUTH", `API Key: ${log.maskKey(apiKey)}`);
```

### Testing (Vitest)

```javascript
import { describe, it, expect, vi, beforeEach, afterEach } from "vitest";

vi.mock("../../open-sse/executors/index.js", () => ({
  getExecutor: vi.fn(() => ({ refreshCredentials: vi.fn().mockResolvedValue(null) })),
}));

beforeEach(() => vi.stubGlobal("fetch", vi.fn()));
afterEach(() => vi.unstubAllGlobals());
```

### VSCode Settings

Project-specific settings in `.vscode/settings.json`:
- Disables some SonarLint rules that produce noise
- Ignores unknown @rules in CSS

---

## Directory Structure

```
/home/user/9router
├── src/
│   ├── app/                    # Next.js App Router pages & API routes
│   │   ├── api/               # API endpoints (route.js files)
│   │   └── dashboard/         # Dashboard UI pages
│   ├── sse/                   # SSE handler services
│   │   ├── handlers/          # Request handlers (chat.js, embeddings.js)
│   │   ├── services/          # Auth, model, token refresh services
│   │   └── utils/             # Logger, utilities
│   ├── shared/                # Shared components, hooks, constants
│   ├── mitm/                  # MITM proxy for traffic inspection
│   └── i18n/                  # Internationalization
├── open-sse/                   # Core SSE library
├── cloud/                      # Cloudflare Worker
├── tests/unit/                # Vitest test files (*.test.js)
├── package.json               # Main dependencies
├── eslint.config.mjs          # ESLint configuration
├── next.config.mjs            # Next.js configuration
└── jsconfig.json              # Path aliases
```

---

## Key Dependencies

- **next**: ^16.1.6, **react**: 19.2.4, **tailwindcss**: ^4
- **eslint**: ^9 (eslint-config-next 16.1.6)
- **vitest**: ^4.0.0 (testing), **wrangler**: ^3.0.0 (cloud worker)

---

## Common Patterns

### API Route Handler

```javascript
// src/app/api/example/route.js
const CORS_HEADERS = {
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Methods": "POST, OPTIONS",
  "Access-Control-Allow-Headers": "*"
};

export async function OPTIONS() {
  return new Response(null, { headers: CORS_HEADERS });
}

export async function POST(request) {
  let body;
  try {
    body = await request.json();
  } catch {
    return new Response(JSON.stringify({ error: "Invalid JSON body" }), {
      status: 400,
      headers: { "Content-Type": "application/json", ...CORS_HEADERS }
    });
  }
  return new Response(JSON.stringify({ result: "success" }), {
    headers: { "Content-Type": "application/json", ...CORS_HEADERS }
  });
}
```

---

## NPM Bundle 修改 SOP (緊急修復用)

當需要緊急修復已發布的 NPM 版本時,可以通過修改 bundled JavaScript 來添加新模型。

### 找到 NPM 包的安裝路徑

```bash
npm root -g
# 通常在: /home/user/.global_modules/lib/node_modules/9router
```

### 添加新模型到 Provider 列表

模型列表被嵌入到 webpack chunk 文件中。找到對應的文件:

```bash
cd /home/user/.global_modules/lib/node_modules/9router
ls app/.next/static/chunks/
```

找到包含 provider models 的 chunk (通常是 `4495-*.js` 或類似名稱):

```bash
# 搜索當前模型的字符串
grep -o 'gc:\["gemini-3-flash-preview"[^]]*\]' app/.next/static/chunks/*.js
```

### 修改步驟

1. **讀取 chunk 文件**:
   ```bash
   nano app/.next/static/chunks/4495-xxxxxxxx.js
   ```

2. **找到模型數組** (例如 Gemini CLI 的 gc 數組):
   ```
   gc:[{id:"gemini-3-flash-preview",name:"Gemini 3 Flash Preview"},{id:"gemini-3-pro-preview",name:"Gemini 3 Pro Preview"}]
   ```

3. **添加新模型**:
   ```
   gc:[{id:"gemini-2.5-flash",name:"Gemini 2.5 Flash"},{id:"gemini-2.5-flash-lite",name:"Gemini 2.5 Flash Lite"},{id:"gemini-3-flash-preview",name:"Gemini 3 Flash Preview"},{id:"gemini-3-pro-preview",name:"Gemini 3 Pro Preview"}]
   ```

4. **重啟服務**:
   ```bash
   # 停止並重新啟動 9router
   pkill -f 9router
   9router
   ```

5. **清除瀏覽器緩存**:
   - 按 Ctrl+Shift+R (或 Cmd+Shift+R) 強制刷新

### 注意事項

- 這是**緊急修復方案**,會在下次 npm 升級後失效
- 長期解決方案: 從源碼修改 `open-sse/config/providerModels.js` 並重新 build 發布
- 每次添加新模型都需要重複此過程

---

## 從源碼 Patch 並發布到 NPM

當需要長期修復或添加新功能時,從源碼构建並發布到 NPM。

### 前置準備

1. **安裝 npm CLI** (如尚未安裝):
   ```bash
   npm install -g npm
   ```

2. **登入 npm**:
   ```bash
   npm login
   # 輸入 username, password, email
   ```

3. **確認 package.json 版本**:
   ```bash
   cat package.json | grep '"version"'
   ```

### 修改源碼

1. **修改模型列表**:
   ```bash
   nano open-sse/config/providerModels.js
   ```

2. **找到對應的 provider 數組** (例如 Gemini CLI):
   ```javascript
   gc: [  // Gemini CLI
     { id: "gemini-3-flash-preview", name: "Gemini 3 Flash Preview" },
     { id: "gemini-3-pro-preview", name: "Gemini 3 Pro Preview" },
   ],
   ```

3. **添加新模型**:
   ```javascript
   gc: [
     { id: "gemini-2.5-flash", name: "Gemini 2.5 Flash" },
     { id: "gemini-2.5-flash-lite", name: "Gemini 2.5 Flash Lite" },
     { id: "gemini-3-flash-preview", name: "Gemini 3 Flash Preview" },
     { id: "gemini-3-pro-preview", name: "Gemini 3 Pro Preview" },
   ],
   ```

### 構建並發布

1. **安裝依賴**:
   ```bash
   npm install
   ```

2. **構建**:
   ```bash
   npm run build
   # 或使用 bun: npm run build:bun
   ```

3. **增加版本號** (根據修改類型選擇):
   ```bash
   # Patch 版本 (bug fix): x.y.z -> x.y.z+1
   npm version patch
   
   # Minor 版本 (新功能): x.y.z -> x.y+1.0
   npm version minor
   
   # Major 版本 (破壞性改動): x.y.z -> x+1.0.0
   npm version major
   ```

4. **發布到 npm**:
   ```bash
   npm publish --access public
   ```

### 用戶端更新

用戶可以通過以下方式獲取更新:

```bash
# 更新到最新版本
npm update -g 9router

# 或重新安裝
npm install -g 9router@latest

# 如果使用 npx
npx 9router@latest
```

### 完整示例: 添加 Gemini 2.5 Flash

```bash
# 1. 修改源碼
nano open-sse/config/providerModels.js
# 將 gc 數組修改為包含 gemini-2.5-flash 和 gemini-2.5-flash-lite

# 2. 安裝依賴並構建
npm install
npm run build

# 3. 發布
npm version patch
npm publish --access public

# 4. 用戶更新
npm update -g 9router
```
