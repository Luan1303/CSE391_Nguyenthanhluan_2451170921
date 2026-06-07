# PBT_05 - CSS Responsive Design
## PHẦN A — KIỂM TRA ĐỌC HIỂU (20 điểm)

---

## Câu A1 (5đ) — Viewport & Mobile-First

### 1. Thẻ Viewport Chuẩn

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Giải thích từng thuộc tính**:
| Thuộc tính | Giá trị | Ý nghĩa |
|-----------|--------|---------|
| `name="viewport"` | - | Báo hiệu đây là cấu hình viewport |
| `width=device-width` | Device width | Chiều rộng trang = chiều rộng thiết bị (không scale cứng) |
| `initial-scale=1.0` | 1.0 (100%) | Độ zoom ban đầu = 100% (không zoom in/out) |

**Các thuộc tính khác (optional)**:
- `maximum-scale=1.0` - Người dùng không zoom được lớn hơn
- `user-scalable=no` - Disable zoom (không khuyên)
- `minimum-scale=1.0` - Zoom nhỏ nhất

### 2. Nếu THIẾU Thẻ Viewport

Nếu không có `<meta name="viewport">`, **iPhone sẽ**:
- Giả lập viewport rộng (960-1024px) để fit đặt screen
- Shrink toàn bộ trang xuống để vừa màn hình
- Text và buttons trở nên **rất nhỏ**, khó đọc
- Người dùng phải pinch-zoom mới xem được → **UX tệ**

### 3. Mobile-First vs Desktop-First

| Phương pháp | Viết CSS | Ví dụ (breakpoint 768px) | Ưu điểm |
|------------|----------|----------------------|---------|
| **Mobile-First** | Viết base CSS cho mobile, dùng `min-width` | Base: 1 cột; `@media (min-width: 768px)` → 2 cột | Dễ bảo trì, nhanh hơn mobile, users hay dùng mobile |
| **Desktop-First** | Viết base CSS cho desktop, dùng `max-width` | Base: 4 cột; `@media (max-width: 768px)` → 2 cột | Dễ với designer desktop |

**Ví dụ CSS**:

**Mobile-First**:
```css
.grid {
    display: grid;
    grid-template-columns: 1fr;  /* Base: 1 cột */
}
@media (min-width: 768px) {
    .grid {
        grid-template-columns: 1fr 1fr;  /* Tablet: 2 cột */
    }
}
```

**Desktop-First**:
```css
.grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;  /* Base: 4 cột */
}
@media (max-width: 768px) {
    .grid {
        grid-template-columns: 1fr 1fr;  /* Mobile: 2 cột */
    }
}
```

**Tại sao Mobile-First được khuyên**:
- ✅ 70% users dùng mobile → optimize cho mobile trước
- ✅ Mobile-first CSS nhẹ hơn (base simple, progressively enhance)
- ✅ Dễ bảo trì (thêm feature progressively)
- ✅ Performance tốt hơn trên mobile devices

---

## Câu A2 (5đ) — Breakpoints

**Breakpoints chuẩn (Bootstrap 5)**:

| Tên | Min-width | Thiết bị | Lưới sản phẩm |
|-----|-----------|---------|---------------|
| **Extra Small (XS)** | < 576px | Mobile (iPhone) | 1 cột |
| **Small (SM)** | ≥ 576px | Tablet nhỏ | 2 cột |
| **Medium (MD)** | ≥ 768px | Tablet | 3 cột |
| **Large (LG)** | ≥ 992px | Laptop nhỏ | 3 cột |
| **Extra Large (XL)** | ≥ 1200px | Desktop | 4 cột |
| **XXL** | ≥ 1400px | Desktop lớn | 5 cột |

**Ví dụ CSS Lưới**:
```css
/* Mobile-First */
.grid { grid-template-columns: 1fr; }  /* 1 cột */
@media (min-width: 576px) { .grid { grid-template-columns: 1fr 1fr; } }  /* 2 cột */
@media (min-width: 768px) { .grid { grid-template-columns: repeat(3, 1fr); } }  /* 3 cột */
@media (min-width: 1200px) { .grid { grid-template-columns: repeat(4, 1fr); } }  /* 4 cột */
```

---

## Câu A3 (5đ) — Media Queries

**CSS**:
```css
.container { width: 100%; padding: 10px; }
@media (min-width: 576px) { .container { width: 540px; } }
@media (min-width: 768px) { .container { width: 720px; } }
@media (min-width: 992px) { .container { width: 960px; } }
@media (min-width: 1200px) { .container { width: 1140px; } }
```

**Bảng Kết Quả**:

| Chiều rộng màn hình | `.container` width | Media query áp dụng |
|-------------------|-------------------|------------------|
| 375px (iPhone SE) | **100%** | Không (< 576px) |
| 600px (Tablet) | **540px** | ≥ 576px (SM) |
| 800px (Tablet lớn) | **720px** | ≥ 768px (MD) |
| 1000px (Laptop) | **960px** | ≥ 992px (LG) |
| 1400px (Desktop) | **1140px** | ≥ 1200px (XL) |

**Giải thích**: Mỗi media query được áp dụng khi điều kiện `min-width` thỏa mãn, nhưng nếu có media query tiếp theo cũng thỏa, nó sẽ override giá trị trước.

---

## Câu A4 (5đ) — SCSS Basics

### 4 Tính Năng Chính SCSS

#### **1. Variables (`$`)**
**Ví dụ**:
```scss
$primary-color: #3498db;
$border-radius: 8px;
$spacing: 20px;

.button {
    background-color: $primary-color;
    border-radius: $border-radius;
    padding: $spacing;
}
```

**Lợi ích**: Dễ thay đổi màu/kích thước toàn app, không cần search-replace

---

#### **2. Nesting (CSS lồng nhau)**
**Ví dụ**:
```scss
.navbar {
    background-color: #2c3e50;
    padding: 20px;

    .logo {
        font-size: 28px;
        color: white;
    }

    .menu {
        display: flex;
        gap: 20px;

        a {
            color: white;
            text-decoration: none;

            &:hover {
                color: #3498db;
            }
        }
    }
}
```

**CSS Output**:
```css
.navbar { background-color: #2c3e50; }
.navbar .logo { font-size: 28px; }
.navbar .menu { display: flex; }
.navbar .menu a { color: white; }
.navbar .menu a:hover { color: #3498db; }
```

**Lợi ích**: Code gọn hơn, dễ đọc, scope clear

---

#### **3. Mixins (`@mixin`, `@include`)**
**Ví dụ**:
```scss
@mixin flexbox {
    display: flex;
    justify-content: center;
    align-items: center;
}

@mixin responsive-font($mobile-size, $desktop-size) {
    font-size: $mobile-size;
    @media (min-width: 768px) {
        font-size: $desktop-size;
    }
}

.hero {
    @include flexbox;
    height: 100vh;
}

h1 {
    @include responsive-font(24px, 48px);
}
```

**Lợi ích**: Reuse CSS patterns, DRY (Don't Repeat Yourself)

---

#### **4. @extend / Inheritance**
**Ví dụ**:
```scss
%button-base {
    padding: 12px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
}

.btn-primary {
    @extend %button-base;
    background-color: #3498db;
    color: white;
}

.btn-secondary {
    @extend %button-base;
    background-color: #95a5a6;
    color: white;
}
```

**Lợi ích**: Share base styles, tránh lặp code

---

### Tại sao Trình duyệt KHÔNG đọc được `.scss`?

**Lý do**:
- Trình duyệt chỉ hiểu CSS, HTML, JavaScript
- SCSS là **preprocessor language** (ngôn ngữ xử lý trước)
- SCSS phải được **compile → CSS** trước khi deploy

**Bước Chuyển Đổi SCSS → CSS**:

```
1. Viết file .scss
2. Dùng SCSS compiler (Sass, node-sass, dart-sass, etc.)
3. Compile → file .css
4. Link .css vào HTML
5. Trình duyệt đọc file .css
```

**Công cụ Compile Phổ Biến**:
```bash
# Cách 1: Command line
sass input.scss output.css

# Cách 2: VS Code Extension (Live Sass Compiler)
# Cách 3: Build tool (Webpack, Vite, Parcel)
```

**Ví dụ**:
```scss
// input.scss
$color: red;
.box { color: $color; }
```

```css
/* output.css (sau compile) */
.box { color: red; }
```

---

## Tóm Tắt A1-A4

| Chủ đề | Điểm chính |
|--------|-----------|
| **A1 - Viewport** | `<meta name="viewport" content="width=device-width, initial-scale=1.0">` |
| **A1 - Mobile-First** | Viết base cho mobile, `@media (min-width)` để enhance. Được khuyên vì 70% users mobile |
| **A2 - Breakpoints** | XS(<576), SM(576), MD(768), LG(992), XL(1200), XXL(1400) |
| **A3 - Media Queries** | 375px→100%; 600px→540px; 800px→720px; 1000px→960px; 1400px→1140px |
| **A4 - SCSS** | Variables, Nesting, Mixins, Extend. Cần compile SCSS→CSS |

---

## PHẦN B — THỰC HÀNH CODE (60 điểm)

### Bài B1 (25đ) — Responsive Product Page

**Files**: `responsive.html` + `responsive.css`

**Mobile-First Approach**:
- CSS mặc định = mobile (1 cột)
- `@media (min-width: 768px)` → Tablet (2 cột)
- `@media (min-width: 1024px)` → Desktop (4 cột)

**Responsive Features**:
- ✅ Hamburger menu (☰) trên mobile, nav ngang trên desktop
- ✅ Sidebar ẩn mobile, hiện tablet+ (`position: sticky; top: 80px`)
- ✅ Product grid: 1col → 2col → 4col
- ✅ Ads bar ẩn mobile, hiện desktop
- ✅ Ảnh responsive: `max-width: 100%; height: auto`
- ✅ Font size thay đổi theo breakpoint
- ✅ 8 product cards

**Breakpoints**:
```css
/* Mobile (default) - 375px */
.product-grid { grid-template-columns: 1fr; }

/* Tablet - 768px+ */
@media (min-width: 768px) {
    .product-grid { grid-template-columns: repeat(2, 1fr); }
    .sidebar { display: block; }
}

/* Desktop - 1024px+ */
@media (min-width: 1024px) {
    .main-container { grid-template-columns: 200px 1fr 180px; }
    .product-grid { grid-template-columns: repeat(4, 1fr); }
    .ads-bar { display: flex; }
}
```

---

### Bài B2 (15đ) — CSS Transitions & Animations

**Files**: `animations.html` + `animations.css`

**5 Hiệu Ứng Bắt Buộc**:

#### 1. Card Hover Effect
```css
.card {
    transition: all 0.3s ease;
}
.card:hover {
    transform: translateY(-8px);
    box-shadow: 0 12px 24px rgba(0,0,0,0.15);
}
```

#### 2. Button Hover Effect
```css
.btn {
    transition: all 0.3s ease;
}
.btn:hover {
    background-color: #2980b9;
    transform: scale(1.05);
}
```

#### 3. Image Zoom On Hover
```css
.image-container {
    overflow: hidden;
}
.image-container:hover img {
    transform: scale(1.1);
    transition: transform 0.4s ease;
}
```

#### 4. Loading Spinner Animation
```css
@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}
.spinner {
    width: 50px;
    height: 50px;
    border: 4px solid #ecf0f1;
    border-top: 4px solid #3498db;
    border-radius: 50%;
    animation: spin 1s linear infinite;
}
```

#### 5. Fade-In Animation
```css
@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}
.fade-in {
    animation: fadeIn 0.8s ease-in-out;
}
```

---

### Bài B3 (20đ) — SCSS Refactor

**File Structure**:
```
scss/
├── _variables.scss    (Colors, fonts, spacing, breakpoints)
├── _mixins.scss       (Responsive, flex-center, card-shadow, etc.)
├── _components.scss   (Card, button, sidebar, footer - with nesting)
└── style.scss         (Main - import all partials)
```

**8+ Variables**:
```scss
$primary-color: #3498db;
$secondary-color: #2c3e50;
$light-bg: #f5f5f5;
$font-primary: 'Segoe UI', Tahoma, Geneva, sans-serif;
$breakpoint-md: 768px;
$breakpoint-lg: 1024px;
$spacing-md: 16px;
$shadow-sm: 0 2px 8px rgba(0,0,0,0.1);
```

**3+ Mixins**:
```scss
@mixin respond-to($breakpoint) { ... }  /* Responsive */
@mixin flex-center { ... }               /* Centered flex */
@mixin card-shadow { ... }               /* Card elevation */
```

**Nesting with Parent Selector (&)**:
```scss
.card {
    padding: 20px;
    
    .card-image { ... }
    .card-title { ... }
    
    &:hover {
        transform: translateY(-8px);
    }
    
    &.featured {
        border: 2px solid $primary-color;
    }
}
```

**Compile SCSS → CSS**:
```bash
# Install Sass globally
npm install -g sass

# Compile command
sass scss/style.scss style.css

# Watch mode (auto-compile on save)
sass --watch scss:. 
```

**Output**: `style.css` được sinh từ `scss/style.scss`

---

## Tóm Tắt PHẦN B

| Bài | Files | Key Features |
|-----|-------|--------------|
| **B1** | responsive.html + responsive.css | Mobile-first, 3 breakpoints, hamburger menu, responsive grid |
| **B2** | animations.html + animations.css | 5 animations (card hover, button, image zoom, spinner, fade-in) |
| **B3** | scss/ folder | Variables, nesting, mixins, partials, SCSS→CSS compile |

---

## PHẦN C — PHÂN TÍCH (20 điểm)

### Câu C1 (10đ) — Phân tích trang web thực

**Trang web chọn**: YouTube

**Phân tích trên 3 kích thước**:

| Aspect | Mobile (375px) | Tablet (768px) | Desktop (1440px) |
|--------|----------------|----------------|------------------|
| **Navigation** | Hamburger menu ☰ + logo | Hamburger + logo | Horizontal nav + search |
| **Grid/Layout** | 1 cột (video list) | 2 cột (videos) | 3-4 cột (video grid) |
| **Hidden Elements** | Sidebar ẩn | Sidebar ẩn | Sidebar visible (left) |
| **Font Size** | 14px (smaller) | 15px (medium) | 16px (base) |
| **Trending Section** | Vertical list | 2 cột | 3 cột grid |

**CSS Media Queries trang YouTube sử dụng**:
```css
/* Mobile First */
.video-grid { display: grid; grid-template-columns: 1fr; }
.sidebar { display: none; }
.nav { flex-direction: column; }

/* Tablet - 768px+ */
@media (min-width: 768px) {
    .video-grid { grid-template-columns: repeat(2, 1fr); }
}

/* Desktop - 1024px+ */
@media (min-width: 1024px) {
    .sidebar { display: block; width: 250px; }
    .video-grid { grid-template-columns: repeat(3, 1fr); }
    .nav { flex-direction: row; }
}
```

**Screenshot DevTools (mô phỏng)**:
- Mobile: Video list nhỏ, hamburger menu ☰
- Tablet: 2 cột video, sidebar ẩn
- Desktop: Sidebar + 3-4 cột video, nav ngang

---

### Câu C2 (10đ) — Thiết kế Responsive Strategy: Trang Đặt Bàn Nhà Hàng

#### **Wireframes 3 Layout**:

**Mobile (375px)**:
```
┌──────────────────────────┐
│   Header (Logo + Phone)   │ (sticky)
├──────────────────────────┤
│      Hero Image (full)   │
├──────────────────────────┤
│      Grid 1 cột (6 ảnh)  │
│   (scroll dọc)           │
├──────────────────────────┤
│    Form Đặt Bàn (full)   │
│  - Ngày / Giờ / Người    │
│  - Ghi chú               │
├──────────────────────────┤
│  Bản đồ (nhỏ)            │
├──────────────────────────┤
│     Footer               │
└──────────────────────────┘
```

**Tablet (768px)**:
```
┌──────────────────────────────────┐
│   Header (Logo + Phone)          │
├──────────────────────────────────┤
│      Hero Image (full width)     │
├──────────────────────────────────┤
│  Grid 2 cột (6 ảnh)              │
├──────────────┬──────────────────┤
│ Form (left)  │  Bản đồ (right)  │
│ Đặt Bàn      │  Google Maps     │
├──────────────┴──────────────────┤
│     Footer (3 cột)              │
└──────────────────────────────────┘
```

**Desktop (1440px)**:
```
┌─────────────────────────────────────────────┐
│      Header (Logo + Phone) - sticky         │
├─────────────────────────────────────────────┤
│         Hero Image (full width)             │
├─────────────────────────────────────────────┤
│    Grid 3 cột (6 ảnh) - responsive         │
├──────────────────┬────────────────────────┤
│   Form Đặt Bàn   │   Google Maps Bản đồ   │
│   (400px left)   │   (flex: 1 right)      │
├──────────────────┴────────────────────────┤
│  Footer (4 cột - About | Menu | Hours | Social)
└─────────────────────────────────────────────┘
```

#### **CSS Skeleton (Mobile-First)**:

```css
/* ===== MOBILE FIRST (Default) ===== */
.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    position: sticky;
    top: 0;
    background-color: white;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.logo { font-size: 24px; }
.phone { font-size: 14px; }

.hero {
    width: 100%;
    height: 250px;
    background-image: url('hero.jpg');
    background-size: cover;
}

.food-grid {
    display: grid;
    grid-template-columns: 1fr;  /* 1 cột mobile */
    gap: 15px;
    padding: 20px;
}

.food-item {
    aspect-ratio: 1;
    background-size: cover;
    border-radius: 8px;
}

.booking-form {
    padding: 20px;
    background-color: #f5f5f5;
}

.booking-form input,
.booking-form textarea {
    width: 100%;
    margin-bottom: 15px;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
}

.booking-form button {
    width: 100%;
    padding: 12px;
    background-color: #e74c3c;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
}

.map {
    width: 100%;
    height: 300px;
    margin: 20px 0;
}

.footer {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
    padding: 40px 20px;
    background-color: #2c3e50;
    color: white;
}

/* ===== TABLET (768px+) ===== */
@media (min-width: 768px) {
    .food-grid {
        grid-template-columns: repeat(2, 1fr);
    }

    .booking-section {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 20px;
    }

    .booking-form {
        padding: 20px;
    }

    .map {
        height: 400px;
    }

    .footer {
        grid-template-columns: repeat(2, 1fr);
    }
}

/* ===== DESKTOP (1024px+) ===== */
@media (min-width: 1024px) {
    .food-grid {
        grid-template-columns: repeat(3, 1fr);
    }

    .booking-section {
        display: grid;
        grid-template-columns: 400px 1fr;
        gap: 30px;
        padding: 40px 20px;
    }

    .booking-form {
        background-color: white;
        padding: 30px;
        border-radius: 8px;
        box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .map {
        border-radius: 8px;
        height: 500px;
    }

    .footer {
        grid-template-columns: repeat(4, 1fr);
    }
}

/* ===== EXTRA LARGE (1440px+) ===== */
@media (min-width: 1440px) {
    .hero {
        height: 400px;
    }

    .booking-section {
        max-width: 1400px;
        margin: 0 auto;
    }
}
```

#### **Key Responsive Features**:

| Aspect | Mobile | Tablet | Desktop |
|--------|--------|--------|---------|
| **Food Grid** | 1 cột | 2 cột | 3 cột |
| **Booking + Map** | Vertical (form↓map) | Side-by-side | Form (400px) + Map (flex) |
| **Footer** | 1 cột | 2 cột | 4 cột |
| **Hero Height** | 250px | 300px | 400px |
| **Padding** | 15-20px | 20px | 40px |

#### **Responsive Strategy Highlights**:
✅ Mobile-first CSS (base = mobile layout)
✅ Form full-width on mobile → 400px sidebar on desktop
✅ Grid auto-adjusts (1 → 2 → 3 columns)
✅ Map scales with viewport
✅ Header sticky on all sizes
✅ Touch-friendly buttons (12px padding)
