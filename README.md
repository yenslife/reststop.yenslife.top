# 狸開火星的休息站（Hugo）

## 開發與預覽

```bash
hugo server -D
```

- `-D` 代表也會顯示 `draft: true` 的文章。

## 文章 Front Matter 寫法（重點：`categories` = 主題）

本網站用 Hugo 的 `categories` 當作「主題」來分類文章；網站導覽的「主題」會連到：

- `/categories/`（主題總覽）

### 最小範本（YAML）

```yaml
---
title: "文章標題"
date: 2025-12-14T10:00:00+08:00
draft: false
categories: ["溫馨友情"]
---
```

### 建議範本（YAML）

```yaml
---
title: "森林深處的微光"
date: 2025-12-13T10:00:00+08:00
draft: false
author: "海狸大師"
description: "一個關於迷失與尋找，以及森林中微小希望的故事。"
categories: ["奇幻冒險", "療癒"]
image: "images/cover.jpg"
---
```

- `title`
  - 文章標題
- `date`
  - 發佈時間（建議含時區 `+08:00`）
- `draft`
  - `true`：草稿
  - `false`：正式文章
- `categories`
  - 文章主題（建議 1-2 個，最多 3 個，避免主題失焦）
- `description`
  - 會用在 SEO 的 `meta description`、分享預覽（Open Graph / Twitter）
- `author`
  - 會顯示在文章頁（目前主題會讀 `.Params.Author`）
- `image`
  - 文章分享預覽圖（Open Graph / Twitter 會優先用它）
  - 建議寫法：用「網站根目錄路徑」或「完整網址」
    - 範例（建議）：`/images/cover.jpg`
    - 範例（也可）：`https://example.com/images/cover.jpg`
  - 圖片檔案放哪裡
    - 放在 `static/images/cover.jpg`，產出後會對應到 `/images/cover.jpg`
  - 也可以放在「文章資料夾」底下（Page Bundle，推薦好管理）
    - 文章路徑長這樣：`content/posts/my-story/index.md`
    - 圖片跟文章放同一層：`content/posts/my-story/cover.jpg`
    - front matter 這樣寫：`image: "cover.jpg"`
    - 這種寫法會把 `cover.jpg` 當作該頁的 Page Resource，Open Graph / Twitter 會自動抓到正確網址
  - 注意：如果文章是單檔（例如 `content/posts/starry-promise.md`），它不是 page bundle，通常就不會有 `.Resources`；
    這種情況建議用 `/images/...`（放在 `static/`）或把文章改成資料夾形式（`content/posts/starry-promise/index.md`）再把圖片放進去。

## 摘要（Summary）控制方式

首頁/列表頁會顯示 `.Summary`。

如果你想手動控制摘要切點，可以在文章內容中加入：

```markdown
<!--more-->
```

`<!--more-->` 之前的內容會當作摘要。

## SEO / 分享預覽設定

目前主題已在 `<head>` 自動輸出：

- `meta description`
- `canonical`
- Open Graph（`og:*`）
- Twitter Card（`twitter:*`）
- RSS link

### 圖片與 Open Graph / Twitter 預覽圖規則

分享預覽圖（例如貼到 LINE/FB/Discord 看到的那張大圖）會依序取用：

1. 文章 front matter 的 `image`
2. `hugo.toml` 的 `[params].ogImage`
3. 都沒設定就不輸出 `og:image` / `twitter:image`

`image` 支援三種寫法：

- 完整網址：`https://.../cover.jpg`
- 站台根目錄路徑：`/images/cover.jpg`（搭配 `static/images/cover.jpg`）
- Page Bundle 相對路徑：`cover.jpg`（圖片放在 `content/posts/xxx/cover.jpg` 且該文章為 `index.md`）

建議準備一張「全站預設」+ 重要文章再各自指定。

尺寸建議：

- Open Graph 常見建議：`1200 x 630`
- 檔案格式：`jpg` / `png` 都可

### 全站預設分享圖（可選）

你可以在 `hugo.toml` 設定預設分享圖，沒有填 `image` 的文章就會用它：

```toml
[params]
  description = "..."
  ogImage = "/images/beaver-master-story.png"
```

文章指定（覆蓋全站預設）：

```yaml
---
title: "星空下的約定"
date: 2025-11-20T19:30:00+08:00
draft: false
categories: ["溫馨友情"]
description: "兩個朋友在星空下許下一個永恆的約定。"
image: "/images/starry-promise.jpg"
---
```

## 常見主題（建議）

主題（`categories`）建議先控制在 6-12 個，例：

- 溫馨友情
- 親子
- 睡前故事
- 奇幻冒險
- 成長
- 療癒
- 生活心情
