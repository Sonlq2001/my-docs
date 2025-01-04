---
sidebar_position: 1
---

# Null and undefined

`JavaScript` có nhiều cách để biểu thị 1 giá trị không có.

`null` và `undefined` là 2 cách phổ biến nhất.

## null

- **Định nghĩa**

  - Từ khóa `null` thể hiện sự thiếu vắng giá trị được xác định có chủ ý.
  - Khác với `undefined`, `null` không được gán tự động mà phải được đặt một cách tường minh bởi lập trình viên.

- **Đặc điểm**

  - `null` là kiểu dữ liệu tham trị (`primitive`), mặc dù toán tử `typeof` trả về `null` là một `đối tượng`
  - Thường được sử dụng để khởi tạo một biến hoặc gán giá trị cho biến để chỉ rằng nó không có giá trị.

```js
let y = null;
console.log(y); // null

let obj = { prop: null };
console.log(obj.prop); // null
```

## undefined

- **Định nghĩa**
  - `undefined` là một giá trị đặc biệt được JavaScript tự động gán cho một biến khi:
    - Biến được khai báo nhưng chưa được gán giá trị.
    - Một hàm không trả về giá trị nào (hoặc không có từ khóa `return`).
    - Một thuộc tính không tồn tại trong đối tượng.
- **Đặc điểm**:
  - Là kiểu dữ liệu nguyên thủy (`primitive type`).
  - JavaScript tự động gán giá trị `undefined` trong các tình huống trên.

```js
let x; // Chưa gán giá trị
console.log(x); // undefined

function myFunction() {}
console.log(myFunction()); // undefined

let obj = {};
console.log(obj.nonExistentProp); // undefined
```

##  So sánh `null` và `undefined`

| **Đặc điểm**            | **`undefined`**                   | **`null`**                                    |
| ----------------------- | --------------------------------- | --------------------------------------------- |
| **Nguồn gốc**           | Do JavaScript tự động gán.        | Do lập trình viên tự gán.                     |
| **Ý nghĩa**             | "Chưa được gán giá trị."          | "Không có giá trị" hoặc "trống rỗng."         |
| **Kiểu dữ liệu**        | `undefined` (nguyên thủy).        | `object` (mặc dù là một giá trị nguyên thủy). |
| **So sánh nghiêm ngặt** | `undefined === undefined` (true). | `null === null` (true).                       |
| **So sánh lỏng lẻo**    | `undefined == null` (true).       | `undefined == null` (true).                   |

## Sử dụng trong thực tế

- **Khi nào dùng `null`?**

  - Khi muốn tường minh rằng một biến hoặc thuộc tính không có giá trị:

- **Khi nào gặp `undefined`?**

  - Khi bạn quên gán giá trị hoặc kiểm tra biến/thuộc tính chưa tồn tại.
