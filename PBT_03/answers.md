# PBT_03 - CSS Core - Answers

## PHẦN A — KIỂM TRA ĐỌC HIỂU (25 điểm)

---

## Câu A1 (5đ) — 3 Cách nhúng CSS

### 1. Inline CSS
```html
<h1 style="color: red; font-size: 24px;">Tiêu đề</h1>
```
- Độ ưu tiên cao nhất, khó bảo trì

### 2. Internal CSS
```html
<style>
    h1 { color: red; font-size: 24px; }
</style>
```
- CSS trong thẻ `<style>` của HTML, áp dụng 1 trang

### 3. External CSS (BEST PRACTICE)
```html
<link rel="stylesheet" href="style.css">
```
- File CSS riêng, tái sử dụng nhiều trang

**Nếu cả 3 cách trong 1 element → INLINE CSS thắng (specificity cao nhất)**

---

## Câu A2 (8đ) — CSS Selectors

| # | Selector | Chọn |
|---|----------|------|
| 1 | `h1` | ShopTLU |
| 2 | `.price` | Cả 2 span.price |
| 3 | `#app header` | KHÔNG (không có <header>) |
| 4 | `nav a:first-child` | Home |
| 5 | `.product.featured h2` | iPhone 16 |
| 6 | `article > p` | Cả 2 <p> |
| 7 | `a[href="/"]` | Home |
| 8 | `.top-bar.dark h1` | ShopTLU |

---

## Câu A3 (7đ) — Box Model

### content-box (mặc định):
- width: 400px, padding: 20px, border: 5px
- **Hiển thị = 400 + 40 + 10 = 450px**

### border-box:
- width: 400px (bao gồm padding + border)
- **Hiển thị = 400px**
- Content thực = 400 - 40 - 10 = 350px

### Margin Collapse (dọc):
- margin-bottom: 25px + margin-top: 40px
- **Khoảng cách = 40px (max, không cộng)**

---

## Câu A4 (5đ) — Specificity

| Selector | Specificity | Ưu tiên |
|----------|-------------|---------|
| `p` | (0,0,1) | Thấp |
| `.price` | (0,1,0) | Cao hơn |
| `#main-price` | (1,0,0) | Cao nhất |
| `p.price` | (0,1,1) | Trung bình |

**Thứ tự từ cao → thấp:** `!important` > Inline > ID > Class > Element > Inherited

---

# PHẦN B — THỰC HÀNH CODE (55 điểm)

---

## Bài B1 (20đ) — Style Trang Profile

**Yêu cầu:**
- `* { box-sizing: border-box; }`
- Header gradient + navigation hover/active
- Table: border-collapse, zebra striping, hover
- Footer: dark bg, center align
- 5+ loại selector

**Selectors:** Universal, Element, Class, Pseudo-class, Descendant

**Files:** `profile.html`, `style.css`

---

## Bài B2 (20đ) — Box Model Lab

**Part 1: content-box vs border-box**
- width: 300px, padding: 20px, border: 5px
- content-box: 300 + 40 + 10 = **350px**
- border-box: **300px** (đã include)

**Part 2: 3-column layout (1000px)**
- KHÔNG border-box: 250+542+282 = **1106px** (wrap)
- Dùng border-box: 250+500+250 = **1000px** (OK)

**Files:** `boxmodel_lab.html`, `boxmodel.css`

---

## Bài B3 (15đ) — Specificity Battle

| Rule | Specificity | Color |
|------|-------------|-------|
| `span` | (0,0,1) | Black |
| `span:first-of-type` | (0,1,1) | Blue |
| `.text` | (0,1,0) | Green |
| `.colored` | (0,1,0) | Purple |
| `.text.colored` | (0,2,0) | Orange |
| `span.special-text` | (0,1,1) | Deep Pink |
| `.special-text.active` | (0,2,0) | Turquoise |
| `div span.text` | (0,1,2) | Tomato |
| `#main-text` | **(1,0,0)** | **Dodger Blue (WINNER)** |
| `span[id="main-text"]` | (0,1,1) | Forest Green |

**Đáp án:** **#1e90ff (Dodger Blue)** - ID selector thắng

**Files:** `specificity.html`, `specificity.css`

---

# PHẦN C — DEBUG & SUY LUẬN (20 điểm)

---

## Câu C1 (10đ) — Debug CSS Layout

**Vấn đề:** 3-column (sidebar 300px + content 660px = 960px) layout bị vỡ

**Nguyên nhân:** content-box mặc định
- Sidebar: 300 + 40 (padding) + 2 (border) = 342px
- Content: 660 + 60 + 2 = 722px
- **Tổng: 1064px > 960px → wrap**

**Sửa:** Thêm `box-sizing: border-box`
- Width đã include padding + border
- Tổng: 300 + 660 = 960px ✅

**File:** `debug_layout.html`

---

## Câu C2 (10đ) — Cascade & Inheritance

| Element | Property | Đáp án | Vì sao |
|---------|----------|--------|--------|
| h2.title (#featured) | font-size | 20px | `.card .title` |
| h2.title (#featured) | color | red | `#featured .title` (ID > class) |
| p (mô tả A) | color | blue | inherit từ `.card` |
| h2.title (card B) | font-size | 20px | `.card .title` |
| h2.title (card B) | color | blue | `.card` (không #featured) |
| p.highlight | color | green | `.highlight !important` |

**Files:** `cascade_puzzle.html`


