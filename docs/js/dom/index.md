---
sidebar_position: 10
---

# DOM

`DOM (Document Object Model)` là một giao diện lập trình ứng dụng (API) giúp lập trình viên có thể tương tác với tài liệu HTML hoặc XML. DOM mô tả một trang web dưới dạng một cấu trúc cây, nơi mỗi phần tử HTML trong trang được biểu diễn như một node (điểm nút).

- Document (Tài liệu): Tức là tài liệu HTML hoặc XML mà DOM đang đại diện.
- Object (Đối tượng): Mỗi phần tử trong tài liệu được coi là một đối tượng có thể được truy cập và thao tác.

![ex1](./images/ex1.png)

## Cấu trúc của DOM

DOM coi một trang web là một "cây" (tree) với một đỉnh (root) là thẻ `<html>`, và các nút (node) khác là các thẻ HTML bên trong. Mỗi thẻ HTML như `<div>, <p>, <a>`, v.v... sẽ là một đối tượng (node) trong DOM.

```html
<html>
  <head>
    <title>Trang web</title>
  </head>
  <body>
    <h1>Chào mừng đến với trang web của tôi!</h1>
    <p>Đây là một đoạn văn bản.</p>
  </body>
</html>
```

Được biểu diễn trong DOM như một cây các đối tượng (nodes), trong đó `<html>, <head>, <body>, <h1>, và <p>` là các node.

## Các loại Node trong DOM

Trong DOM, mỗi phần tử trong trang HTML được biểu diễn dưới dạng một node, và có một số loại node cơ bản:

- `Element node`: Đây là những đối tượng đại diện cho các phần tử HTML (ví dụ: `<div>, <p>, <h1>`,...).
- `Text node`: Đại diện cho văn bản nằm bên trong các thẻ HTML. Ví dụ, văn bản trong thẻ `<h1>` là một Text node.
- `Comment node`: Đại diện cho các bình luận trong tài liệu, ví dụ: <!-- Đây là một bình luận -->.
- `Attribute node`: Đại diện cho các thuộc tính của thẻ HTML, ví dụ: class="main" hoặc id="header".

## Truy cập và Thao tác với DOM bằng JavaScript

JavaScript có thể truy cập và thay đổi DOM thông qua các phương thức của đối tượng document (đối tượng đại diện cho tài liệu HTML). Dưới đây là một số phương thức quan trọng:

### Truy cập phần tử

- `getElementById()`: Truy cập phần tử dựa trên id của nó.
- `getElementsByClassName()`: Truy cập tất cả các phần tử có một lớp (class) cụ thể.
- `getElementsByTagName()`: Truy cập tất cả các phần tử có một tên thẻ cụ thể (ví dụ: tất cả thẻ `<p>`).
- `querySelector()`: Truy cập phần tử đầu tiên phù hợp với selector (giống như trong CSS).
- `querySelectorAll()`: Truy cập tất cả các phần tử phù hợp với selector.

```js
// Truy cập phần tử theo ID
let header = document.getElementById("header");

// Truy cập tất cả các phần tử có class="item"
let items = document.getElementsByClassName("item");

// Truy cập phần tử đầu tiên với thẻ <p>
let paragraph = document.querySelector("p");

// Truy cập tất cả các thẻ <p>
let paragraphs = document.querySelectorAll("p");
```

### Thay đổi nội dung

- `innerHTML`: Thay đổi nội dung HTML của một phần tử.
- `textContent`: Thay đổi nội dung văn bản của một phần tử (không bao gồm HTML).

```js
// Thay đổi nội dung văn bản
let header = document.getElementById("header");
header.textContent = "Nội dung mới";

// Thay đổi HTML bên trong một phần tử
let div = document.getElementById("content");
div.innerHTML = "<p>Đoạn văn mới</p>";
```

### Thêm, Xóa, và Sửa đổi các phần tử

- `createElement()`: Tạo một phần tử mới.
- `appendChild()`: Thêm một phần tử con vào phần tử khác.
- `removeChild()`: Xóa một phần tử con khỏi phần tử khác.
- `replaceChild()`: Thay thế một phần tử con bằng một phần tử khác.

```js
// Tạo một phần tử mới
let newParagraph = document.createElement("p");
newParagraph.textContent = "Đoạn văn mới";

// Thêm phần tử mới vào cuối phần tử body
document.body.appendChild(newParagraph);

// Xóa phần tử mới vừa thêm
document.body.removeChild(newParagraph);
```

## Xử lý sự kiện với DOM

Một trong những tính năng quan trọng của DOM là khả năng xử lý sự kiện (events).

Có thể lắng nghe các sự kiện như nhấp chuột, di chuột, nhập liệu, v.v...

- `addEventListener()`: Phương thức này giúp thêm một trình xử lý sự kiện (event handler) vào một phần tử.

```js
// Lắng nghe sự kiện click trên một nút
let button = document.getElementById("myButton");
button.addEventListener("click", function () {
  alert("Bạn đã nhấn nút!");
});
```

## DOM và Render Trang Web

DOM là yếu tố quan trọng trong việc làm cho trang web có thể thay đổi nội dung mà không cần tải lại trang.

Khi một phần tử trong DOM được thay đổi, trình duyệt sẽ tự động cập nhật và render lại phần đó mà không phải tải lại toàn bộ trang. Điều này giúp cải thiện hiệu suất và trải nghiệm người dùng
