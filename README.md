# 小確幸金庫 🦁

一個單檔（`index.html`）的靜態帳本網頁，記錄零食、飲料、下午茶、慶生的支出與金主贊助。
辛苦工作之餘，靠這些小確幸補一下電再繼續拚 💪
資料存在瀏覽器 `localStorage`（key：`cheer_fund3`），不需後端、不需資料庫。

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

## 小提醒

- 資料存在「使用該網頁的瀏覽器」裡，換裝置或清除瀏覽器資料會不見
- 若要重置回預設範例資料：開瀏覽器 Console 執行 `localStorage.removeItem('cheer_fund3')` 後重新整理
