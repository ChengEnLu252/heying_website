# 鶴英新北芭蕾舞團 官方網站

**He Ying New Taipei Ballet — Official Website**

鶴英新北芭蕾舞團是位於新北市板橋區的古典芭蕾舞團與舞蹈教室，開設幼兒律動、兒童芭蕾、成人芭蕾、硬鞋課與一對一訓練，並提供表演服裝租借。

🌐 **網站：** [www.heying.com.tw](https://www.heying.com.tw)（Netlify 站點名稱：`heying`，備用網址 https://heying.netlify.app）

---

## 網站內容

單頁式網站，區塊依序為：

| 區塊 | 錨點 | 說明 |
|---|---|---|
| 關於鶴英 | `#about` | 舞團介紹 |
| 演出紀錄 | `#perf` | 歷年演出卡片、演出影片 |
| 專業師資 | `#teach` | 陳濰翎、李宛蓉老師 |
| 課程介紹 | `#courses` | 兒童課程／成人課程／1對1課程三個分頁 |
| 服裝租借 | `#costume` | 芭蕾 Tutu、芭蕾長紗、男生服裝三類，資料寫在 JS 的 `costumeSets` |
| 照片集錦 | `#gallery` | 演出花絮／課堂風景／活動花絮／比賽花絮，資料寫在 JS 的 `galPhotos` |
| 學員好評 | `#rev` | 好評輪播 |
| 常見問題 | `#faq` | 手風琴展開收合 |
| 教室位置 | `#location` | 兩處教室地址、交通方式、Google 地圖 |
| 聯絡我們 | `#contact` | 電話、LINE、Facebook、Instagram |

## 上課地點

| 教室 | 地址 | 在此上課的課程 |
|---|---|---|
| 文化路教室（主教室） | 新北市板橋區文化路一段182號4樓 | 除下列以外的所有課程 |
| 漢生東路教室（另址） | 新北市板橋區漢生東路43巷30號（[Google 地圖](https://maps.app.goo.gl/RH5ibW3FSwzCo1q76)） | 幼兒律動（週二、週五）、成人纖體芭蕾週二晚班 19:30~21:00 |

在漢生東路上課的課程，課程卡片上會有「另址上課」小卡。課程分頁下方有一行地點提醒，教室位置區塊也有一張漢生東路教室的卡片。以後調整課程或地點時，這三個地方要一起改。

## 網站功能

- 響應式設計（RWD），支援桌機與手機
- 日夜模式切換，會記住訪客上次的選擇（`localStorage` 的 `heying-theme`）
- 中英文雙語切換：每個文字元素都用 `data-zh`、`data-en` 屬性存兩種語言，修改文字時兩個屬性和元素本身的內容都要改
- 頁面載入動畫、滾動漸現動畫、數字計數動畫
- 照片集錦分類篩選、「查看更多照片」、精選照片置頂，以及可播放影片的 Lightbox
- 服裝租借卡片與多圖瀏覽
- SEO：結構化資料（JSON-LD）、Open Graph、`sitemap.xml`、`robots.txt`、Google Search Console 驗證
- LINE 預約按鈕

## 資料夾結構

```
/
├── index.html      # 網站主檔案（HTML、CSS、JS 都在這一個檔案裡）
├── robots.txt
├── sitemap.xml
├── favicon.ico
├── README.md
├── images/         # 第一批素材：logo、師資照、課程照、演出紀錄與課堂影片、
│                   #   stage-*/class-*/event-* 編號照片
└── images2/        # 第二批素材
    ├── 比賽花絮/    # 照片集錦「比賽花絮」
    ├── 演出花絮/    # 照片集錦「演出花絮」
    ├── 課堂風景/    # 照片集錦「課堂風景」
    ├── 活動花絮/    # 照片集錦「活動花絮」
    ├── 服裝/        # 服裝租借照片，檔名對應服裝編號（A01.jpg、A03-2.jpg…）
    └── 地圖-web.jpg 等  # 教室入口實景圖、其他區塊用圖
```

### 新增照片到照片集錦

1. 把照片放進 `images2/` 底下對應的分類資料夾。建議長邊縮到 1600px 左右，單張控制在 1MB 內。
2. 在 `index.html` 的 `galPhotos` 陣列加一行，例如：
   `{src:'images2/比賽花絮/檔名.jpg',cat:'competition'},`
   分類代碼：`stage` 演出花絮、`class` 課堂風景、`event` 活動花絮、`competition` 比賽花絮。加上 `featured:true` 會置頂並標示「精選」。

## 部署方式

網站部署在 [Netlify](https://www.netlify.com/)，站點名稱 `heying`。這個站點**沒有**連結 GitHub，推上 GitHub 不會自動更新網站，改完要另外部署。

部署方式擇一：

- **拖曳上傳**：Netlify 後台 → `heying` → Deploys，把網站資料夾拖進去。上傳前先把不屬於網站的檔案（原始照片、草稿等）移出資料夾，否則它們也會變成公開網址。
- **Netlify CLI**：
  ```bash
  npx netlify-cli login
  npx netlify-cli deploy --dir=. --site=heying          # 先產生預覽網址確認
  npx netlify-cli deploy --dir=. --site=heying --prod   # 確認後再上正式網站
  ```

上線後如果要退回，到 Netlify 後台 Deploys 頁面選擇舊版本，按「Publish deploy」即可。

**請記得每次修改都推上 GitHub。** 2026 年 11 月曾經發生 GitHub 上只有舊版 `index.html`、照片也沒推上去的情況，最後是從線上網站下載回來重建的。

## 技術

- 純 HTML / CSS / JavaScript，無框架、不需要建置步驟
- Google Fonts：LXGW WenKai TC、Noto Serif TC、Caveat
- CSS 自訂屬性實現日夜主題
- IntersectionObserver 實現滾動動畫

## 聯絡資訊

- 📞 電話：02-2969-9257
- 💬 LINE：[點擊加入好友](https://lin.ee/Y4DDKji)
- 📘 Facebook：[鶴英新北芭蕾舞團](https://www.facebook.com/heyingballet/)
- 📷 Instagram：[@heyingballet](https://www.instagram.com/heyingballet/)

---

© 鶴英新北芭蕾舞團 He Ying New Taipei Ballet
