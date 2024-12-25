---
sidebar_position: 3
---

# Cookies

Cookies trong JavaScript là một cơ chế lưu trữ dữ liệu nhỏ được gửi và lưu trữ trong trình duyệt của người dùng. Chúng được sử dụng chủ yếu để duy trì trạng thái của người dùng trên các trang web, chẳng hạn như lưu trữ thông tin đăng nhập, ngôn ngữ, hoặc các tùy chọn của người dùng. Cookies có thể được đọc và sửa đổi bởi cả phía máy chủ và phía client (trình duyệt).

Các dữ liệu này được gửi từ máy chủ tới trình duyệt khi người dùng truy cập vào trang web, và sau đó được gửi lại máy chủ mỗi khi người dùng gửi yêu cầu (request) tiếp theo.

- Mỗi cookie bao gồm:
  - **Tên (Name)**: Định danh cookie.
  - **Giá trị (Value)**: Dữ liệu được lưu trữ trong cookie.
  - **Ngày hết hạn (Expires/Max-Age)**: Thời gian cookie còn hiệu lực. Nếu không có giá trị này, cookie sẽ chỉ tồn tại trong phiên duyệt web (session).
  - **Đường dẫn (Path)**: Định nghĩa phạm vi các URL mà cookie có thể được gửi tới.
  - **Miền (Domain)**: Chỉ định miền mà cookie có thể gửi đến.
  - **Chỉ thị bảo mật (Secure)**: Chỉ phép cookie được gửi qua giao thức HTTPS.
  - **HttpOnly**: Cookie không thể bị truy cập qua JavaScript, chỉ có thể truy cập thông qua HTTP request (để bảo mật hơn).
  - **SameSite**: Giới hạn cách thức mà cookie có thể được gửi theo các yêu cầu cross-site.

## Cách thức hoạt động của Cookies

Khi người dùng truy cập một trang web, máy chủ có thể gửi một cookie đến trình duyệt của người dùng.

Sau đó, khi người dùng gửi các yêu cầu tiếp theo đến máy chủ, trình duyệt sẽ tự động gửi các cookie đã lưu trữ cùng với yêu cầu đó.

Điều này cho phép máy chủ nhận diện người dùng và duy trì trạng thái (như thông tin đăng nhập, cài đặt, v.v.) giữa các phiên làm việc.

## Các phương thức làm việc với Cookies trong JavaScript

JavaScript cung cấp một API để làm việc với cookies qua đối tượng `document.cookie`. Tuy nhiên, thao tác với cookies trong JavaScript có một số hạn chế và không trực quan bằng việc sử dụng HTTP headers (gửi cookie qua máy chủ).

### Lấy thông tin cookie

Để lấy tất cả cookies của một trang web, bạn chỉ cần sử dụng `document.cookie`. Tuy nhiên, lưu ý rằng `document.cookie` sẽ trả về một chuỗi các cookies dưới dạng "key=value" nối liền nhau, phân tách bởi dấu chấm phẩy (`;`).

```js
console.log(document.cookie); // Ví dụ: "username=john_doe; theme=dark"
```

### Cấu trúc của một cookie

```js
document.cookie =
  "key=value; expires=expiration_date; path=path; domain=domain; secure; samesite=sameSite_value";
```

### Cài đặt cookie

```js
// Tạo một cookie với tên "username" và giá trị "john_doe"
document.cookie = "username=john_doe";

// Tạo một cookie với ngày hết hạn và đường dẫn
let expireDate = new Date();
expireDate.setMinutes(expireDate.getMinutes() + 30); // Cookie hết hạn sau 30 phút
document.cookie =
  "username=john_doe; expires=" + expireDate.toUTCString() + "; path=/";
```

### Xóa cookie

Để xóa một cookie, bạn chỉ cần thiết lập ngày hết hạn của cookie là một thời điểm trong quá khứ.

```js
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/";
```

> Lưu ý rằng khi xóa cookie, bạn phải chỉ định chính xác path của cookie đó. Nếu cookie được tạo ra với path=/, bạn cần chỉ định path=/ khi xóa.

## Các thuộc tính của Cookie

- **Expires/Max-Age**: Nếu không có thuộc tính này, cookie sẽ bị xóa khi phiên làm việc kết thúc (tức khi đóng trình duyệt). Nếu bạn chỉ định một expires cụ thể (thường là một ngày trong tương lai), cookie sẽ tồn tại cho đến thời điểm đó.

  - Ví dụ: expires=Fri, 31 Dec 2024 23:59:59 GMT.
  - Hoặc dùng Max-Age để chỉ định thời gian sống tính bằng giây. Ví dụ: max-age=3600 sẽ làm cookie tồn tại trong 1 giờ.

- **Path**: Tham số này xác định phạm vi URL mà cookie có thể được gửi đến. Nếu bạn chỉ định path=/, cookie sẽ được gửi cho tất cả các trang trong miền hiện tại. Nếu bạn chỉ định một đường dẫn cụ thể, cookie chỉ được gửi khi truy cập vào các trang có đường dẫn này.

- **Domain**: Chỉ định tên miền mà cookie có thể được truy cập từ. Thông thường, bạn không cần chỉ định thuộc tính này, trình duyệt sẽ mặc định là tên miền của trang web hiện tại.

- **Secure**: Nếu có thuộc tính secure, cookie chỉ được gửi qua giao thức HTTPS, giúp bảo vệ cookie khỏi việc bị đánh cắp trong quá trình truyền tải.

- **HttpOnly**: Khi có thuộc tính này, cookie chỉ có thể được truy cập bởi máy chủ và không thể bị JavaScript truy cập từ trình duyệt. Điều này giúp bảo vệ cookie khỏi các cuộc tấn công Cross-site Scripting (XSS).

- **SameSite**: Thuộc tính này giúp bảo vệ cookie khỏi các cuộc tấn công Cross-Site Request Forgery (CSRF). Có ba giá trị:

  - Strict: Cookie chỉ được gửi nếu yêu cầu được gửi từ cùng một miền.
  - Lax: Cookie chỉ được gửi trong các yêu cầu điều hướng an toàn (như GET).
  - None: Cookie có thể được gửi trong mọi yêu cầu, nhưng phải kết hợp với Secure nếu được sử dụng.

## Ưu điểm và Nhược điểm của Cookies

### Ưu điểm:

- **Giữ trạng thái**: Cookies giúp duy trì trạng thái của người dùng giữa các phiên làm việc, chẳng hạn như lưu trữ thông tin đăng nhập.
- **Lưu trữ ít dữ liệu**: Cookies là một cách tốt để lưu trữ các dữ liệu nhỏ (khoảng 4KB mỗi cookie).
- **Hỗ trợ từ cả phía máy chủ và client**: Cookies có thể được tạo và truy xuất cả từ phía máy chủ và trình duyệt của người dùng.

### Nhược điểm:

- **Dung lượng hạn chế**: Mỗi cookie có dung lượng giới hạn (khoảng 4KB), không thích hợp cho việc lưu trữ lượng lớn dữ liệu.
- **Tác động đến hiệu suất**: Cookies được gửi cùng với mỗi yêu cầu HTTP, có thể làm giảm hiệu suất của ứng dụng nếu lưu trữ quá nhiều cookie.
- **Vấn đề bảo mật**: Cookies có thể bị tấn công nếu không được cấu hình đúng, đặc biệt là khi không sử dụng Secure và HttpOnly.

## Lưu ý khi sử dụng Cookies

- **Bảo mật**: Đảm bảo rằng bạn sử dụng cookie với thuộc tính `Secure` và `HttpOnly` nếu bạn đang lưu trữ thông tin nhạy cảm.
- **Quản lý cookie**: Quản lý cookies hợp lý để tránh lưu trữ quá nhiều dữ liệu, gây ảnh hưởng đến hiệu suất.
- **Chú ý đến chính sách bảo mật**: Cẩn thận khi làm việc với cookies trong các ứng dụng yêu cầu bảo mật cao như giao dịch trực tuyến hoặc ứng dụng ngân hàng.
