# PBT_04 - CSS Layout
## PHẦN A — KIỂM TRA ĐỌC HIỂU (20 điểm)

---

## Câu A1 (10đ) — 5 Loại Positioning

### Bảng Tóm Tắt 5 Loại Positioning

| Position | Chiếm chỗ trong flow? | Tham chiếu vị trí | Cuộn theo trang? | Use case |
|----------|----------------------|------------------|------------------|----------|
| `static` | ✅ Có | Normal flow position | ✅ Có | Vị trí mặc định, normal document flow |
| `relative` | ✅ Có | Tương đối so với vị trí normal của nó | ✅ Có | Điều chỉnh vị trí nhỏ mà không loại bỏ khỏi flow |
| `absolute` | ❌ Không | Nearest positioned ancestor (hoặc body nếu không có) | ❌ Không | Overlays, modals, tooltips, popups |
| `fixed` | ❌ Không | Viewport (cửa sổ trình duyệt) | ❌ Không | Fixed headers, footers, sticky navigation |
| `sticky` | ✅ Có (ban đầu) | Mix of relative & fixed (relative đến positioned ancestor) | ✅ Có → Không (sau khi scroll đến threshold) | Sticky headers, scroll tables |

### Câu Hỏi Thêm: Absolute positioning với body vs parent

#### Khi nào `absolute` tham chiếu `body`?

**Trả lời**: `absolute` tham chiếu `body` (hoặc `html`) khi **KHÔNG có positioned ancestor** (nearest ancestor không có `position` khác `static`).

#### Khi nào `absolute` tham chiếu parent?

**Trả lời**: `absolute` tham chiếu parent khi parent (hoặc bất kỳ ancestor nào gần nhất) có `position` khác `static` (ví dụ: `relative`, `absolute`, `fixed`, `sticky`).

#### Khái niệm "Nearest Positioned Ancestor"

**Định nghĩa**: "Nearest positioned ancestor" là ancestor element gần nhất (trong cây DOM, từ parent trực tiếp tới grandparent, v.v.) mà có `position` khác `static`.

**Ví dụ**:
```html
<div id="grandparent" style="position: relative;">  <!-- Positioned ancestor -->
  <div id="parent" style="position: static;">        <!-- NOT positioned -->
    <div id="child" style="position: absolute;">     <!-- Tham chiếu #grandparent -->
      Content
    </div>
  </div>
</div>
```

Ở ví dụ trên:
- `#child` sẽ tham chiếu `#grandparent` (vì đó là nearest ancestor có `position != static`)
- `#parent` **không** được xem xét vì nó có `position: static` (mặc định)

---

## Câu A2 (10đ) — Flexbox vs Grid Layout Prediction

### Trường Hợp 1: Flex với `flex: 1` (4 items)

```css
.container { display: flex; }
.item { flex: 1; }
```

**Dự đoán layout:**
```
┌─────────────────────────────────────┐
│  Item1  │  Item2  │  Item3  │  Item4 │
└─────────────────────────────────────┘

Layout: 1 hàng, 4 cột (mỗi item bằng 25% width)
```

**Giải thích**: 
- `flex: 1` = `flex-grow: 1, flex-shrink: 1, flex-basis: 0`
- Tất cả 4 items chia đều không gian: mỗi item = 25%
- Mặc định `flex-direction: row` = 1 hàng

---

### Trường Hợp 2: Flex + Wrap (6 items)

```css
.container { display: flex; flex-wrap: wrap; }
.item { width: 45%; margin: 2.5%; }
```

**Tính toán**: 
- Mỗi item = 45% + 2.5% (trái) + 2.5% (phải) = **50% width**
- Container = 100%
- Có thể fit: **2 items per row** (50% + 50% = 100%)
- 6 items = **3 hàng**

**Dự đoán layout:**
```
┌──────────────────────────────────────┐
│    Item1    │    Item2               │
├──────────────────────────────────────┤
│    Item3    │    Item4               │
├──────────────────────────────────────┤
│    Item5    │    Item6               │
└──────────────────────────────────────┘

Layout: 3 hàng, 2 cột
```

---

### Trường Hợp 3: Flex + `space-between` + `center` (3 items)

```css
.container { display: flex; justify-content: space-between; align-items: center; }
```

**Dự đoán layout:**
```
┌────────────────────────────────────┐
│ Item1          Item2          Item3 │
└────────────────────────────────────┘

Layout: 1 hàng, 3 cột (các items ở mép ngoài & giữa)
- Item1: mép trái
- Item2: giữa
- Item3: mép phải
- Tất cả căn giữa theo chiều dọc (center)
```

**Giải thích**:
- `justify-content: space-between` = chia spacing đều giữa items, item đầu & cuối ở mép
- `align-items: center` = căn giữa các items theo chiều dọc
- Mặc định 1 hàng (flex-direction: row, flex-wrap: nowrap)

---

### Trường Hợp 4: Grid 3 columns (3 items)

```css
.container { display: grid; grid-template-columns: 200px 1fr 200px; gap: 20px; }
```

**Dự đoán layout:**
```
┌─────────┬──────────────────────┬─────────┐
│ Item1   │      Item2           │ Item3   │
│ (200px) │   (flexible/1fr)     │ (200px) │
└─────────┴──────────────────────┴─────────┘

Layout: 1 hàng, 3 cột
- Col 1: 200px (fixed)
- Col 2: 1fr (flexible - nhận hết space còn lại - flexible = 1 fraction unit)
- Col 3: 200px (fixed)
- Gap: 20px giữa các cột
```

**Giải thích**:
- `grid-template-columns: 200px 1fr 200px` = 3 columns cố định
- 3 items = 1 hàng đầy đủ
- `1fr` = 1 fraction unit = chia đều hết space còn lại

---

### Trường Hợp 5: Grid `repeat(3, 1fr)` (7 items)

```css
.container { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; }
```

**Dự đoán layout:**
```
┌──────────────┬──────────────┬──────────┐
│   Item1      │   Item2      │ Item3    │
├──────────────┼──────────────┼──────────┤
│   Item4      │   Item5      │ Item6    │
├──────────────┼──────────────┼──────────┤
│   Item7      │              │          │
└──────────────┴──────────────┴──────────┘

Layout: 3 hàng, 3 cột (cell empty cuối)
- Hàng 1: Item1, Item2, Item3
- Hàng 2: Item4, Item5, Item6
- Hàng 3: Item7 (ở cột 1), cột 2-3 trống
- Gap: 10px
```

**Giải thích**:
- `grid-template-columns: repeat(3, 1fr)` = 3 columns, mỗi column = 1fr (chia đều)
- 7 items trong 3 columns = ⌈7÷3⌉ = 3 hàng
- Row 1: cols 1,2,3 filled
- Row 2: cols 1,2,3 filled  
- Row 3: col 1 filled, cols 2,3 empty
- Mặc định hàng không xác định số = implicit rows (tự động thêm hàng cần thiết)

---

## Tóm Tắt So Sánh 5 Cases

| Case | Type | # Rows | # Cols | Layout Type | Notes |
|------|------|--------|--------|-------------|-------|
| 1 | Flex | 1 | 4 | Horizontal equal | `flex: 1` chia đều |
| 2 | Flex + Wrap | 3 | 2 | 2-column wrapped | 50% width/item |
| 3 | Flex | 1 | 3 | Spaced out | Mép ngoài & giữa |
| 4 | Grid | 1 | 3 (fixed) | Fixed-flex-fixed | 200px-1fr-200px |
| 5 | Grid | 3 | 3 | Equal grid | repeat(3, 1fr) |

---

## PHẦN B — THỰC HÀNH CODE (60 điểm)

### Bài B1 (15đ) — Positioning Playground

**Files**: `positioning.html` + `positioning.css`

**Yêu cầu hoàn thành**:
- ✅ Fixed header (60px, full width, nền #2c3e50, chữ trắng)
- ✅ Logo + Navigation (nav items căn phải)
- ✅ Sticky sidebar (250px, `position: sticky; top: 80px;`)
- ✅ Product cards với HOT badge (absolute positioning ở góc phải trên)
- ✅ Scroll to top button (position: fixed, góc phải dưới, hình tròn)
- ✅ Content dài để scroll và thấy các hiệu ứng

**Key CSS Features**:
```css
.fixed-header { position: fixed; top: 0; left: 0; right: 0; }
.sticky-sidebar { position: sticky; top: 80px; }
.badge { position: absolute; top: 10px; right: 10px; border-radius: 50%; }
.scroll-to-top { position: fixed; bottom: 30px; right: 30px; }
```

**Screenshot cần chụp**:
1. Header cố định khi scroll
2. Sidebar dính khi scroll
3. Badge HOT trên card

---

### Bài B2 (20đ) — Flexbox Navigation & Cards

**Files**: `flexbox_layout.html` + `flexbox.css`

**Phần 1 — Navbar (10đ)**:
- Logo bên trái
- Menu items giữa (`justify-content: center`)
- Login/Register nằm bên phải
- `align-items: center` cho vertical centering
- Hover effect: đổi màu + underline

**Phần 2 — Product Cards Grid (10đ)**:
- Container: `display: flex; flex-wrap: wrap;`
- Card: `flex: 0 0 calc(25% - 15px);` (4 cột/hàng)
- Card inner: `flex-direction: column` (image, title, price, button)
- Button stick to bottom: `margin-top: auto;`
- 8 cards (2 hàng × 4 cột)
- Hover: `transform: translateY(-5px);` + shadow tăng

**Key CSS Features**:
```css
.navbar { display: flex; justify-content: space-between; align-items: center; }
.products-container { display: flex; flex-wrap: wrap; gap: 20px; }
.product-card { flex: 0 0 calc(25% - 15px); display: flex; flex-direction: column; }
.btn-buy { margin-top: auto; }
```

---

### Bài B3 (25đ) — Grid Layout — E-Commerce

**Files**: `grid_layout.html` + `grid.css`

**Layout Grid chính**:
```css
grid-template-columns: 200px 1fr 200px;
grid-template-areas:
    "header header header"
    "hero hero hero"
    "sidebar main-content ads"
    "footer footer footer";
gap: 20px;
```

**Các vùng**:
- **Header**: Logo + Navigation (full width)
- **Hero**: Banner "Summer Sale" (full width, gradient background)
- **Sidebar**: Filter checkboxes (200px, left)
- **Main**: Product grid 3 cột (`grid-template-columns: repeat(3, 1fr)`)
- **Ads**: 2 ad boxes stacked (200px, right)
- **Footer**: 3 columns (About, Support, Follow) - full width

**Key CSS Features**:
```css
.container { display: grid; grid-template-columns: 200px 1fr 200px; grid-template-areas: ... }
.product-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 15px; }
```

**Content**: Ít nhất 6 product cards

---

## Summary — Các File Tạo Được

| Exercise | HTML File | CSS File | Key Techniques |
|----------|-----------|----------|-----------------|
| B1 | positioning.html | positioning.css | `position: fixed`, `sticky`, `absolute` |
| B2 | flexbox_layout.html | flexbox.css | `display: flex`, `flex-wrap`, `flex-direction: column` |
| B3 | grid_layout.html | grid.css | `display: grid`, `grid-template-areas`, nested grids |

---

## PHẦN C — SUY LUẬN (20 điểm)

### Câu C1 (10đ) — Flexbox vs Grid: Khi nào dùng gì?

| Tình huống | Dùng? | Giải thích |
|-----------|-------|-----------|
| 1. Navigation bar ngang (logo + menu + buttons) | **Flexbox** | Bố cục 1 chiều (ngang), căn chỉnh items đơn giản (`justify-content: space-between`) |
| 2. Lưới ảnh Instagram (3 cột đều, số ảnh không biết) | **Grid** | Cần layout 2 chiều cố định, `repeat(3, 1fr)` tự động wrap items |
| 3. Layout blog: main + sidebar | **Flexbox hoặc Grid** | Grid tốt hơn nếu có header/footer; Flexbox nếu chỉ main-sidebar |
| 4. Footer 4 cột (Về, Liên kết, Hỗ trợ, Liên hệ) | **Grid** hoặc **Flexbox** | Cả hai đều tốt; Grid nếu muốn cải thiệt ở desktop/mobile; Flexbox nếu đơn giản |
| 5. Card sản phẩm (ảnh/text/nút dính đáy) | **Flexbox** | `flex-direction: column` + `margin-top: auto` cho nút dính đáy |

**Tóm tắt nguyên tắc**:
- **Flexbox**: 1 chiều (row hoặc column), alignment đơn giản, items co/dãn đều
- **Grid**: 2 chiều (rows + columns), template phức tạp, precise positioning
- **Cả hai**: Layout lớn (Grid chính) + Flexbox cho từng component

---

### Câu C2 (10đ) — Debug Flexbox

#### **Lỗi 1: Cards không đều chiều cao — nút bị nhảy**

**Nguyên nhân**: Container không set `align-items: stretch`, cards không match height

**Code sửa**:
```css
.card-container { 
    display: flex; 
    flex-wrap: wrap;
    align-items: stretch;  /* ← Thêm dòng này */
}
.card { 
    width: 30%; 
    margin: 1.5%;
    display: flex;         /* ← Card cũng dùng flex */
    flex-direction: column;
}
.card .btn { 
    margin-top: auto;      /* ← Nút dính đáy */
    padding: 10px; 
}
```

**Screenshot**: Trước: nút ở vị trí khác nhau; Sau: nút luôn ở đáy card

---

#### **Lỗi 2: Content không căn giữa trong 100vh**

**Nguyên nhân**: Container `flex` nhưng không set `justify-content` và `align-items`, `.hero-content` chỉ có `text-align: center` (căn ngang text, không căn div)

**Code sửa**:
```css
.hero {
    height: 100vh;
    display: flex;
    justify-content: center;      /* ← Căn giữa ngang */
    align-items: center;           /* ← Căn giữa dọc */
}
.hero-content {
    text-align: center;
}
```

**Screenshot**: Trước: content ở góc trái trên; Sau: content ở giữa

---

#### **Lỗi 3: Sidebar bị co lại khi content dài**

**Nguyên nhân**: `.sidebar` width cố định 250px, nhưng khi content dài, flex items bị squeeze. Thiếu `flex-shrink: 0`

**Code sửa**:
```css
.layout { 
    display: flex;
}
.sidebar { 
    width: 250px;
    flex-shrink: 0;    /* ← Ngăn sidebar co lại */
}
.content { 
    flex: 1;
    overflow: auto;    /* ← Cho content scroll nếu cần */
}
```

**Screenshot**: Trước: sidebar co < 250px; Sau: sidebar giữ 250px, content scroll

---

## Tóm Tắt Bug & Fix

| Lỗi | Nguyên nhân | Fix | Kỹ thuật chính |
|-----|-----------|-----|-----------------|
| 1. Cards không đều cao | Không set `align-items: stretch` | Thêm flex column + `margin-top: auto` | `display: flex; flex-direction: column` |
| 2. Content không căn giữa | Không set `justify-content` + `align-items` | Thêm `justify-content: center; align-items: center;` | Centering with flex |
| 3. Sidebar bị co | Không set `flex-shrink: 0` | Thêm `flex-shrink: 0` | Preventing flex shrink |

