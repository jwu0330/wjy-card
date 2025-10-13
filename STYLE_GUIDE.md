# 個人連結頁面 - 樣式設計規範

> **重要提示**：此文件記錄所有設計參數和樣式規範。任何修改前必須先閱讀此文件，確保不破壞現有設計風格。

---

## 📐 設計理念

### 核心原則
- **簡潔至上**：避免過度裝飾，保持乾淨的視覺層次
- **米色系透明風格**：整體使用米色調，透明元素營造輕盈感
- **毛玻璃效果**：所有浮動元素使用 `backdrop-filter: blur(10px)`
- **統一間距**：使用 CSS 變數和 flexbox gap 統一管理

---

## 🎨 色彩系統

### CSS 變數定義
```css
:root {
  --bg: #F5EFE6;                    /* 背景色：米色 */
  --card: rgba(255,255,255,.35);    /* 卡片/按鈕背景：35% 透明白 */
  --card-hover: rgba(255,255,255,.5); /* 懸停背景：50% 透明白 */
  --text: #1F2937;                  /* 主文字色：深灰 */
  --muted: #6B7280;                 /* 次要文字色：中灰 */
  --accent: #C89B65;                /* 強調色：金色 */
  --ring: rgba(200,155,101,.35);    /* 焦點環：35% 透明金 */
  --radius: 18px;                   /* 圓角半徑 */
  --shadow: 0 4px 12px rgba(0,0,0,.06); /* 陰影 */
}
```

### 顏色使用規則
1. **背景色 (`--bg`)**：僅用於 `body` 和 `.sheet`
2. **卡片色 (`--card`)**：所有按鈕、語言切換、面板按鈕
3. **文字色 (`--text`)**：所有主要文字，**禁止使用藍色或其他顏色**
4. **強調色 (`--accent`)**：僅用於 hover 狀態的邊框和陰影

---

## 📏 間距系統

### 容器間距
```css
.container {
  max-width: 680px;           /* 最大寬度固定 */
  padding: 24px 16px 64px;    /* 上 24px，左右 16px，下 64px */
}
```

### 按鈕間距
```css
.links {
  gap: 10px;                  /* 按鈕之間間距：10px */
}

.btn {
  padding: 14px 16px;         /* 內邊距：上下 14px，左右 16px */
}
```

### 圖示間距
```css
.left {
  gap: 12px;                  /* 圖示與文字間距：12px */
}
```

**❌ 禁止事項**：
- 不要在 `.btn` 上使用 `margin`（已用 `gap` 處理）
- 不要修改 `.container` 的 `max-width`

---

## 🔘 按鈕樣式

### 基礎樣式
```css
.btn {
  background: var(--card);           /* 半透明白色 */
  border: 1.5px solid #E5E7EB;       /* 淺灰邊框 */
  border-radius: var(--radius);      /* 18px 圓角 */
  padding: 14px 16px;
  transition: all .2s ease;
}
```

### Hover 效果
```css
.btn:hover {
  border-color: var(--accent);       /* 金色邊框 */
  background: var(--card-hover);     /* 更透明的白色 */
  transform: translateY(-2px);       /* 上移 2px */
  box-shadow: 0 6px 16px rgba(200,155,101,.15); /* 金色陰影 */
}
```

### Active 效果
```css
.btn:active {
  transform: scale(.97);             /* 縮小至 97% */
}
```

**❌ 禁止事項**：
- 不要移除 `backdrop-filter: blur(10px)`
- 不要將背景改為純白色 `#FFF`
- 不要使用其他顏色的邊框（除了 hover 的金色）

---

## 🌐 語言切換

### 設計規格
```css
.lang-switch {
  position: fixed;
  top: 14px;                         /* 電腦版：14px */
  right: 14px;
  background: var(--card);
  border: 1px solid #E5E7EB;
  border-radius: 999px;              /* 完全圓角 */
  font-weight: 500;
  backdrop-filter: blur(10px);
}
```

### 響應式尺寸
- **手機版（≤640px）**：
  - `top: 60px`（避免被狀態列遮擋）
  - `font-size: 13px`
  - `padding: 6px 12px`

- **電腦版（>640px）**：
  - `top: 14px`
  - `font-size: 16px`
  - `padding: 10px 20px`

### 顯示格式
- **固定文字**：`中/EN`
- **功能**：點擊切換中英文內容
- **❌ 禁止**：改為下拉選單或其他形式

---

## 💬 Toast 提示

### 位置與動畫
```css
.toast {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(.9); /* 居中 + 初始縮小 */
  opacity: 0;
}

.toast.show {
  transform: translate(-50%, -50%) scale(1);  /* 放大到正常 */
  opacity: 1;
}
```

### 樣式規格
- **背景**：`var(--text)`（深灰色）
- **文字**：白色
- **圓角**：12px
- **內邊距**：`12px 24px`
- **陰影**：`0 8px 24px rgba(0,0,0,.3)`

**❌ 禁止事項**：
- 不要改為右下角顯示
- 不要使用其他背景顏色

---

## 📱 響應式設計

### 斷點
- **手機/平板**：`@media(max-width:640px)`
- **電腦版**：`@media(min-width:641px)`

### Email 面板
- **電腦版**：居中 Modal
  - `max-width: 420px`
  - `border-radius: 18px`（四周圓角）
  - `margin: 16px`

- **手機版**：底部面板
  - `max-width: 680px`
  - `border-radius: 18px 18px 0 0`（只有上方圓角）
  - `margin: 0`

---

## 🎭 毛玻璃效果

### 必須使用的元素
```css
.btn,
.lang-switch,
.sheet,
.sheet-btn {
  backdrop-filter: blur(10px);       /* 10px 模糊 */
}
```

**❌ 禁止事項**：
- 不要移除任何元素的 `backdrop-filter`
- 不要修改模糊值（固定 10px）

---

## 🔤 字體系統

### 字體堆疊
```css
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, 
             "Noto Sans TC", "PingFang TC", "Microsoft JhengHei", sans-serif;
```

### 字體大小
- **標題 (h1)**：24px
- **副標題 (.subtitle)**：15px
- **按鈕文字**：繼承 body（默認）
- **Footer**：12px（手機版 11px）
- **Toast**：15px
- **語言切換**：16px（電腦版）/ 13px（手機版）

---

## 🎯 圖示規範

### 尺寸
```css
.icon {
  width: 22px;
  height: 22px;
  flex-shrink: 0;               /* 防止壓縮 */
  display: block;
}

.open-arrow {
  width: 18px;
  height: 18px;
  opacity: .6;
}

.sheet-icon {
  width: 20px;
  height: 20px;
  flex-shrink: 0;
}
```

### 圖示風格
- **主按鈕圖示**：填滿式（filled）SVG
- **箭頭圖示**：輪廓式（stroke）SVG
- **面板圖示**：輪廓式（stroke）SVG

**❌ 禁止事項**：
- 不要混用 emoji 和 SVG
- 不要使用不同風格的圖示

---

## 🎨 頭像設計

### 規格
```css
.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;                /* 圓形 */
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); /* 紫藍漸層 */
  font-size: 36px;                   /* emoji 大小 */
  box-shadow: 0 4px 12px rgba(102,126,234,.25);
}
```

### 內容
- **當前**：👨‍💻 emoji
- **可替換**：其他 emoji 或圖片

---

## 🚫 絕對禁止的修改

### 1. 顏色相關
- ❌ 將背景改為純白色
- ❌ 將按鈕背景改為純白色
- ❌ 使用藍色或其他顏色的文字
- ❌ 移除或修改 `--accent` 金色

### 2. 結構相關
- ❌ 在按鈕外層加入卡片容器
- ❌ 將語言切換改為下拉選單
- ❌ 將 Toast 改為右下角顯示

### 3. 效果相關
- ❌ 移除毛玻璃效果 `backdrop-filter`
- ❌ 移除按鈕的 hover 動畫
- ❌ 修改透明度值（35% 和 50%）

### 4. 間距相關
- ❌ 在 `.btn` 上加入 `margin`
- ❌ 修改 `.container` 的 `max-width: 680px`
- ❌ 修改 `.links` 的 `gap: 10px`

---

## ✅ 允許的修改

### 可以修改的內容
1. **文字內容**：標題、副標題、按鈕文字
2. **連結網址**：社交媒體連結
3. **頭像**：更換 emoji 或上傳圖片
4. **新增按鈕**：按照現有樣式新增社交平台

### 新增按鈕範例
```html
<a class="btn" href="YOUR_URL" target="_blank" rel="noopener">
  <div class="left">
    <svg class="icon" viewBox="0 0 24 24" aria-hidden="true">
      <!-- SVG path -->
    </svg>
    <span>平台名稱</span>
  </div>
  <svg class="open-arrow" viewBox="0 0 24 24" aria-hidden="true">
    <path d="M8 5l8 7-8 7" fill="none" stroke="currentColor" stroke-width="2"/>
  </svg>
</a>
```

---

## 📋 檢查清單

在修改前，請確認：
- [ ] 是否保持米色系透明風格？
- [ ] 是否保留所有毛玻璃效果？
- [ ] 文字顏色是否統一為 `var(--text)`？
- [ ] 按鈕是否使用 `gap` 而非 `margin`？
- [ ] Toast 是否居中顯示？
- [ ] 語言切換是否為「中/EN」格式？
- [ ] 響應式設計是否正常運作？

---

## 📞 聯絡資訊

- **作者**：Wu Jiying
- **Email**：jwu1008171@gmail.com
- **最後更新**：2025-10-13

---

**記住：簡潔、透明、米色系是這個設計的靈魂。任何修改都應該遵循這些原則。**
