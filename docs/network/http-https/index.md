---
sidebar_position: 2
---

# Http and Https

HTTP (HyperText Transfer Protocol) và HTTPS (HyperText Transfer Protocol Secure) đều là các giao thức (protocol) dùng để truyền tải dữ liệu trên Internet, nhưng có sự khác biệt quan trọng về bảo mật.

## HTTP (HyperText Transfer Protocol)

**`Định nghĩa`**

- HTTP là giao thức dùng để truyền tải dữ liệu giữa trình duyệt web và máy chủ web.
- Khi bạn truy cập một trang web, trình duyệt của bạn gửi yêu cầu HTTP tới máy chủ, và máy chủ phản hồi với dữ liệu của trang web đó.

**`Đặc điểm`**

- Không mã hóa: Dữ liệu được truyền tải qua HTTP là dạng văn bản thuần túy và không được mã hóa, nghĩa là nếu ai đó có thể "nghe lén" kết nối (tấn công man-in-the-middle), họ có thể đọc được nội dung của các yêu cầu và phản hồi.
- Dễ bị tấn công: Vì không có mã hóa, HTTP dễ bị tấn công qua các phương thức như nghe lén hoặc thay đổi dữ liệu trong quá trình truyền tải.

> URL của một trang web sử dụng HTTP có dạng `http://example.com`

## Https

**`Định nghĩa`**

- HTTPS là phiên bản bảo mật của HTTP. Nó sử dụng mã hóa `SSL/TLS` để bảo vệ dữ liệu khi truyền tải giữa máy khách (trình duyệt) và máy chủ.

**`Đặc điểm`**

- `Mã hóa`: HTTPS sử dụng mã hóa mạnh mẽ để bảo vệ dữ liệu khi truyền tải. Điều này có nghĩa là ngay cả khi ai đó có thể truy cập vào kết nối mạng giữa bạn và máy chủ (ví dụ: kẻ tấn công ở cùng mạng Wi-Fi), họ cũng không thể đọc được thông tin vì dữ liệu được mã hóa.
- `Xác thực máy chủ`: Với HTTPS, bạn có thể chắc chắn rằng bạn đang giao tiếp với đúng máy chủ. Điều này giúp ngăn ngừa các cuộc tấn công giả mạo (phishing).
- `Tính toàn vẹn của dữ liệu`: SSL/TLS bảo đảm rằng dữ liệu không bị thay đổi trong quá trình truyền tải. Nếu dữ liệu bị thay đổi, kết nối sẽ bị ngắt và người dùng sẽ được thông báo.

> URL của một trang web sử dụng HTTPS có dạng `https://example.com`

**`Nên sử dụng HTTPS`**

- `Bảo mật thông tin người dùng`: HTTPS giúp bảo vệ các thông tin nhạy cảm như mật khẩu, thông tin thẻ tín dụng, thông tin cá nhân, khỏi các cuộc tấn công.
- `Tăng độ tin cậy`: Các trang web sử dụng HTTPS thường được xem là đáng tin cậy hơn trong mắt người dùng, vì họ cảm thấy an toàn khi giao tiếp với trang web đó.
- `SEO (Tối ưu hóa công cụ tìm kiếm)`: Google và các công cụ tìm kiếm khác ưu tiên các trang web sử dụng HTTPS trong kết quả tìm kiếm, vì vậy sử dụng HTTPS có thể giúp cải thiện xếp hạng của trang web.
- `Ngăn chặn các cuộc tấn công man-in-the-middle`: HTTPS giúp ngăn ngừa việc kẻ tấn công giả mạo máy chủ và can thiệp vào dữ liệu người dùng.

## Compare

| Tiêu chí | HTTP                                                                          | HTTPS                                                                     |
| -------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| Bảo mật  | Không bảo mật (không mã hóa)                                                  | Bảo mật (mã hóa SSL/TLS)                                                  |
| Mã hóa   | Không có mã hóa dữ liệu                                                       | Dữ liệu được mã hóa                                                       |
| Xác thực | Không xác thực máy chủ                                                        | Xác thực máy chủ qua chứng chỉ SSL/TLS                                    |
| Tốc độ   | Nhanh hơn, vì không có mã hóa                                                 | Chậm hơn một chút vì có mã hóa                                            |
| Sử dụng  | Thích hợp cho các trang không yêu cầu bảo mật (như blog, thông tin công khai) | Phù hợp với các trang yêu cầu bảo mật cao (ngân hàng, mua sắm trực tuyến) |
