# Restful api

`RESTful` API là một tiêu chuẩn dùng trong việc thiết kế API cho các ứng dụng web (thiết kế Web services) để tiện cho việc quản lý các resource.

Nó chú trọng vào tài nguyên hệ thống (tệp văn bản, ảnh, âm thanh, video, hoặc dữ liệu động…), bao gồm các trạng thái tài nguyên được định dạng và được truyền tải qua HTTP.

**Các khái niệm cơ bản trong RESTful API**

- `Tài nguyên (Resource)`: Mọi thứ mà API quản lý đều được coi là một tài nguyên (ví dụ: người dùng, sản phẩm, bài viết). Mỗi tài nguyên được đại diện bởi một URL duy nhất.
- `Phương thức HTTP`: RESTful API sử dụng các phương thức HTTP như GET, POST, PUT, DELETE để tương tác với tài nguyên.
- `Trạng thái (Status)`: Sau khi thực hiện một yêu cầu, server sẽ trả về một mã trạng thái HTTP (ví dụ: 200 OK, 404 Not Found) để cho biết kết quả của yêu cầu.
- `Dữ liệu (Data)`: Dữ liệu được truyền đi dưới dạng các định dạng như `JSON` hoặc `XML`.

```
Giả sử chúng ta có một API quản lý danh sách sách. Các yêu cầu có thể như sau:

GET /books: Lấy danh sách tất cả các sách.
GET /books/123: Lấy thông tin chi tiết của sách có ID là 123.
POST /books: Tạo một cuốn sách mới.
PUT /books/123: Cập nhật thông tin của sách có ID là 123.
DELETE /books/123: Xóa sách có ID là 123.
```

## How the RESTful API works

![restful-api](../../images/rest-api.png)

## Advantage / Disadvantages

**Ưu điểm**

- Đơn giản và dễ hiểu: RESTful API sử dụng các phương thức HTTP quen thuộc và các nguyên lý rõ ràng, dễ dàng tiếp cận.
- Dễ dàng mở rộng và bảo trì: Với kiến trúc phân tách client và server, việc thay đổi một bên không ảnh hưởng đến bên còn lại.
- Tính linh hoạt: Các client có thể dễ dàng tương tác với API mà không cần phải biết về cách thức xử lý của server.
- Hiệu suất cao: Tận dụng các giao thức HTTP.

**Nhược điểm**

- Có thể phức tạp khi thiết kế: Cần thiết kế cẩn thận để đảm bảo tính nhất quán và hiệu quả.
- Không phù hợp với tất cả các trường hợp: Có một số loại ứng dụng phức tạp hơn có thể yêu cầu các giao thức khác.
