# 真佛宗法會報導製作指南

本專案用於將西雅圖雷藏寺每週法會的直播影片，轉換為結構化的報導文章（`.docx` 格式）。

## 工作流程總覽

```
YouTube 直播影片 → MP3 音檔 → 裁切加速 → 語音轉錄 → 逐字稿 → Claude Code 產生報導
```

---

## Step 1：取得法會直播影片連結

前往西雅圖雷藏寺 YouTube 頻道：

https://www.youtube.com/@tbsseattleorg-pu6rn

找到目標日期的法會直播影片，複製影片連結。

> **注意**：直播結束後，YouTube 需要約 1～3 小時處理影片，在這段期間嘗試下載會出現錯誤，這是正常現象，等待處理完成即可。

## Step 2：下載 MP3 音檔

使用 **4K YouTube to MP3** 工具下載音檔：

1. 開啟 4K YouTube to MP3
2. 貼上影片連結
3. 選擇 MP3 格式下載

> 如果出現無法下載的錯誤，代表 YouTube 尚未處理完直播影片，請稍後再試。

## Step 3：裁切與加速音檔

使用 **Audacity** 進行音檔處理，目的是配合轉錄工具免費版的限制（每天 3 個檔案，單檔最長 25 分鐘）。

### 操作步驟

1. 開啟 Audacity，匯入下載的 MP3 檔案
2. 將音檔裁切為三段：
   - **迴向**：法會開頭的迴向部分
   - **main1**：開示與問答的前半段
   - **main2**：開示與問答的後半段（含楞嚴經講授）
3. 對每段音檔進行 **1.75 倍加速**（音軌右上「...圖示」->音高和速度->片段速度->調整為175後按Emter）
4. 分別匯出為 MP3 檔案(點選要會出的音軌->左上「檔案>匯出聲音」->匯出區段選「目前選擇」)

> 裁切的分段點可以彈性調整，重點是確保每段加速後不超過 25 分鐘。

## Step 4：語音轉錄為逐字稿

使用 TurboScribe 線上工具進行語音轉錄：

https://turboscribe.ai/zh-TW/

1. 上傳三段 MP3 檔案（免費版每天限 3 個檔案）
2. 等待轉錄完成
3. 將三段轉錄結果合併，存為 `{YYYYMMDD}逐字.txt`
4. 將逐字稿放入專案目錄下的 `{YYYYMMDD}/` 資料夾

> 逐字稿是語音辨識的原始輸出，會包含大量錯字，尤其是佛教術語和人名，這些會在下一步由 Claude Code 修正。

## Step 5：使用 Claude Code 產生報導

在本專案目錄下開啟 Claude Code，輸入指令：

```
/dharma-report
```

Claude Code 會自動觸發 `dharma-report` skill，執行以下工作：

1. 讀取逐字稿
2. 參考既有報導格式
3. 修正語音辨識錯誤（佛教術語、人名等）
4. 整理為結構化的報導文章
5. 產生格式化的 `.docx` 檔案
6. 重新命名資料夾

### 產出後的人工校對

Claude Code 產出的報導仍需人工校對，重點檢查：

- **迴向文用詞**是否正確
- **楞嚴經原文**是否與經典一致
- **人名、地名、專有名詞**是否正確
- **笑話選取**是否合適（最多 3 則）
- **不確定的內容**是否應移除

---

## 專案目錄結構

```
法會報導/
├── README.md                          ← 本文件
├── {YYYYMMDD}-{報導標題}/
│   ├── {YYYYMMDD}逐字.txt            ← 語音轉錄的逐字稿
│   └── {YYYYMMDD}-{報導標題}.docx     ← 完成的報導文章
├── .claude/
│   └── skills/
│       └── dharma-report/             ← Claude Code skill
│           ├── SKILL.md
│           └── references/
│               └── terminology.md     ← 術語修正對照表
└── ...
```

## 使用的工具

| 工具 | 用途 | 取得方式 |
|------|------|---------|
| 4K YouTube to MP3 | 下載 YouTube 影片音檔 | https://www.4kdownload.com/zh-tw/products/youtubetomp3-1 |
| Audacity | 音檔裁切與加速 | https://www.audacityteam.org/ |
| TurboScribe | 語音轉錄為文字 | https://turboscribe.ai/zh-TW/ |
| Claude Code | 逐字稿整理與報導產生 | https://claude.ai/download |
