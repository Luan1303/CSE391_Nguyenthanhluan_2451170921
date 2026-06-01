
PHẦN A — KIỂM TRA ĐỌC HIỂU
Câu A1: (Tài liệu: 07_forms_interactive.md)
1. type="text"
 → Ô nhập chữ 1 dòng → Không validation đặc biệt (chỉ theo required/minlength/maxlength nếu có) → Dùng nhập tên khách hàng / tên sản phẩm cần tìm

2. type="email"
 → Ô nhập text có dạng email → Tự kiểm tra có ký tự @ và đúng định dạng email → Dùng cho form đăng ký / đăng nhập tài khoản

3. type="password"
 → Ô nhập mật khẩu (hiện dấu •••) → Không tự kiểm tra độ mạnh, chỉ theo required/minlength → Dùng nhập mật khẩu khi đăng nhập

4. type="number"
 → Ô nhập số (có nút tăng/giảm) → Chỉ cho nhập số, có thể giới hạn min/max/step → Dùng nhập số lượng sản phẩm muốn mua

5. type="tel"
 → Ô nhập số điện thoại → Không tự check chuẩn 100%, có thể kết hợp pattern → Dùng nhập số điện thoại giao hàng

6. type="date"
 → Bộ chọn ngày (calendar) → Tự kiểm tra đúng định dạng ngày → Dùng chọn ngày sinh khi tạo tài khoản / ngày nhận hàng

7. type="time"
 → Bộ chọn giờ (hh:mm) → Tự kiểm tra định dạng thời gian → Dùng chọn giờ giao hàng mong muốn

8. type="file"
 → Nút chọn file từ máy tính → Có thể giới hạn loại file bằng accept → Dùng để upload ảnh đánh giá sản phẩm / gửi ảnh khiếu nại

9. type="checkbox"
 → Ô tick chọn (có thể chọn nhiều) → Không validation đặc biệt → Dùng chọn đồng ý điều khoản / chọn nhiều bộ lọc sản phẩm

10. type="radio"
 → Nút chọn 1 trong nhiều lựa chọn → Không validation đặc biệt → Dùng chọn phương thức thanh toán (COD, Momo, Visa...)

Câu A2: (Tài liệu: 07_forms_interactive.md)
Trường hợp 1
<input type="text" required value="">  
Dự đoán: Browser chặn submit bởi trường required trống. Thông báo validation kiểu "Please fill out this field".

Trường hợp 2
<input type="email" value="abc">        
Dự đoán: Browser chặn submit vì giá trị không đúng định dạng email, thông báo "Please enter an email address.".

Trường hợp 3
<input type="number" min="1" max="10" value="15"> 
Dự đoán: Browser chặn submit vì 15 vượt quá max=10, thông báo "Value must be less than or equal to 10.".

Trường hợp 4
<input type="text" pattern="[0-9]{10}" value="abc123"> 
Dự đoán: Browser chặn submit vì giá trị không khớp pattern 10 chữ số, thông báo "Please match the requested format.".

Trường hợp 5
<input type="password" minlength="8" value="123">  
Dự đoán: Browser chặn submit vì độ dài nhỏ hơn minlength 8, thông báo "Please lengthen this text to 8 characters or more.".

Kết quả thực tế: Khi submit form có cả 5 trường, browser dừng ở trường invalid đầu tiên (Case 1) và hiển thị cảnh báo required. Đây là hành vi validation của HTML5: kiểm tra tuần tự và ngăn submit nếu có trường invalid. Đã tạo file `validation_test.html` và chụp màn hình kết quả tại `screenshots/validation_test_submit.png`.

Câu A3: (Accessibility)
1. `<label for="email">` quan trọng cho screen reader vì nó tạo tên truy cập cho input và liên kết nhãn với control. Screen reader đọc label khi người dùng focus vào input, giúp người dùng khiếm thị hiểu mục đích của trường.
2. Dùng `<fieldset>` + `<legend>` khi nhóm nhiều control liên quan lại với nhau, ví dụ nhóm thông tin giao hàng hoặc lựa chọn phương thức thanh toán. Cụ thể:
   <fieldset>
       <legend>Thông tin giao hàng</legend>
       <label for="city">Thành phố</label>
       <select id="city" name="city">...</select>
       ...
   </fieldset>
   `fieldset` giúp bố cục rõ ràng và `legend` mô tả mục đích nhóm cho cả người nhìn và assistive technology.
3. `aria-label` dùng khi control không có nhãn văn bản nhìn thấy được, hoặc khi cần cung cấp tên truy cập duy nhất cho control không có `<label>`. Không nên dùng `aria-label` khi đã có `<label>` vì `<label>` đã cung cấp tên truy cập tự nhiên; dùng cả hai dễ gây trùng lặp, mâu thuẫn, hoặc làm screen reader đọc hai lần.

Câu A4: (Media)
1. `loading="lazy"` trên `<img>` làm trì hoãn tải ảnh đến khi ảnh gần xuất hiện trên màn hình, giảm thời gian tải trang và tiết kiệm băng thông. Không nên dùng cho ảnh quan trọng ở trên cùng trang (above-the-fold) vì ảnh đó cần tải ngay để hiển thị nhanh.
2. Nên cung cấp nhiều `<source>` trong `<video>` vì trình duyệt khác nhau hỗ trợ khác nhau; nhiều source giúp video phát được trên nhiều trình duyệt và thiết bị hơn. Ba format video web phổ biến: `video/mp4`, `video/webm`, `video/ogg`.
3. `alt` trên `<img>` dùng để mô tả nội dung hình ảnh cho screen reader và hiển thị khi ảnh không tải được. Ví dụ alt tốt:
   - Ảnh sản phẩm iPhone 16: `alt="iPhone 16 màu bạc, mặt trước và mặt sau"`
   - Ảnh trang trí (decorative): `alt=""`
   - Ảnh biểu đồ doanh thu Q1/2026: `alt="Biểu đồ cột doanh thu Q1/2026 theo tháng"`

Câu A5: (`<figure>` vs `<img>`)
- Cách 1 (`<img src="product.jpg" alt="iPhone">`) dùng khi ảnh là một phần nội dung đơn giản, không cần chú thích chi tiết. Ví dụ: ảnh thumbnail sản phẩm trên danh sách, logo cửa hàng, ảnh avatar người dùng.
- Cách 2 (`<figure> <img ...> <figcaption>...</figcaption> </figure>`) dùng khi ảnh cần chú thích hoặc giải thích thêm. Ví dụ: hình sản phẩm có giá và mô tả dưới ảnh trên trang chi tiết, hoặc hình minh họa biểu đồ kèm chú thích số liệu.

Ví dụ thực tế:
- `<img>`: ảnh thumbnail sản phẩm, logo thương hiệu, ảnh biểu tượng nút.
- `<img>`: avatar tài khoản, ảnh nền thanh toán, icon giao diện.
- `<figure>`: ảnh sản phẩm với `figcaption` ghi tên và giá, ảnh bộ sưu tập với chú thích mẫu, hình ảnh so sánh tính năng với chú thích giải thích.
- `<figure>`: biểu đồ doanh thu kèm caption, infographic kèm chú thích chi tiết.
`<figure>`: biểu đồ doanh thu kèm caption, infographic kèm chú thích chi tiết.

Bài B1: Form đăng ký tài khoản
HTML không thể kiểm tra (validate) trường "confirm password" chỉ bằng thuộc tính HTML vì các thuộc tính validation xử lý từng input riêng lẻ. HTML5 không có thuộc tính để so sánh trực tiếp giá trị của hai ô mật khẩu; do đó cần dùng JavaScript phía client để kiểm tra hai giá trị có khớp trước khi cho phép submit, và bắt buộc kiểm tra lại ở phía server (backend) để đảm bảo an toàn.

### Câu C1: Debug Form — 8 lỗi & sửa

Liệt kê lỗi theo format:

Lỗi 1: Input "Tên" không có `<label for="...">`, vi phạm accessibility.
Sửa: `<label for="name">Tên:</label> <input id="name" name="name" type="text" required>`

Lỗi 2: Input email chỉ có `placeholder` (placeholder chứa xuống dòng), thiếu `label`, `id`, `name`, và `required`.
Sửa: `<label for="email">Email:</label> <input id="email" name="email" type="email" placeholder="Email của bạn" required>`

Lỗi 3: Hai ô password không có `label`/`id`/`name` và không có cơ chế confirm-password.
Sửa: `<label for="pw">Mật khẩu:</label> <input id="pw" name="password" type="password" minlength="8" required>`
Sửa: `<label for="pw2">Nhập lại mật khẩu:</label> <input id="pw2" name="confirm_password" type="password" minlength="8" required>`
Ghi chú: cần JavaScript để so sánh `password` và `confirm_password` trước submit.

Lỗi 4: "Phone" dùng `type="text"` và thiếu `label`/`pattern` — có value mặc định không thích hợp.
Sửa: `<label for="phone">Phone:</label> <input id="phone" name="phone" type="tel" pattern="[0-9]{10}" placeholder="0901234567" required>`

Lỗi 5: `<select>` không có `label`, thiếu option mặc định (`value=""`) và các `<option>` không có `value` attribute.
Sửa: `<label for="city">Thành phố:</label> <select id="city" name="city" required> <option value="">Chọn thành phố</option> <option value="HN">Hà Nội</option> <option value="HCM">TP.HCM</option> </select>`

Lỗi 6: Checkbox "Tôi đồng ý" không liên kết đúng với input và thiếu `required`.
Sửa: `<label><input id="agree" name="agree" type="checkbox" required> Tôi đồng ý điều khoản</label>`

Lỗi 7: `<form>` thiếu `action` và `method` (best practice để xác định hành vi submit).
Sửa: `<form action="#" method="POST"> ... </form>`

Lỗi 8: Nhiều input thiếu `name` attribute => dữ liệu không gửi được cho server.
Sửa: Đảm bảo mọi input có `id` và `name` (ví dụ `name="email"`, `name="password"`, `name="phone"`).

### Câu C2: Thiết kế chiến lược Validation (Ngân hàng số)

1) Regex `pattern`:
- CMND/CCCD (12 chữ số): `pattern="^[0-9]{12}$"`
- Số tài khoản (10–15 chữ số): `pattern="^[0-9]{10,15}$"`

2) HTML5 validation đủ an toàn cho ứng dụng ngân hàng chưa?
Không. HTML5 validation chỉ là cơ chế client-side để cải thiện trải nghiệm người dùng; nó có thể bị bỏ qua (bằng cách gửi request trực tiếp hoặc tắt JS). Mọi kiểm tra quan trọng (tính hợp lệ, tính duy nhất, bảo mật) bắt buộc phải thực hiện ở phía server.

3) Ba loại validation mà HTML5 KHÔNG THỂ làm được (phải dùng JavaScript / server):
- So sánh cross-field (ví dụ: confirm password phải khớp password)
- Kiểm tra bất đồng bộ/tra cứu server (ví dụ: email hoặc tài khoản đã tồn tại)
- Kiểm tra logic nghiệp vụ/phức tạp (ví dụ: checksum, xác thực số thẻ, hạn mức, hoặc kiểm tra độ mạnh mật khẩu theo thuật toán riêng)

4) Hai rủi ro nếu chỉ validate trên frontend:
- Kẻ tấn công có thể bỏ qua validation client-side và gửi dữ liệu độc hại (SQL injection, XSS) tới server.
- Dữ liệu không hợp lệ hoặc trùng lặp (ví dụ: số CMND/CCCD giả, PIN yếu) có thể được chấp nhận, dẫn tới gian lận hoặc lộ thông tin.

