# 2026 AIA Taipei Design Awards — Call for Entries page

A single, self-contained **static HTML page**. No build step, no framework, no
server-side code. Site chrome (header / navigation / footer) has been removed
deliberately so the page can be dropped inside an existing site template.

單一檔案的**靜態網頁**，不需編譯、不需框架、不需後端。已刻意移除頁首、導覽列與頁尾，
可直接嵌入既有網站模板。

---

## 1. Contents 檔案內容

```
index.html                                          the page 網頁本體
assets/
  poster.jpg                                        the poster shown at the top 頁首海報
downloads/
  2026-AIA-Taipei-AWARDS_Appendix-Forms-A-E.docx    entry forms, linked from the page
README.md                                           this file 本說明
```

That is everything the page needs. Keep `assets/` and `downloads/` next to
`index.html` — both are referenced by relative paths.

以上即為全部所需檔案。`assets/` 與 `downloads/` 需與 `index.html` 同層，
兩者皆以相對路徑引用。

---

## 2. Deploying 上架方式

Copy `index.html` and the `assets/` and `downloads/` folders to the web root, keeping
their relative positions. The download link is relative
(`downloads/2026-AIA-Taipei-AWARDS_Appendix-Forms-A-E.docx`), so the folder
must stay next to the page.

將 `index.html` 與 `assets/`、`downloads/` 資料夾一併複製到網站目錄，**保持相對位置**；
下載連結為相對路徑，資料夾必須與網頁放在同一層。

Serve over HTTPS. Nothing else is required.

### Embedding in a CMS 嵌入 CMS
If you are pasting into an existing template rather than serving the file
as-is, copy **the entire `<style>` block in `<head>`** together with
**everything inside `<body>`**. The two `<link>`/`<script>` tags for fonts
(see §3) should also be carried over, or the page falls back to system fonts.

若要貼進既有模板，請將 `<head>` 內的整段 `<style>` 與 `<body>` 內所有內容一起複製；
字型的 `<link>`／`<script>`（見第 3 節）也建議一併保留，否則會退回系統字型。

---

## 3. Fonts 字型

The page loads **Proxima Nova** from Adobe Typekit — the same typeface and the
same kit used on aiainternational.org — with **Hanken Grotesk** (Google Fonts)
and then Helvetica / Arial as fallbacks.

If the Typekit kit is not licensed for the destination domain, the page still
renders correctly using the fallbacks; only the typeface changes. To use a
different kit, replace the `use.typekit.net` `<script>` tag in `<head>`.

頁面透過 Adobe Typekit 載入 **Proxima Nova**（與 aiainternational.org 同一組 kit），
後備字型為 Hanken Grotesk 與 Helvetica／Arial。若目標網域未取得 Typekit 授權，
頁面仍可正常顯示，只是字型改用後備字型；如需更換，請替換 `<head>` 內的
`use.typekit.net` script 標籤。

---

## 4. The poster 海報

The poster at the top is the **official artwork**, at `assets/poster.jpg`.

It is a web-optimised copy: **1920 x 2718** (A4 proportions, 1:1.414), ~200 KB.
The page displays it at most 960 px wide, so 1920 px covers 2x retina screens
with room to spare. The 600 dpi print master (7016 x 9933) is **not** part of
this package - keep it with the design files.

頁首海報為**正式設計稿**，位於 `assets/poster.jpg`，已針對網頁最佳化：
1920×2718（A4 比例 1:1.414）、約 200 KB。網頁最大顯示寬度 960px，
1920px 足以應付 2 倍解析度螢幕。600dpi 印刷原稿（7016×9933）未收錄於本包。

To replace it, drop a new file at the same path, keeping A4 proportions, and
update the `width` / `height` attributes on the `<img>` in `index.html` to the
new pixel dimensions so the browser reserves the right space while loading.

如需更換，請以相同路徑放入新檔（維持 A4 比例），並將 `index.html` 中該
`<img>` 的 `width` / `height` 屬性改為新的像素尺寸，避免載入時版面跳動。

The full poster wording is duplicated in the image's `alt` text, so screen
readers and search engines still get it.

海報上的完整文案已寫入 `alt` 屬性，螢幕閱讀器與搜尋引擎仍可讀取。

---

## 5. Editing content 修改內容

All copy is plain HTML in `<body>` — no templating. The most likely edits:

| What 項目 | Where to look 位置 |
|---|---|
| Submission deadline 截稿日 | 6 places — the poster text `.p-t5`, the poster's `aria-label`, the red badge `<div class="deadline">`, the Key Dates block `#dates`, and in `#fees` both the final fee phase (`19–31 Oct`) and the milestone row |
| Fees 費用 | the table in `#fees` |
| Contact email 聯絡信箱 | search for `aiataipeiaward@gmail.com` |
| Sponsors 贊助 | `#sponsors` — currently reads "Coming soon" |

**The deadline appears in six places.** If you change it, change all six so the
page stays consistent — including the poster's `aria-label` (screen-reader text)
and the end of the final fee phase, which is bounded by the deadline.

**截稿日共出現於六處**，修改時請一併更新（含海報的 `aria-label` 及最後一段費率的結束日），以免前後不一致。

---

## 6. Browser support 瀏覽器支援

Current Chrome, Edge, Safari and Firefox. Layout is responsive down to phone
widths; the fee table scrolls sideways inside its own box on narrow screens
rather than stretching the page.

The poster uses CSS container queries and `aspect-ratio`, both supported in all
current browsers. In a browser older than ~2023 the poster type may not scale,
but the page remains readable.

---

## 7. Accessibility 無障礙

Headings run in order, the fee table uses proper `<th scope>` and a caption,
the poster carries a text alternative, and colour contrast meets WCAG AA.
Please keep these intact when editing.

---

## 8. The demo notice 展示版提示

The preview build shows a **"this is a demonstration page"** dialog on load,
plus a small bar along the bottom once it is dismissed.

**It disables itself on any real domain.** The script only runs when the
hostname is `*.github.io`, `localhost` or `127.0.0.1`, so once this page is
deployed to the live site the notice never appears — no edit required.

To strip it out completely, delete the two blocks marked `DEMO NOTICE`: the
`<style>` + markup just after `<body>`, and the `<script>` just before
`</body>`. Nothing else depends on them.

展示版在開啟時會彈出「本頁為展示版本」對話框，關閉後底部保留一條提示。

**部署到正式網域時會自動停用** —— 該腳本僅在 `*.github.io`、`localhost`、
`127.0.0.1` 執行，正式站不會出現，無需修改。若要完全移除，刪除標示為
`DEMO NOTICE` 的兩個區塊（`<body>` 後的 `<style>` 與標記、`</body>` 前的
`<script>`）即可，其餘功能不受影響。
