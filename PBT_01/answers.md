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
