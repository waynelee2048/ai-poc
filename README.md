# AI-POC: PostMessage Test Page for Addon AI Analysis

一個輕量級的測試工具頁面，用於測試與除錯 AI Analysis Addon 的 PostMessage 通訊協定。此頁面可作為 iframe 嵌入父應用程式中，透過 `window.postMessage()` 進行雙向通訊。

## 功能

- **REQUEST_CONFIG** - 請求 Addon 設定資料
- **REQUEST_AI_ANALYSES** - 取得目前 AI 分析結果
- **ENABLE/DISABLE Pipeline** - 啟用或停用 batch / realtime pipeline
  - `batch` - 課後逐字稿
  - `realtime` - 即時字幕
- **SET_AI_ANALYSIS_PARAMS** - 設定多個 AI 角色參數（JSON 格式）
- **SUBSCRIBE_AI_ANALYSES** - 訂閱 AI 分析推播通知
- **SUBSCRIBE_TRANSCRIPT** - 訂閱即時逐字稿更新

## 快速開始

### 直接開啟

```bash
open index.html
```

## PostMessage 通訊協定

### 送出訊息格式

```json
{
  "type": "MESSAGE_TYPE",
  "requestId": "req-1",
  "payload": {}
}
```

### 支援的訊息類型

| 送出 (Send) | 回應 (Response) |
|---|---|
| `REQUEST_CONFIG` | `RESPONSE_CONFIG` |
| `REQUEST_AI_ANALYSES` | `RESPONSE_AI_ANALYSES` |
| `ENABLE_BATCH_PIPELINE` | `RESPONSE_ENABLE_BATCH_PIPELINE` |
| `SET_AI_ANALYSIS_PARAMS` | `RESPONSE_SET_AI_ANALYSIS_PARAMS` |
| `SUBSCRIBE_AI_ANALYSES` | `RESPONSE_SUBSCRIBE_AI_ANALYSES` |
| `SUBSCRIBE_TRANSCRIPT` | `RESPONSE_SUBSCRIBE_TRANSCRIPT` |

### 推播訊息

| 類型 | 說明 |
|---|---|
| `PUSH_AI_ANALYSES` | AI 分析結果推播 |
| `PUSH_TRANSCRIPT` | 即時逐字稿推播 |
| `ERROR` | 錯誤訊息 |

## 頁面初始化流程

頁面載入後會自動依序執行：

1. 請求 Addon 設定 (`REQUEST_CONFIG`)
2. 啟用 Batch Pipeline (`ENABLE_BATCH_PIPELINE`)
3. 請求 AI 分析結果 (`REQUEST_AI_ANALYSES`)
4. 訂閱 AI 分析推播 (`SUBSCRIBE_AI_ANALYSES`)
5. 訂閱逐字稿推播 (`SUBSCRIBE_TRANSCRIPT`)

## 技術

- 純 HTML / CSS / JavaScript，無外部依賴
- PostMessage API 跨視窗通訊
- 深色主題 UI
