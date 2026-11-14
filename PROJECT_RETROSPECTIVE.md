# JavaScript API Connect：技術經歷回顧

> 本文件依據靜態 HTML、JavaScript API client 及歷史程式碼整理，未重新呼叫外部 API。

## 1. 專案定位

此 Repository 是一個小型前端 API 串接原型，將氣象資料、栽植期提醒及預警報資訊放入簡單網頁。程式以原生 JavaScript 和 XMLHttpRequest 直接發送 HTTP GET，解析 JSON 後更新 DOM。

## 2. 氣象 API client

主要檔案：`api.js`、`api_V2.js`

- 使用 XMLHttpRequest 發送 GET 請求至氣象開放資料 API。
- 解析 JSON 中的地點與天氣要素資料。
- 讀取指定地點的溫度及天氣現象。
- 依溫度、天氣代碼切換圖片。
- V2 版本嘗試顯示多個預報時段，將溫度與天氣圖示更新至多組 DOM 元素。

程式使用固定陣列索引取得地點及 weatherElement，對 API 回傳排序、資料缺漏及欄位變更缺少防護。

## 3. 農務提醒 API client

主要檔案：`plantApi.js`、`alerApi.js`

- `plantApi.js` 呼叫歷史管理 API 的 `/users` endpoint，讀取最後一筆資料中的溫度與雨量提醒。
- `alerApi.js` 呼叫歷史管理 API 的 `/rooms` endpoint，讀取最後一筆警報文字。
- 透過 JavaScript DOM API 將資料更新到頁面。

兩者透過第三方 cors-anywhere proxy 轉送請求，且將 API 回應的內容直接寫入 `innerHTML`。若資料來源未受信任，需考慮 HTML injection 風險。

## 4. 技術能力摘要

| 技術 | 程式證據 | 合理定位 |
|---|---|---|
| JavaScript | 函式、事件及條件判斷 | 有原生 JavaScript 實作經驗 |
| XMLHttpRequest | GET 請求及 onreadystatechange／onload | 有非同步 API 串接經驗 |
| JSON | 解析天氣與提醒 API 回應 | 有 JSON 資料處理經驗 |
| DOM API | 更新文字與圖片 | 有前端動態內容更新經驗 |
| HTML | 天氣與提醒顯示欄位 | 有簡易網頁展示經驗 |

## 5. 已知限制

- 固定陣列索引依賴特定 API 回應順序。
- API 請求缺少完整 status code、timeout、錯誤回應及缺漏資料處理。
- CORS proxy 為外部服務依賴，不是可控的正式 API gateway。
- 提醒 API 使用歷史 Heroku URL，未確認目前是否仍在線。
- 以 `innerHTML` 顯示 API 回應，未見輸入清理或 HTML sanitization。
- 目前主分支的氣象 API 金鑰已替換為佔位值；Git 歷史未重寫，舊 commit 仍可能保留原始金鑰。

## 6. 履歷描述建議

使用原生 JavaScript 與 XMLHttpRequest 串接氣象開放資料及農務提醒 API，解析 JSON 回應，依地點與預報時段更新網頁中的天氣資訊、圖示、栽植提醒及預警報內容。

## 7. 驗證界線

- 未重新呼叫氣象 API 或歷史管理 API。
- 未確認 CORS proxy 與 Heroku endpoint 目前狀態。
- 未重新測試各 API 回應與 HTML DOM 的相容性。
- 本文件描述程式碼可辨識的 API 串接流程，不代表舊服務目前仍可用。
