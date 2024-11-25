---
sidebar_position: 2
---

# While

Là vòng lặp khi số lần lặp không xác định trước, mà phụ thuộc và điều kiện.

```js
while (condition) {
  // Khối mã được thực thi
}
```

- condition: Là một biểu thức kiểm tra điều kiện, trả về giá trị Boolean (`true` hoặc `false`).
- Nếu condition là `true`, khối mã bên trong vòng lặp sẽ được thực thi.
- Khi condition là `false`, vòng lặp sẽ dừng lại.

```js
let count = 1;

while (count <= 5) {
  console.log(count);
  count++;
}
// 1, 2, 3, 4, 5
```

**Vòng lặp vô hạn (cần tránh)**

Nếu điều kiện luôn đúng, vòng lặp sẽ không bao giờ dừng, dẫn đến vòng lặp vô hạn. Điều này thường gây treo chương trình.

```js
let count = 0;
while (true) {
  console.log(count);
  count++;
  if (count > 5) break; // Sử dụng `break` để thoát khỏi vòng lặp
}
```
