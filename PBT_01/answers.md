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

  <!-- =========================================================
       HEADER + NAVIGATION
       <header> vì đây là vùng nhận diện thương hiệu đầu trang,
       giúp screen reader nhảy thẳng đến landmark "banner".
       ========================================================= -->
  <header>

    <!-- <a> để logo có thể click về trang chủ, đúng ngữ nghĩa hơn <div> -->
    <a href="/" aria-label="Về trang chủ">
      <!-- Logo placeholder -->
    </a>

    <!-- <nav> vì đây là khối điều hướng chính của site;
         landmark "navigation" giúp screen reader nhận ra ngay -->
    <nav aria-label="Điều hướng chính">
      <!-- <ul> vì các mục menu là danh sách không có thứ tự -->
      <ul>
        <li><a href="/dien-thoai">Điện thoại</a></li>
        <li><a href="/may-tinh-bang">Máy tính bảng</a></li>
        <li><a href="/phu-kien">Phụ kiện</a></li>
      </ul>
    </nav>

    <!-- <search> (HTML5.3) hoặc <form role="search"> để crawler
         và AT hiểu đây là chức năng tìm kiếm, không phải form thường -->
    <search>
      <label for="site-search">Tìm kiếm</label>
      <input id="site-search" type="search" placeholder="Tìm sản phẩm..." />
      <button type="submit">Tìm</button>
    </search>

  </header>
  <!-- /header -->


  <!-- =========================================================
       BREADCRUMB
       <nav aria-label="breadcrumb"> vì breadcrumb là dạng
       điều hướng phụ; label phân biệt với <nav> chính ở trên.
       <ol> vì breadcrumb CÓ THỨ TỰ (Trang chủ → Danh mục → SP).
       ========================================================= -->
  <nav aria-label="breadcrumb">
    <ol>
      <li><a href="/">Trang chủ</a></li>       <!-- cấp 1 -->
      <li><a href="/dien-thoai">Điện thoại</a></li> <!-- cấp 2 -->
      <li aria-current="page">iPhone 16</li>   <!-- trang hiện tại, không cần link -->
    </ol>
  </nav>
  <!-- /breadcrumb -->


  <!-- =========================================================
       NỘI DUNG CHÍNH
       <main> đảm bảo chỉ có 1 vùng nội dung chính trên trang;
       landmark "main" cho phép skip navigation bằng bàn phím.
       ========================================================= -->
  <main>

    <!-- <div> hợp lý ở đây: wrapper layout 2 cột (product + sidebar),
         không mang ý nghĩa ngữ nghĩa, chỉ phục vụ CSS grid/flex -->
    <div class="layout-product-page">


      <!-- =====================================================
           KHU VỰC SẢN PHẨM (ảnh + thông tin + specs + reviews)
           <article> vì đây là nội dung độc lập, có thể tồn tại
           riêng lẻ ngoài ngữ cảnh trang (chia sẻ, RSS, v.v.)
           ===================================================== -->
      <article>

        <!-- <h1> vì tên sản phẩm là tiêu đề cấp cao nhất của trang;
             mỗi trang chỉ nên có 1 <h1> -->
        <h1>Apple iPhone 16</h1>


        <!-- ---------------------------------------------------
             KHU VỰC ẢNH SẢN PHẨM
             <figure> bao bọc nhóm ảnh có liên quan đến nhau;
             <figcaption> mô tả chú thích cho toàn bộ nhóm ảnh.
             --------------------------------------------------- -->
        <figure>

          <!-- <img> chính — ảnh lớn đang hiển thị -->
          <!-- alt mô tả nội dung ảnh, quan trọng cho screen reader & SEO -->
          <img
            src=""
            alt="iPhone 16 màu đen, mặt trước"
            width="600"
            height="600"
          />

          <!-- Danh sách thumbnail: <ul> vì không có thứ tự bắt buộc -->
          <ul aria-label="Ảnh sản phẩm khác">
            <li>
              <button type="button" aria-label="Xem ảnh mặt sau">
                <img src="" alt="iPhone 16 mặt sau" width="80" height="80" />
              </button>
            </li>
            <li>
              <button type="button" aria-label="Xem ảnh cạnh bên">
                <img src="" alt="iPhone 16 cạnh bên" width="80" height="80" />
              </button>
            </li>
            <li>
              <button type="button" aria-label="Xem ảnh hộp sản phẩm">
                <img src="" alt="Hộp iPhone 16" width="80" height="80" />
              </button>
            </li>
            <li>
              <button type="button" aria-label="Xem ảnh phụ kiện đi kèm">
                <img src="" alt="Phụ kiện trong hộp" width="80" height="80" />
              </button>
            </li>
            <li>
              <button type="button" aria-label="Xem ảnh màu titan">
                <img src="" alt="iPhone 16 màu titan" width="80" height="80" />
              </button>
            </li>
          </ul>

          <figcaption>Bộ ảnh chính thức iPhone 16 — 5 góc chụp</figcaption>

        </figure>
        <!-- /figure ảnh -->


        <!-- ---------------------------------------------------
             THÔNG TIN SẢN PHẨM
             <section> vì đây là một phần có chủ đề riêng biệt
             (giá, đánh giá, mô tả) bên trong article.
             --------------------------------------------------- -->
        <section aria-labelledby="product-info-heading">

          <!-- <h2> tiêu đề cấp 2, cấp con của <h1> tên sản phẩm -->
          <h2 id="product-info-heading">Thông tin sản phẩm</h2>

          <!-- <p> đơn giản cho giá — đây là đoạn văn bản thông thường -->
          <p>
            Giá:
            <!-- <strong> vì giá là thông tin quan trọng nhất về mặt ngữ nghĩa,
                 không chỉ in đậm về mặt trình bày -->
            <strong>22.990.000 đ</strong>
          </p>

          <!-- <p> chứa giá gốc; <s> (strikethrough) đúng ngữ nghĩa
               "nội dung không còn chính xác/áp dụng nữa" (giá cũ) -->
          <p>Giá gốc: <s>25.990.000 đ</s></p>

          <!-- Đánh giá sao: dùng <meter> vì nó biểu diễn
               một giá trị trong phạm vi đã biết (0–5 sao) -->
          <p>
            Đánh giá:
            <meter value="4.5" min="0" max="5" title="4.5 trên 5 sao">
              4.5/5 sao
            </meter>
            <!-- <span> thuần túy để nhóm text hiển thị, không có ngữ nghĩa riêng -->
            <span aria-hidden="true">★★★★½</span>
            <span>(1.284 đánh giá)</span>
          </p>

          <!-- Mô tả ngắn: <p> là phần tử phù hợp cho đoạn văn xuôi -->
          <p>
            iPhone 16 với chip A18, camera 48MP, màn hình Super Retina XDR 6.1 inch,
            pin 3.561 mAh hỗ trợ sạc nhanh 25W.
          </p>

          <!-- Chọn phiên bản: <fieldset> + <legend> đúng chuẩn
               nhóm các input liên quan, giúp screen reader đọc ngữ cảnh -->
          <fieldset>
            <legend>Dung lượng</legend>
            <label>
              <input type="radio" name="storage" value="128gb" checked /> 128 GB
            </label>
            <label>
              <input type="radio" name="storage" value="256gb" /> 256 GB
            </label>
            <label>
              <input type="radio" name="storage" value="512gb" /> 512 GB
            </label>
          </fieldset>

          <!-- <button> (không phải <div> hay <a>) vì đây là hành động,
               có thể focus bằng bàn phím, có role="button" mặc định -->
          <button type="button">Thêm vào giỏ hàng</button>
          <button type="button">Mua ngay</button>

        </section>
        <!-- /section thông tin sản phẩm -->


        <!-- ---------------------------------------------------
             BẢNG THÔNG SỐ KỸ THUẬT
             <section> riêng vì đây là chủ đề độc lập với phần giá/mô tả.
             <table> vì dữ liệu là dạng quan hệ 2 chiều (tên thông số : giá trị).
             --------------------------------------------------- -->
        <section aria-labelledby="specs-heading">

          <h2 id="specs-heading">Thông số kỹ thuật</h2>

          <table>
            <!-- <caption> mô tả bảng cho screen reader,
                 tốt hơn chỉ dùng heading đứng bên ngoài -->
            <caption>Thông số kỹ thuật chi tiết iPhone 16</caption>

            <thead>
              <tr>
                <!-- <th scope="col"> khai báo đây là header của cột,
                     giúp AT liên kết ô dữ liệu với đúng tiêu đề -->
                <th scope="col">Thông số</th>
                <th scope="col">Chi tiết</th>
              </tr>
            </thead>

            <tbody>
              <!-- <th scope="row"> cho tiêu đề từng hàng -->
              <tr>
                <th scope="row">Màn hình</th>
                <td>6.1 inch, Super Retina XDR, 2556 × 1179 px</td>
              </tr>
              <tr>
                <th scope="row">Chip</th>
                <td>Apple A18, 6 nhân</td>
              </tr>
              <tr>
                <th scope="row">Camera sau</th>
                <td>48 MP (chính) + 12 MP (siêu rộng)</td>
              </tr>
              <tr>
                <th scope="row">Pin</th>
                <td>3.561 mAh, sạc nhanh 25W</td>
              </tr>
              <tr>
                <th scope="row">Hệ điều hành</th>
                <td>iOS 18</td>
              </tr>
            </tbody>
          </table>

        </section>
        <!-- /section thông số kỹ thuật -->


        <!-- ---------------------------------------------------
             KHU VỰC ĐÁNH GIÁ / BÌNH LUẬN
             <section> riêng vì reviews là một chủ đề độc lập.
             Bên trong, mỗi review dùng <article> vì mỗi bình luận
             là nội dung độc lập, có tác giả và thời gian riêng.
             --------------------------------------------------- -->
        <section aria-labelledby="reviews-heading">

          <h2 id="reviews-heading">Đánh giá từ khách hàng</h2>

          <!-- <article> cho từng review: có thể tồn tại độc lập,
               có tác giả (<address>) và thời gian (<time>) riêng -->
          <article>
            <h3>Sản phẩm tốt, giao hàng nhanh</h3>
            <!-- <address> biểu thị thông tin liên hệ/tác giả
                 trong ngữ cảnh của article này -->
            <address>Nguyễn Văn A</address>
            <!-- <time datetime> cung cấp timestamp machine-readable
                 cho crawler và AT -->
            <time datetime="2025-04-10">10 tháng 4, 2025</time>
            <p>Máy đẹp, hiệu năng mượt, pin dùng được cả ngày...</p>
          </article>

          <article>
            <h3>Hài lòng với camera</h3>
            <address>Trần Thị B</address>
            <time datetime="2025-04-08">8 tháng 4, 2025</time>
            <p>Camera chụp đêm cải thiện rõ rệt so với đời trước...</p>
          </article>

          <!-- Form viết bình luận mới -->
          <!-- <form> đúng nghĩa cho tập hợp input người dùng gửi lên server -->
          <form method="post" action="/reviews">
            <h3>Viết đánh giá của bạn</h3>

            <label for="review-title">Tiêu đề</label>
            <input id="review-title" type="text" name="title" required />

            <label for="review-body">Nội dung</label>
            <!-- <textarea> cho văn bản dài nhiều dòng, khác với <input> -->
            <textarea id="review-body" name="body" rows="4" required></textarea>

            <button type="submit">Gửi đánh giá</button>
          </form>

        </section>
        <!-- /section đánh giá -->

      </article>
      <!-- /article sản phẩm -->


      <!-- =====================================================
           SIDEBAR: SẢN PHẨM TƯƠNG TỰ
           <aside> vì đây là nội dung bổ sung, liên quan gián tiếp
           đến sản phẩm chính; landmark "complementary" trong AT.
           ===================================================== -->
      <aside aria-labelledby="related-heading">

        <h2 id="related-heading">Sản phẩm tương tự</h2>

        <!-- <ul> vì các sản phẩm gợi ý không có thứ tự ưu tiên bắt buộc -->
        <ul>

          <!-- Mỗi sản phẩm gợi ý dùng <li> > <article>:
               article vì mỗi card có thể đứng độc lập -->
          <li>
            <article>
              <a href="/iphone-15">
                <img src="" alt="iPhone 15" width="150" height="150" />
                <h3>iPhone 15</h3>
              </a>
              <p><strong>19.990.000 đ</strong></p>
            </article>
          </li>

          <li>
            <article>
              <a href="/samsung-galaxy-s25">
                <img src="" alt="Samsung Galaxy S25" width="150" height="150" />
                <h3>Samsung Galaxy S25</h3>
              </a>
              <p><strong>21.990.000 đ</strong></p>
            </article>
          </li>

          <li>
            <article>
              <a href="/pixel-9">
                <img src="" alt="Google Pixel 9" width="150" height="150" />
                <h3>Google Pixel 9</h3>
              </a>
              <p><strong>18.990.000 đ</strong></p>
            </article>
          </li>

        </ul>

      </aside>
      <!-- /aside sản phẩm tương tự -->

    </div>
    <!-- /div.layout-product-page (wrapper layout thuần túy, không có ngữ nghĩa) -->

  </main>
  <!-- /main -->


  <!-- =========================================================
       FOOTER
       <footer> vì đây là vùng thông tin cuối trang: bản quyền,
       liên kết phụ, địa chỉ công ty — landmark "contentinfo".
       ========================================================= -->
  <footer>

    <!-- <address> ở cấp document (ngoài article) biểu thị
         thông tin liên hệ của tổ chức/chủ sở hữu trang -->
    <address>
      Công ty TNHH Thương mại ABC — 123 Nguyễn Văn Linh, TP. HCM
    </address>

    <!-- <nav> thứ hai cho footer links; label phân biệt với nav header -->
    <nav aria-label="Điều hướng footer">
      <ul>
        <li><a href="/chinh-sach-bao-mat">Chính sách bảo mật</a></li>
        <li><a href="/dieu-khoan">Điều khoản sử dụng</a></li>
        <li><a href="/lien-he">Liên hệ</a></li>
      </ul>
    </nav>

    <!-- <small> đúng nghĩa cho chú thích bản quyền (fine print) -->
    <small>© 2025 ABC Shop. All rights reserved.</small>

  </footer>
  <!-- /footer -->

</body>
</html>


## Câu C2:
Phản hồi: trả lời Semantic HTML không phải "học thêm cho vui"
Quan điểm "dùng <div>cho mọi thứ" nghe có vẻ thực tế, nhưng thực tế đang đánh đổi chất lượng kỹ thuật thu được lợi ích ngắn hạn.
Về SEO , các công cụ tìm kiếm như Google không chỉ đọc nội dung — chúng đọc cấu trúc . Khi dùng <h1>, <article>, <nav>, crawler hiểu ngay đâu là tiêu đề chính, đâu là nội dung bài viết, đâu là điều hướng. Một trang bắt <div>buộc phải được tính toán, dẫn đến phân loại gần hơn so với tiêu chuẩn đánh dấu đối thủ sử dụng đúng.
Về Khả năng tiếp cận , đây mới là vấn đề nghiêm trọng hơn. Trình đọc màn hình như NVDA hay VoiceOver dựa hoàn toàn vào thẻ ngữ nghĩa để điều hướng. Người dùng nhấn phím tắt để nhảy thẳng đến <main>, <nav>, hay <button>— thứ thứ hai không thể thay đổi <div class="button">. Một <div>mặc định không có vai trò, không thể lấy tiêu điểm bằng bàn phím, không thể đọc đúng ngữ cảnh.
Ví dụ cụ thể: Thay <div class="nav">bằng <nav>, trình duyệt tự động hiển thị vai trò mốc "điều hướng" cho công nghệ hỗ trợ. Không cần thêm một dòng JavaScript hay ARIA nào — HTML ngữ nghĩa làm điều đó miễn phí.
Tuy nhiên , <div>vẫn có giải pháp hợp lý: khi cần một thùng chứa tinh chất để bố trí mà không mang ý nghĩa ngữ nghĩa nào — ví dụ một trình bao bọc flex/lưới để điều chỉnh các phần tử con. Lúc đó việc sử dụng <div>là hoàn toàn chính xác.
Kết luận: HTML ngữ nghĩa không phải "học thêm thẻ mới" — đó là nền tảng để sản phẩm hoạt động tốt cho mọi người dùng và mọi công cụ đọc trang web.