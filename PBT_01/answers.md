# PHẦN A - KIỂM TRA ĐỌC HIỂU:

## Câu A1: (Tài liệu 01_instroduction_html_universe.md)
1. Thứ tự 5 bước khi gõ `https://shopee.vn`:
    - DNS: Trình duyệt tra cứu địa chỉ IP của trang web.
    - HTTP: gửi request đến với server
    - Parse HTML: trình duyệt đọc HTML và bắt đầu tạo DOM Tree
    - Layout: trình duyệt tính toán vị trí và kích thước từng phần tử trên trang
    - Reder: render dữ liệu HTML/CSS
2. Screenshots file `PBT01_A1-2.png`.

## Câu A2: (Tài liệu: 04_visible_part_html.md)
Web bị đánh giá thấp vì sử dụng quá nhiều thẻ div mà không có thẻ semantic nào để định hình bố cục của web.
Các lỗi semantic:
- `<div class="header">`
- `<div class="menu">`
- `<div class="main">`
- `<div class="product">`
Nên thay thế thành:
- `<head>`
- `<nav>`
- `<main>`
- `<article>`
## Câu A3: (Tài liệu: 04_visible_part_html.md)
```html
[Hộp 1]
Text A Text B
[Hộp 2]
Text C Text D
[Hộp 3]
```
- `<div>` là 1 thẻ thuộc Block element vì vậy khi kết thúc thẻ sẽ xuống 1 dòng mới.
- `<span>` và `<strong>` là 2 thẻ thuộc Inline element vì vậy khi kết thúc thẻ thì vẫn sẽ nằm trên dòng đó không xuống dòng mới.

## Câu A4:
- `<thead>` là tiêu đề của cột, vị trí xuất hiện trên cùng
- `<tbody>` là dữ liệu chính của bảng, vị trí xuất hiện ở giữa
- `<tfoot>` là tổng kết, vị trí xuất hiện ở dưới cùng
* Lý do không nên dùng `<table>` làm layout:
- Table không linh hoạt được như CSS Grid/Flexbox
- Code khi dùng với Table dễ rối hơn
- Table chỉ được thiết kế để hiển thị dữ liệu bảng, không phải layout trang nên các trình duyệt sẽ chỉ hiểu table là dữ liệu.

# PHẦN B - THỰC HÀNH CODE:

## Câu B3:
Các lỗi có trong bài là:
- `<!DOCTYPE>`ở dòng 136 thiếu html -> Sửa thành `<!DOCTYPE html>`.
- `<title>Trang web`ở dòng 139 thiếu thẻ đóng title -> Sửa thành `<title>Trang web</title>`.
- `<h1>Welcome to ShopTLU<h1>` ở dòng 143 thẻ đóng bị sai -> Sửa thành `<h1>Welcome to ShopTLU</h1>`.
- `<a href="home">Trang chủ<a>` ở dòng 147 thẻ đóng bị sai -> Sửa thành `<a href="home">Trang chủ</a>`.
- `<img src=iphone.jpg>` ở dòng 155 sau phần src= thiếu dấu ngoặc kép -> Sửa thành `<img src="iphone.jpg">`.
- `<p>Giá: <b>25.990.000đ</p></b>` ở dòng 157 để sai vị trí thẻ đóng của thẻ `<b>` -> Sửa thành `<p>Giá: <b>25.990.000đ</b></p>`.
- Từ dòng 162 đến 170 Table nên sửa dụng 2 thẻ `<thead>` và `<tbody>`.
- `<td>` từ dòng 164 trong Table nên thay `<td>` thành `<th>`.

## Câu B4:
1 Với trang shoppe, 3 thẻ semantic HTML5 được sử dụng:
- <html dir="ltr" lang="vi"> — dòng 2 (lang="vi"báo cho trình đọc màn hình sử dụng giọng đọc tiếng Việt; dir="ltr"khai báo chiều đọc văn bản. Không cần trang trí — là siêu dữ liệu ngôn ngữ thực sự.)
- <noscript> — dòng 5 (Đây là thẻ ngữ nghĩa rõ ràng nhất trên trang: trình duyệt hiểu nội dung bên trong chỉ hiển thị khi JavaScript tắt.)
- <iframe title="_hjSafeContext">( bộ ba thuộc tính này cho thấy nhóm Hotjar có ý thức về khả năng truy cập: ẩn iframe vô nghĩa khỏi trình đọc màn hình.)
  2 thẻ không dùng đúng semantic:
- <div id="main">thay vì<main> — dòng 6 (<div id="main">…</div>. Toàn bộ nội dung trang nằm ở đây nhưng không phải <main>. Mất mốc đọc màn hình, người dùng bàn phím không thể "Chuyển sang nội dung chính".)
- <div id="modal">thay vì<dialog> — dòng 17 (Không có role="dialog", không có aria-modal, không có bẫy tự động lấy nét. Khi modal open, screen reader không có thông báo gì.)
2.Trong ảnh này không có table nào cả
3.trong ảnh không có form nào cả

# PHẦN C - SUY LUẬN:
## Câu C1:
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>iPhone 16 - Chi tiết sản phẩm</title>
</head>
<body>

  <!-- HEADER: landmark "banner" -->
  <header>
    <a href="/" aria-label="Về trang chủ"><!-- Logo --></a>

    <!-- NAV: landmark "navigation" -->
    <nav aria-label="Điều hướng chính">
      <ul>
        <li><a href="/dien-thoai">Điện thoại</a></li>
        <li><a href="/may-tinh-bang">Máy tính bảng</a></li>
        <li><a href="/phu-kien">Phụ kiện</a></li>
      </ul>
    </nav>

    <!-- SEARCH: thẻ <search> HTML5 -->
    <search>
      <label for="q">Tìm kiếm</label>
      <input id="q" type="search" placeholder="Tìm sản phẩm..." />
      <button type="submit">Tìm</button>
    </search>
  </header>

  <!-- BREADCRUMB: <ol> vì có thứ tự -->
  <nav aria-label="breadcrumb">
    <ol>
      <li><a href="/">Trang chủ</a></li>
      <li><a href="/dien-thoai">Điện thoại</a></li>
      <li aria-current="page">iPhone 16</li>
    </ol>
  </nav>

  <!-- MAIN: landmark "main", chỉ 1 trên trang -->
  <main>
    <div class="layout-product-page"> <!-- div: wrapper layout thuần túy -->

      <!-- ARTICLE: nội dung độc lập, có thể chia sẻ riêng lẻ -->
      <article>
        <h1>Apple iPhone 16</h1>

        <!-- FIGURE: nhóm ảnh có chú thích -->
        <figure>
          <img src="" alt="iPhone 16 màu đen, mặt trước" width="600" height="600" />
          <ul aria-label="Ảnh sản phẩm khác">
            <li><button type="button" aria-label="Xem ảnh mặt sau"><img src="" alt="iPhone 16 mặt sau" width="80" height="80" /></button></li>
            <li><button type="button" aria-label="Xem ảnh cạnh bên"><img src="" alt="iPhone 16 cạnh bên" width="80" height="80" /></button></li>
            <li><button type="button" aria-label="Xem ảnh hộp"><img src="" alt="Hộp iPhone 16" width="80" height="80" /></button></li>
            <li><button type="button" aria-label="Xem ảnh phụ kiện"><img src="" alt="Phụ kiện trong hộp" width="80" height="80" /></button></li>
            <li><button type="button" aria-label="Xem ảnh màu titan"><img src="" alt="iPhone 16 màu titan" width="80" height="80" /></button></li>
          </ul>
          <figcaption>Bộ ảnh chính thức iPhone 16 — 5 góc chụp</figcaption>
        </figure>

        <!-- SECTION: nhóm thông tin giá/đánh giá -->
        <section aria-labelledby="info-heading">
          <h2 id="info-heading">Thông tin sản phẩm</h2>
          <p>Giá: <strong>22.990.000 đ</strong></p>
          <p>Giá gốc: <s>25.990.000 đ</s></p> <!-- <s>: nội dung không còn áp dụng -->
          <p>
            Đánh giá:
            <meter value="4.5" min="0" max="5" title="4.5 trên 5 sao">4.5/5</meter>
            <span aria-hidden="true">★★★★½</span>
            <span>(1.284 đánh giá)</span>
          </p>
          <p>iPhone 16 với chip A18, camera 48MP, màn hình 6.1 inch, pin 3.561 mAh.</p>

          <!-- FIELDSET: nhóm radio có ngữ cảnh cho screen reader -->
          <fieldset>
            <legend>Dung lượng</legend>
            <label><input type="radio" name="storage" value="128gb" checked /> 128 GB</label>
            <label><input type="radio" name="storage" value="256gb" /> 256 GB</label>
            <label><input type="radio" name="storage" value="512gb" /> 512 GB</label>
          </fieldset>

          <button type="button">Thêm vào giỏ hàng</button>
          <button type="button">Mua ngay</button>
        </section>

        <!-- SECTION + TABLE: dữ liệu quan hệ 2 chiều -->
        <section aria-labelledby="specs-heading">
          <h2 id="specs-heading">Thông số kỹ thuật</h2>
          <table>
            <caption>Thông số kỹ thuật chi tiết iPhone 16</caption>
            <thead>
              <tr>
                <th scope="col">Thông số</th>
                <th scope="col">Chi tiết</th>
              </tr>
            </thead>
            <tbody>
              <tr><th scope="row">Màn hình</th><td>6.1 inch, Super Retina XDR, 2556×1179 px</td></tr>
              <tr><th scope="row">Chip</th><td>Apple A18, 6 nhân</td></tr>
              <tr><th scope="row">Camera sau</th><td>48 MP + 12 MP siêu rộng</td></tr>
              <tr><th scope="row">Pin</th><td>3.561 mAh, sạc nhanh 25W</td></tr>
              <tr><th scope="row">Hệ điều hành</th><td>iOS 18</td></tr>
            </tbody>
          </table>
        </section>

        <!-- SECTION: reviews — mỗi review là <article> độc lập -->
        <section aria-labelledby="reviews-heading">
          <h2 id="reviews-heading">Đánh giá từ khách hàng</h2>

          <article>
            <h3>Sản phẩm tốt, giao hàng nhanh</h3>
            <address>Nguyễn Văn A</address>
            <time datetime="2025-04-10">10 tháng 4, 2025</time>
            <p>Máy đẹp, hiệu năng mượt, pin dùng được cả ngày...</p>
          </article>

          <article>
            <h3>Hài lòng với camera</h3>
            <address>Trần Thị B</address>
            <time datetime="2025-04-08">8 tháng 4, 2025</time>
            <p>Camera chụp đêm cải thiện rõ rệt so với đời trước...</p>
          </article>

          <!-- FORM: gửi dữ liệu người dùng lên server -->
          <form method="post" action="/reviews">
            <h3>Viết đánh giá của bạn</h3>
            <label for="review-title">Tiêu đề</label>
            <input id="review-title" type="text" name="title" required />
            <label for="review-body">Nội dung</label>
            <textarea id="review-body" name="body" rows="4" required></textarea>
            <button type="submit">Gửi đánh giá</button>
          </form>
        </section>

      </article>

      <!-- ASIDE: nội dung bổ sung, landmark "complementary" -->
      <aside aria-labelledby="related-heading">
        <h2 id="related-heading">Sản phẩm tương tự</h2>
        <ul>
          <li>
            <article>
              <a href="/iphone-15"><img src="" alt="iPhone 15" width="150" height="150" /><h3>iPhone 15</h3></a>
              <p><strong>19.990.000 đ</strong></p>
            </article>
          </li>
          <li>
            <article>
              <a href="/samsung-galaxy-s25"><img src="" alt="Samsung Galaxy S25" width="150" height="150" /><h3>Samsung Galaxy S25</h3></a>
              <p><strong>21.990.000 đ</strong></p>
            </article>
          </li>
          <li>
            <article>
              <a href="/pixel-9"><img src="" alt="Google Pixel 9" width="150" height="150" /><h3>Google Pixel 9</h3></a>
              <p><strong>18.990.000 đ</strong></p>
            </article>
          </li>
        </ul>
      </aside>

    </div>
  </main>

  <!-- FOOTER: landmark "contentinfo" -->
  <footer>
    <address>Công ty TNHH Thương mại ABC — 123 Nguyễn Văn Linh, TP. HCM</address>
    <nav aria-label="Điều hướng footer">
      <ul>
        <li><a href="/chinh-sach-bao-mat">Chính sách bảo mật</a></li>
        <li><a href="/dieu-khoan">Điều khoản sử dụng</a></li>
        <li><a href="/lien-he">Liên hệ</a></li>
      </ul>
    </nav>
    <small>© 2025 ABC Shop. All rights reserved.</small>
  </footer>

</body>
</html>


## Câu C2:

Quan điểm “dùng `<div>` cho mọi thứ rồi thêm class là đủ” nghe có vẻ nhanh, nhưng về lâu dài lại gây nhiều vấn đề kỹ thuật, đặc biệt là **SEO** và **Accessibility**.

Thứ nhất, về **SEO**, các công cụ tìm kiếm như Google không chỉ đọc nội dung mà còn đánh giá cấu trúc trang. Khi dùng semantic HTML như `<header>`, `<main>`, `<article>`, `<section>`, `<nav>`, bot dễ hiểu đâu là phần chính, đâu là menu, đâu là bài viết. Nếu mọi thứ đều là `<div>`, cấu trúc trở nên “mù mờ”, khiến việc lập chỉ mục và xếp hạng kém hiệu quả hơn.

Thứ hai, về **Accessibility**, semantic HTML hỗ trợ người dùng dùng screen reader (người khiếm thị). Ví dụ, screen reader có thể đọc “Navigation” khi gặp `<nav>`, hoặc chuyển nhanh đến `<main>`. Nếu chỉ dùng `<div>`, lập trình viên phải tự thêm ARIA role thủ công, dễ sai và mất thời gian hơn.

Ví dụ cụ thể: thay vì viết
`<div class="menu">...</div>`
ta dùng `<nav>...</nav>`. Screen reader sẽ tự hiểu đây là thanh điều hướng, và người dùng có thể nhảy thẳng đến menu mà không cần dò từng dòng.

Tuy nhiên, `<div>` vẫn phù hợp trong thực tế, chẳng hạn khi cần **bọc layout** hoặc nhóm các phần tử chỉ để CSS/JS xử lý, ví dụ `<div class="card">` chứa ảnh, tiêu đề, nút bấm nhưng không mang ý nghĩa nội dung riêng biệt.

Tóm lại, semantic HTML không phải “thừa”, mà là nền tảng giúp web chuẩn hơn và dễ bảo trì hơn.
