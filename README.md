# 我的排班月曆：Firebase 同步版

## 1. 建立 Firebase 專案
前往 https://console.firebase.google.com/ → 建立專案 → 註冊 Web 應用程式（`</>`）。不必啟用 Firebase Hosting。

## 2. 啟用 Google 登入
Firebase 控制台 → Authentication → Sign-in method → Google → 啟用，設定支援電子郵件。
在 Authentication → Settings → Authorized domains 加入 `你的帳號.github.io`（不含 https 或路徑）。本機 `localhost` 若要測試，也需列為授權網域。

## 3. 建立 Cloud Firestore
Firebase 控制台 → Firestore Database → Create database → 選擇適當區域 → Production mode。
在 Firestore → Rules 將 `firestore.rules` 內容完整貼上，按 Publish。不要使用測試模式的公開規則。

## 4. 填入設定
Firebase 控制台 → 專案設定（齒輪）→ 你的應用程式 → SDK 設定和配置 → Config。
將 `firebase-config.js` 的 6 個欄位替換成你的專案值。這些值屬公開 Web 設定，不是服務帳戶私鑰；保護資料靠 Firestore Rules。

## 5. 上傳 GitHub Pages
將 `index.html` 與 `firebase-config.js` 放到 GitHub repository 根目錄。
Settings → Pages → Deploy from a branch → main / (root)。
等待部署，開啟 `https://你的帳號.github.io/你的repo/`，用 Google 登入。
**不要**將管理員金鑰、服務帳戶 JSON 或 Google 密碼放進 GitHub。

## 6. 舊資料轉移
在原本存有 localStorage 排班的同一個瀏覽器、同一個網站網址開啟新版；登入後會出現「將舊排班匯入雲端」。若改了 GitHub Pages 網址，原 localStorage 不會自動讀到；請先從舊版匯出 JSON，再在新版登入後匯入。

## 注意
- 登入只請求基本 Google 身分資料，不讀取 Google Calendar、Gmail 或 Drive。
- 此版本的雲端同步需網路；不保證離線編輯。
- 排班統計按每班 9 小時時間跨度，未扣除休息時間。
- 先在私人裝置登入測試；公司公用電腦使用完記得登出 Google 和 APP。
- Firebase Spark 免費額度通常足夠個人使用，但需遵守 Firebase 的實際方案與額度。
