# Hexo Blog 專案說明

這是使用 [Hexo](https://hexo.io/) 建立的個人部落格專案，文章使用 Markdown 撰寫，透過 GitHub Pages 部署靜態網站。


---

## 📁 分支說明

| 分支 | 用途 |
|------|------|
| `main` | Hexo 原始碼（寫作、設定、主題都在這） |
| `gh-branch` | Hexo 部署輸出的靜態網站，GitHub Pages 用這個分支作為網站來源 |

---

## 🧰 常用指令（寫文、預覽、上線）

### 🔹 新增一篇文章
```bash
hexo new post "文章標題"
```

### 🔹 本地預覽（開啟 http://localhost:4000）
```bash
hexo s
```

### 🔹 部署上線
```bash
hexo clean     # 清掉舊的產出
hexo g         # 產出新的靜態網頁
hexo d         # 推送到 gh-branch 分支
```
* 大約2分鐘後，新文章才會更新完(網站有快取)
---

## ⚙️ 設定說明

- `_config.yml`：Hexo 主設定檔
- `themes/xxx/`：佈景主題
- `source/_posts/`：文章 Markdown 檔案放這裡

---

## 📝 注意事項

- Hexo deploy 會根據 `_config.yml` 的設定將靜態頁面推到 `gh-branch` 分支
- 若部署失敗，可檢查 `.deploy_git` 或執行 `hexo clean` 重來
- GitHub Pages 要設定網站來源為 `gh-branch` 分支的 root

---

## 🔄 若太久沒動，請從這開始：
```bash
npm install # 重新裝套件
hexo clean
hexo g
hexo s # 啟動本地伺服器
```

然後看 localhost:4000 預覽網站是否正常～

---

## 🙋 作者

###### Teddy Luo  
INTP｜顯示者｜日柱癸水｜命宮天相

靈感型人格。喜歡思考，卻常常想不透ＸＤ

