---
sidebar_position: 2
---

# Recursion

Đệ quy (recursion) là một kỹ thuật lập trình mà một hàm gọi lại chính nó bên trong định nghĩa của nó. Nói cách khác, một hàm đệ quy là một hàm tự gọi lại mình, tạo thành một chuỗi các cuộc gọi hàm lồng nhau.

> Hàm đệ quy thường sử dụng một điều kiện dừng để ngừng gọi chính nó, tránh việc lặp lại vô hạn.

**Một hàm đệ quy thường có hai phần chính**

- Điều kiện dừng (Base Case): Là trường hợp khi hàm không gọi lại chính nó nữa. Điều kiện dừng giúp tránh tình trạng gọi đệ quy vô hạn.
- Câu lệnh đệ quy (Recursive Case): Là phần gọi lại chính hàm trong một cách khác để tiếp tục giải quyết bài toán cho đến khi gặp điều kiện dừng.

**Ưu điểm**

- Giúp giải quyết các bài toán phức tạp một cách đơn giản và dễ hiểu, đặc biệt với những bài toán có cấu trúc phân chia (chia để trị).
- Đặc biệt hữu ích khi giải quyết các bài toán đệ quy tự nhiên như sắp xếp, tìm kiếm, hoặc tính toán số Fibonacci.

**Nhược điểm**

- Đệ quy có thể gây ra việc sử dụng bộ nhớ lớn do phải lưu trữ các trạng thái của từng cuộc gọi hàm.
- Trong một số trường hợp, đệ quy có thể gây ra lỗi tràn ngăn xếp (stack overflow) nếu không có điều kiện dừng chính xác hoặc bài toán yêu cầu quá nhiều bước đệ quy.

## Example

**Tính giai thừa (`Factorial`)**

Giai thừa của một số `n` (ký hiệu là `n!`) là tích của tất cả các số nguyên dương từ `1` đến `n`

```
4! = 4 x 3 x 2 x 1 = 24
```

Hàm đệ quy tính giai thừa có thể được định nghĩa như sau:

```js
function factorial(n) {
  // Điều kiện dừng: nếu n là 0 hoặc 1, giai thừa bằng 1
  if (n === 0 || n === 1) {
    return 1;
  }
  // Câu lệnh đệ quy: gọi lại hàm factorial với n-1
  return n * factorial(n - 1);
}

console.log(factorial(5)); // Output: 120
```

**Giải thích**

- `Điều kiện dừng`: Khi n bằng 0 hoặc 1, hàm trả về 1. Đây là điểm dừng của đệ quy.
- `Câu lệnh đệ quy`: Hàm gọi lại chính nó với giá trị n - 1 cho đến khi điều kiện dừng được thỏa mãn.

Quá trình thực hiện của factorial(5) như sau:

```js
factorial(5) → 5 * factorial(4)
factorial(4) → 4 * factorial(3)
factorial(3) → 3 * factorial(2)
factorial(2) → 2 * factorial(1)
factorial(1) → 1  (Điều kiện dừng)
```
