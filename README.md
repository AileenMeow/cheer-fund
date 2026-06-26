# 小確幸金庫 🦁

一個單檔（`index.html`）的靜態帳本網頁，記錄零食、飲料、下午茶的支出與金主贊助。
辛苦工作之餘，靠這些小確幸補一下電再繼續拚 💪
預設用瀏覽器 `localStorage`（key：`cheer_fund3`）存資料；填入 JSONBin 金鑰後，會改用雲端共用資料，多人看到同一份。

## 功能

- **密碼保護**：進站需輸入密碼，通過後存在 `sessionStorage`，同分頁不重複問
- **明細**：分類篩選、支出／贊助一目了然，可編輯與刪除
- **記一筆**：支出 / 金主贊助切換，含品項、金額、類別、日期、備註
- **統計**：贊助總額／總支出／結餘三格卡、各分類支出長條圖、最近五筆
- 全站手繪 SVG icon，無 emoji、無外部 icon library

## 部署到 GitHub Pages

1. 把整個資料夾（包含 `index.html`、`.nojekyll`、`README.md`）push 到 GitHub repo 的 `main` 分支：

   ```bash
   git init
   git add .
   git commit -m "建立小確幸金庫"
   git branch -M main
   git remote add origin https://github.com/[username]/cheer-fund.git
   git push -u origin main
   ```

2. 到 GitHub repo 的 **Settings → Pages**
3. **Source** 選 `Deploy from a branch`
4. **Branch** 選 `main`，資料夾選 `/ (root)`，按 **Save**
5. 等待約 1 分鐘，取得網址：

   ```
   https://[username].github.io/cheer-fund/
   ```

> `.nojekyll` 是空檔案，用來告訴 GitHub Pages 不要用 Jekyll 處理，純靜態直出。

## 多人共用同一份資料（JSONBin 雲端同步）

預設情況下，資料只存在「各自的瀏覽器」裡，所以每個人看到的數字會不一樣。
要讓大家看到同一份，接上免費的 [JSONBin](https://jsonbin.io)：

1. 到 [jsonbin.io](https://jsonbin.io) 註冊登入
2. 建一個 **Bin**：內容先填一個空陣列 `[]`，建立後在網址或詳情頁複製 **Bin ID**（一串英數）
3. 左側 **API Keys → Access Keys** 建一把 Access Key：
   - 權限只勾 **Read** 與 **Update**（不用 Create/Delete）
   - 範圍可限定只給這個 bin（Allowed Bins 填上面的 Bin ID）
   - 複製這把 **Access Key**
4. 打開 `index.html`，找到這兩行填進去：

   ```js
   const JSONBIN_ID  = '';   // ← 貼上 Bin ID
   const JSONBIN_KEY = '';   // ← 貼上 Access Key
   ```

5. commit、push，等 Pages 更新

> **第一次設定後，請「有正確資料的人」先開一次 App**：因為 bin 內容是空的 `[]`，
> App 偵測到雲端是空的，會把這台瀏覽器目前的資料上傳當作初始內容。
> 之後其他人再打開，就會讀到同一份雲端資料。

運作方式：開啟時、切回頁面時、每 25 秒會自動向雲端抓最新；新增／修改／刪除時會合併後寫回，
盡量避免蓋掉別人剛輸入的資料。沒填金鑰時則維持純本機（localStorage）模式。

> ⚠️ 因為是純前端，Access Key 會出現在網頁原始碼裡。請只給「單一 bin、Read+Update」的最小權限，
> 不要用 Master Key。這對「密碼保護的小型私人帳本」來說足夠，但別放機密資料。

## 小提醒

- 純本機模式下，資料存在「使用該網頁的瀏覽器」裡，換裝置或清除瀏覽器資料會不見
- 若要重置回預設範例資料：開瀏覽器 Console 執行 `localStorage.removeItem('cheer_fund3')` 後重新整理
