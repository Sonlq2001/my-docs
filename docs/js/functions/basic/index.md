---
sidebar_position: 1
---

# Basic

Là khối câu lệnh, có thể tái sử dụng, dùng để thực hiện 1 tập hợp các tác vụ liên quan.

Hàm được coi như là 1 đối tượng, có thể được sử dụng trong tất cả các ngữ cảnh giống như bất kì đối tượng trong JS nào khác.

```js
function myFunction() {
  console.log("This is my function.");
}
```

> Hàm trong 1 đối tượng `class` được gọi là `phương thức`.

## Function declarations

Khai báo hàm bao gồm từ khóa hàm `function`, theo sau là mã định danh, danh sách các tham số được phân tách bằng dấu phẩy được đặt trong dấu ngoặc đơn và một câu lệnh khối được gọi là "nội dung hàm".

```js
function myFunction() {
  console.log("This is my function.");
}
```

**Có thể thực hiện gọi hàm trước khi hàm được khai báo**

Hành vi giống như cơ chế `Hoisting` của từ khóa khai báo biến `var`

```js
myFunction();

function myFunction() {
  console.log("This is my function.");
}

// gọi hàm xong mới khai báo hàm, kết quả vẫn được hiển thị
```

:::warning[Chú ý]
Phạm vi của hàm cũng chỉ được gọi trong `block scope`
:::

```js
{
  function myFunction() {
    console.log("This is my function.");
  }
}

myFunction(); // error
```

## Function calling

Sử dụng `tên định danh hàm` và dấu ngoặc tròn `()` để thực hiện gọi hàm.

```js
myFunction();
```

Các giá trị nhận được bên trong hàm được gọi là `tham số`, đóng vai trò giữ chỗ.

Các giá trị trong dấu ngoặc đơn khi hàm được gọi là `đối số`

```js
function myLog(message) {
  // message ở đây được gọi là "tham số"
  console.log(message);
}
myLog("hello world"); // giá trị truyền vào gọi là "đối số", ở đây là "hello world"
```

## Default value

Có thể gán giá trị mặc định cho `tham số` của hàm

- Trường hợp không truyền `đối số`, sẽ lấy giá trị mặc định.
- Trường hợp có truyền `đối số`, sẽ ưu tiên giá trị truyền vào.

```js
function myLog(message = "hello world") {
  console.log(message);
}
myLog(); // hello world
myLog("developer"); // developer
```
