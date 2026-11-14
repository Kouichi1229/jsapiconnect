# JavaScript API Connect｜天氣與農務提醒前端串接原型

本 Repository 保存以原生 JavaScript 串接氣象資料與農務提醒 API 的簡易前端原型。

## 功能

- 呼叫氣象開放資料 API，顯示指定地點的天氣資訊。
- 使用不同 JavaScript 版本嘗試顯示目前及多個預報時段的溫度與天氣圖示。
- 讀取歷史管理 API 的栽植期提醒與預警報資料。
- 將 API 回應更新到 HTML DOM。

## 技術

- HTML
- JavaScript
- XMLHttpRequest
- JSON
- DOM API
- 第三方 CORS proxy

## 目前實作界線

- 天氣程式使用固定陣列索引定位地點及預報時段。
- 提醒 API 讀取流程使用 CORS proxy 及歷史 Heroku endpoint，不能假設目前仍可使用。
- 程式沒有完整處理 HTTP 錯誤、資料缺漏或非 JSON 回應。
- 氣象 API 金鑰已在目前主分支的 `api.js` 與 `api_V2.js` 中替換為 `APIKey` 佔位值；Git 歷史未重寫。
- 本次未重新呼叫外部 API。

完整技術回顧請參閱 [PROJECT_RETROSPECTIVE.md](PROJECT_RETROSPECTIVE.md)。
