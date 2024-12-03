---
sidebar_position: 3
---

# HTTP request methods

`HTTP Request Methods` (Phương thức yêu cầu HTTP) là các phương thức mà các ứng dụng hoặc máy khách (client) sử dụng để yêu cầu dịch vụ từ một máy chủ (server) thông qua giao thức `HTTP (Hypertext Transfer Protocol)`.

Mỗi phương thức HTTP chỉ định một hành động mà máy khách muốn thực hiện trên tài nguyên (resource) mà máy chủ đang quản lý.

Các phương thức HTTP phổ biến nhất:

- `GET`
- `POST`
- `PUT`
- `DELETE`
- `PATCH`
- `HEAD`
- `OPTIONS`

## GET

- `Mục đích`: Lấy dữ liệu từ máy chủ.
- `Cách sử dụng`: Phương thức này chỉ yêu cầu máy chủ trả về một tài nguyên (như trang web, ảnh, dữ liệu JSON, v.v.) mà không thay đổi bất kỳ thông tin nào trên máy chủ.
- `Đặc điểm`
  - Không có tác dụng phụ (được gọi là `idempotent`, có nghĩa là thực hiện yêu cầu nhiều lần vẫn cho kết quả như nhau).
  - Dữ liệu yêu cầu thường được gửi qua URL (vì vậy có thể có giới hạn về độ dài URL).

## POST

- `Mục đích`: Gửi dữ liệu đến máy chủ để tạo mới hoặc cập nhật tài nguyên.
- `Cách sử dụng`: Phương thức này thường được dùng để gửi dữ liệu từ form trong trang web, hoặc khi tạo tài nguyên mới trên máy chủ.
- `Đặc điểm`
  - Dữ liệu gửi đi thường nằm trong phần thân của yêu cầu (body).
  - Có thể tạo hoặc thay đổi tài nguyên trên máy chủ.
  - Không có giới hạn độ dài dữ liệu.

## PUT

- `Mục đích`: Cập nhật hoặc thay thế tài nguyên hiện có trên máy chủ.
- `Cách sử dụng`: Phương thức này được dùng khi bạn muốn cập nhật một tài nguyên cụ thể, thay thế hoàn toàn tài nguyên hiện tại.
- `Đặc điểm`
  - Nếu tài nguyên đã tồn tại, nó sẽ được thay thế hoàn toàn.
  - Dữ liệu gửi đi cũng nằm trong phần thân của yêu cầu (body).

## DELETE

- `Mục đích`: Xóa tài nguyên khỏi máy chủ.
- `Cách sử dụng`: Phương thức này được dùng khi bạn muốn xóa tài nguyên trên máy chủ.
- `Đặc điểm`
  - Khi thực hiện xóa một tài nguyên, yêu cầu sẽ xóa tài nguyên đó trên máy chủ.
  - Thường không có phần thân yêu cầu.

## PATCH

- `Mục đích`: Cập nhật một phần tài nguyên (chỉ thay đổi một số thuộc tính của tài nguyên, không thay thế toàn bộ).
- `Cách sử dụng`: Phương thức này thường được dùng khi bạn chỉ muốn cập nhật một phần nhỏ của tài nguyên, thay vì thay thế toàn bộ tài nguyên như với phương thức PUT.
- `Đặc điểm`
  - Thường chỉ thay đổi một số thuộc tính thay vì toàn bộ tài nguyên.

## HEAD

- `Mục đích`: Lấy thông tin về tài nguyên mà không nhận dữ liệu nội dung (chỉ nhận phần header).
- `Cách sử dụng`: Phương thức này tương tự như GET, nhưng chỉ yêu cầu phần header (thông tin về tài nguyên) mà không nhận dữ liệu thực tế từ tài nguyên đó.
- `Đặc điểm`
  - Không có phần thân yêu cầu hoặc phản hồi.
  - Thường dùng để kiểm tra sự tồn tại của tài nguyên mà không tải dữ liệu.

## OPTIONS

- `Mục đích`: Kiểm tra các phương thức HTTP được hỗ trợ cho một tài nguyên.
- `Cách sử dụng`: Phương thức này yêu cầu máy chủ trả về các phương thức HTTP mà nó hỗ trợ cho tài nguyên (ví dụ như GET, POST, PUT, v.v.).
- `Đặc điểm`
  - Thường dùng để kiểm tra tính khả dụng của tài nguyên mà không thực hiện hành động nào với nó.

| Phương thức | Mục đích                                                  | Cập nhật dữ liệu | Cách gửi dữ liệu |
| ----------- | --------------------------------------------------------- | ---------------- | ---------------- |
| GET         | Lấy dữ liệu từ máy chủ                                    | Không            | URL              |
| POST        | Gửi dữ liệu để tạo tài nguyên mới                         | Có               | Body             |
| PUT         | Cập nhật hoặc thay thế toàn bộ tài nguyên                 | Có               | Body             |
| DELETE      | Xóa tài nguyên khỏi máy chủ                               | Không            | Không có Body    |
| PATCH       | Cập nhật một phần tài nguyên (không thay thế toàn bộ)     | Có               | Body             |
| HEAD        | Lấy header thông tin của tài nguyên mà không tải nội dung | Không            | Không có Body    |
| OPTIONS     | Kiểm tra phương thức HTTP được hỗ trợ cho một tài nguyên  | Không            | Không có Body    |
