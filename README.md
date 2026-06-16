# 多益核心單字高效學習系統

一個純前端（HTML/CSS/JS）的多益（TOEIC）單字互動學習網頁，包含：

- 📇 單字閃卡模式（可翻面看中文解釋、例句、提示，並支援英文發音）
- 📝 隨機小考模式（單字填空選擇題，含計分與整句翻譯解析）

## 線上使用

推送到 GitHub 後，到 repo 的 **Settings → Pages**，
Source 選擇 `main` 分支 / `/ (root)`，存檔後幾分鐘內即可透過
`https://<你的帳號>.github.io/<repo名稱>/` 開啟使用。

## 如何新增之後的 Day（例如 Day 3、Day 4...）

打開 `index.html`，找到 `<script>` 區塊裡的 `const dataSet = { ... }`，
依照已有的 Day 1 / Day 2 格式，在最後面加上新的一組即可，**不需要修改任何 HTML 結構**，
畫面上方「學習進度」的按鈕會自動產生對應的 Day 按鈕。

```js
3: {
    title: "Day 3 ...",
    vocabulary: [
        { word: "單字 (詞性)", zh: "中文解釋", eg: "英文例句", trans: "例句翻譯", hint: "提示句" },
        // ...繼續加
    ],
    quiz: [
        { q: "含空格的題目句子 _______.", options: ["選項1", "選項2", "選項3", "選項4"], ans: "正確答案", trans: "整句翻譯" },
        // ...繼續加
    ]
},
```

加完後存檔、`git add` / `git commit` / `git push` 上去即可，網頁會自動更新。

## 本次優化內容

- 修正小考比對答案時用 `includes()` 子字串比對可能誤判的問題，改為用 `data-option` 屬性精準比對
- 答對題數改用獨立計數器 `correctCount`，不再依賴 `score / 10`（避免日後改變每題分數時跑出錯誤統計）
- 「學習進度」Day 按鈕改為依資料動態產生，之後新增 Day 不需要再手動加 HTML 按鈕
- 語音播放加上 `speechSynthesis.cancel()`，避免連續快速點擊發音鍵時聲音疊在一起
- 補上 `<meta name="description">`，對 GitHub Pages 的 SEO 略有幫助
