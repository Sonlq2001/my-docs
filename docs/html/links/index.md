# Links

Thẻ liên kết link `<a>`

```html title="Example"
<a href="">Link</a>
```

## Href attribute

Mặc dù không bắt buộc nhưng thuộc tính href được tìm thấy trong hầu hết các thẻ `<a>`.

Thuộc tính `href` được sử dụng để tạo siêu liên kết đến các vị trí trong trang hiện tại, các trang khác trong một trang hoặc các trang khác. Nó cũng có thể được `mã hóa` để `tải xuống` các tệp hoặc `gửi email` đến một địa chỉ cụ thể, thậm chí bao gồm chủ đề và nội dung nội dung email được đề xuất.

```html title="Example"
<a href="https://machinelearningworkshop.com">Machine Learning Workshop</a>
<!-- tạo 1 link có siêu liên kết -->

<a href="#teachers">Our teachers</a>
<!-- tạo định danh liên kết đến phần tử có id="teachers" -->

<a href="https://machinelearningworkshop.com#teachers">MLW teachers</a>
<!-- tạo siêu liên kết "https://machinelearningworkshop.com" và liên kết đến phần tử có id="teachers" -->

<a href="mailto:hal9000@machinelearningworkshop.com">Email Hal</a>
<!-- tạo liên kết gửi mail -->

<a href="tel:8005551212">Call Hal</a>
<!-- tạo liên kết thực hiện cuộc gọi -->
```

## Status link

Thẻ `<a>` gồm 4 trạng thái:

- `link`: Đây là trạng thái mặc định của một liên kết khi nó chưa được truy cập. Thông thường, các trình duyệt sẽ hiển thị liên kết này dưới dạng văn bản màu xanh lam.
- `active`: Trạng thái này xảy ra khi người dùng nhấn chuột xuống trên liên kết, nhưng trước khi nhả chuột. Thường được dùng để thay đổi màu sắc hoặc kiểu dáng của liên kết khi nhấn vào.
- `hover`: Trạng thái này xảy ra khi người dùng di chuyển con trỏ chuột qua liên kết. Thông thường, các trang web thay đổi kiểu của liên kết khi ở trạng thái hover để tạo hiệu ứng khi người dùng tương tác.
- `visited`: Trạng thái này xảy ra khi người dùng đã truy cập vào liên kết. Các trình duyệt thường thay đổi màu của liên kết đã truy cập để phân biệt với các liên kết chưa được truy cập.

## Downloadable resources

Thuộc tính `download` phải được đưa vào khi href `trỏ đến tài nguyên có thể tải xuống`.

Giá trị của thuộc tính `download` là tên tệp được đề xuất cho tài nguyên sẽ được lưu trong hệ thống tệp cục bộ của người dùng.

`download="myFileDownload"`

```html title="Example"
<a
  href="blob:https://jakearchibald.github.io/944a5fc8-fdb3-458a-91ee-cdd5964b6646"
  download="hal.svg"
></a>
```

## Browsing context

Thuộc tính `target` cho phép xác định ngữ cảnh duyệt để điều hướng liên kết.

- `_self`: mặc định, là mở liên kết trong tab hiện tại.
- `_blank`: mở liên kết trong 1 tab mới.
- `_parent`: mở tài liệu được liên kết trong khung cha.
- `_top`: mở liên kết trong toàn bộ nội dung của cửa sổ.
- `framename`: mở tài liệu được liên kết trong iframe được đặt tên.
