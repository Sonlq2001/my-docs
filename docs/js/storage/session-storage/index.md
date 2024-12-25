---
sidebar_position: 2
---

# Session storage

**Session Storage** là một phần của **Web Storage API** trong JavaScript, tương tự như **Local Storage**, nhưng có sự khác biệt quan trọng về thời gian lưu trữ và phạm vi sử dụng. Dữ liệu được lưu trữ trong **Session Storage** sẽ chỉ tồn tại trong phiên làm việc (session) của trình duyệt và sẽ bị xóa khi người dùng đóng cửa sổ hoặc tab của trình duyệt. Điều này làm cho **Session Storage** phù hợp cho việc lưu trữ dữ liệu tạm thời trong quá trình tương tác với một trang web.

## Đặc điểm của Session Storage

- **Lưu trữ tạm thời**: Dữ liệu trong sessionStorage chỉ tồn tại trong một phiên làm việc của trình duyệt (trong một tab hoặc cửa sổ). Khi người dùng đóng cửa sổ hoặc tab, dữ liệu sẽ bị xóa.
- **Phạm vi của sessionStorage**: Dữ liệu trong sessionStorage chỉ có sẵn trong cùng một tab hoặc cửa sổ trình duyệt. Nếu người dùng mở một tab hoặc cửa sổ mới và truy cập vào trang web, dữ liệu sẽ không được chia sẻ.
- **Dung lượng giới hạn**: Dung lượng của sessionStorage cũng tương tự như localStorage, thường là khoảng 5MB, tùy thuộc vào trình duyệt.
- **Dữ liệu dạng key-value**: Giống như localStorage, sessionStorage lưu trữ dữ liệu dưới dạng các cặp khóa (key) và giá trị (value), nhưng dữ liệu này sẽ chỉ tồn tại trong phạm vi của session hiện tại.

## Các phương thức chính của Session Storage

Session Storage cung cấp các phương thức rất giống với **Local Storage** để bạn có thể lưu trữ, truy xuất, và xóa dữ liệu.

### `sessionStorage.setItem(key, value)`

Phương thức này được sử dụng để lưu trữ dữ liệu vào sessionStorage. Tham số `key` là tên của khóa (một chuỗi), và `value` là giá trị bạn muốn lưu trữ (cũng phải là chuỗi).

```js
sessionStorage.setItem("username", "john_doe");
sessionStorage.setItem("age", "25");
```

### `sessionStorage.getItem(key)`

Phương thức này được sử dụng để lấy giá trị từ sessionStorage dựa trên khóa (key). Nếu khóa không tồn tại, phương thức sẽ trả về `null`.

```js
let username = sessionStorage.getItem("username");
console.log(username); // "john_doe"
```

### `sessionStorage.removeItem(key)`

Phương thức này dùng để xóa một mục (key-value pair) trong sessionStorage dựa trên khóa (`key`).

```js
sessionStorage.removeItem("username");
```

### `sessionStorage.clear()`

Phương thức này xóa tất cả các mục trong sessionStorage, không cần chỉ định khóa.

```js
sessionStorage.clear();
```

### `sessionStorage.length`

Thuộc tính này trả về số lượng các mục (key-value pairs) trong sessionStorage.

```js
console.log(sessionStorage.length);
```

### `sessionStorage.key(index)`

Phương thức này trả về khóa (key) tại chỉ mục nhất định. Chỉ mục được truyền vào là một số (index).

```js
let firstKey = sessionStorage.key(0);
console.log(firstKey); // Khóa của mục đầu tiên
```

## Lưu trữ các kiểu dữ liệu phức tạp

- Sử dụng `JSON.stringyfi` để truyển đổi sang chuỗi trước khi lưu và localStorage.
- Sử dụng `JSON.parse` để truyển đổi từ chuỗi sang kiểu dữ liệu thật của giá trị.

```js
// Lưu đối tượng trong sessionStorage
let user = {
  name: "John Doe",
  age: 30,
};

sessionStorage.setItem("user", JSON.stringify(user));

// Lấy đối tượng từ sessionStorage
let storedUser = JSON.parse(sessionStorage.getItem("user"));
console.log(storedUser.name); // "John Doe"
```

## Ưu điểm và Nhược điểm của Session Storage

### Ưu điểm:

- **Lưu trữ tạm thời**: Session Storage rất hữu ích khi bạn cần lưu trữ thông tin trong một phiên duyệt web, chẳng hạn như khi người dùng đang điều hướng giữa các trang trong cùng một ứng dụng.
- **Không cần kết nối mạng**: Tương tự như Local Storage, Session Storage hoạt động hoàn toàn trong trình duyệt mà không cần kết nối với server, giúp giảm tải cho server.
- **Không bị mất khi tải lại trang**: Dữ liệu vẫn tồn tại trong suốt phiên duyệt web, kể cả khi người dùng tải lại trang.

### Nhược điểm:

- **Không lưu trữ lâu dài**: Dữ liệu sẽ bị xóa khi người dùng đóng tab hoặc cửa sổ trình duyệt, vì vậy nó không thích hợp để lưu trữ thông tin lâu dài.
- **Không chia sẻ giữa các tab**: Dữ liệu trong sessionStorage chỉ có sẵn trong tab hoặc cửa sổ trình duyệt hiện tại. Nếu người dùng mở một tab mới và truy cập vào trang web, dữ liệu sẽ không được chia sẻ.
- **Giới hạn dung lượng**: Session Storage có dung lượng lưu trữ tương đối hạn chế (thường khoảng 5MB), vì vậy không nên sử dụng để lưu trữ quá nhiều dữ liệu.

## Lưu ý khi sử dụng Session Storage

- **Không lưu trữ thông tin nhạy cảm**: Mặc dù Session Storage chỉ tồn tại trong phiên duyệt web, nhưng cũng không nên lưu trữ thông tin nhạy cảm như mật khẩu hay thông tin thanh toán trong sessionStorage vì dữ liệu này có thể bị truy cập từ bất kỳ mã JavaScript nào chạy trên trang web.
- **Dữ liệu chỉ tồn tại trong phiên làm việc**: Đảm bảo rằng dữ liệu bạn lưu trữ trong sessionStorage là tạm thời và sẽ không cần thiết sau khi người dùng kết thúc phiên duyệt web.
- **Phạm vi giới hạn trong một tab**: Nếu bạn cần dữ liệu được chia sẻ giữa các tab hoặc cửa sổ trình duyệt, bạn nên sử dụng Local Storage hoặc các cơ chế khác (như cookies hoặc IndexedDB).
