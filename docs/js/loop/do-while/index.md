---
sidebar_position: 3
---

# Do while

Là một loại vòng lặp kiểm tra điều kiện sau khi thực hiện khối mã.
Điều này có nghĩa là khối mã trong vòng lặp `do...while` luôn được thực thi ít nhất một lần, bất kể điều kiện ban đầu đúng hay sai.

```js
do {
  // Khối mã được thực thi
} while (condition);
```

- condition: Là một biểu thức kiểm tra điều kiện. Nếu trả về true, vòng lặp sẽ tiếp tục. Nếu false, vòng lặp dừng lại.
- Khối mã trong do: Sẽ được thực thi trước khi kiểm tra điều kiện.

```js
let count = 10;
do {
  console.log(count);
  count++;
} while (count < 5);

// Mặc dù điều kiện sai nhưng vẫn sẽ hiện thị console.log = 10 trước khi kiểm tra điều kiện.
```

**Khi nào nên dùng `do...while`?**

- Khi bạn muốn đảm bảo rằng khối mã luôn được thực thi ít nhất một lần trước khi kiểm tra điều kiện.
- Trong các tình huống như nhập dữ liệu từ người dùng, nơi bạn cần kiểm tra điều kiện sau khi thực hiện hành động:
