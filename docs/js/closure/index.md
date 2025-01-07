---
sidebar_position: 17
title: "Closure"
---

Là 1 hàm có thể ghi nhớ nơi nó được tạo ra và có thể truy cập được biến ở phạm vi bên ngoài.

> Bản thân khi tạo ra 1 hàm, trong thân hàm đã có thể truy cập được bên trong và bên ngoài phạm vi của hàm rồi.

## Mục đích

- **Tạo các biến riêng tư:** Closure cho phép chúng ta tạo các biến riêng tư, không thể truy cập trực tiếp từ bên ngoài. Điều này giúp bảo vệ dữ liệu và tạo ra các module độc lập.
- **Tạo các hàm tự thực thi:** Closure được sử dụng để tạo các hàm tự thực thi (IIFE), giúp chúng ta kiểm soát phạm vi và tránh ô nhiễm không gian tên toàn cục.
- **Tạo các hàm đóng gói dữ liệu:** Closure có thể đóng gói dữ liệu và các hàm liên quan vào một đối tượng, tạo ra các đối tượng giống như lớp trong JavaScript.

## Cách Closure hoạt động

- Khi một hàm được định nghĩa, nó tạo ra một môi trường thực thi (execution context).
- Môi trường thực thi này chứa các biến và tham số của hàm.
- Khi hàm trả về, môi trường thực thi của nó thường bị hủy bỏ.
- Tuy nhiên, nếu hàm trả về một hàm con, hàm con này sẽ giữ một tham chiếu đến môi trường thực thi của hàm cha.
- Do đó, hàm con có thể truy cập và sử dụng các biến trong môi trường thực thi của hàm cha, ngay cả khi hàm cha đã kết thúc thực thi.

```js
function counter() {
  let count = 0;

  function increment() {
    return ++count;
  }

  return increment;
}

const incrementCounter = counter();

console.log(incrementCounter()); // 1
console.log(incrementCounter()); // 2
console.log(incrementCounter()); // 3
```

**Giải thích**

- **Khi `counter` được gọi**, một phạm vi (scope) mới được tạo ra.

  - Biến `count` tồn tại trong phạm vi này.
  - Hàm `increment` được định nghĩa trong phạm vi này.

- **Closure xảy ra khi `counter` trả về hàm `increment`**.

  - Hàm `increment` vẫn giữ tham chiếu đến phạm vi nơi `count` được định nghĩa, ngay cả sau khi `counter` hoàn tất.

- **Mỗi lần gọi `incrementCounter`**, hàm `increment` sử dụng biến `count` từ phạm vi mà nó "nhớ".

  - Biến `count` không bị khởi tạo lại mỗi lần gọi, mà được cập nhật liên tục.

## Ứng dụng của Closure

- **Tạo các module:** Closure được sử dụng để tạo các module JavaScript, giúp quản lý code và tránh xung đột tên.
- **Tạo các hàm tự thực thi (IIFE):** Closure được sử dụng để tạo các hàm tự thực thi, giúp khởi tạo các biến và hàm ngay khi chúng được định nghĩa.
- **Tạo các đối tượng giống như lớp:** Closure có thể đóng gói dữ liệu và các hàm liên quan vào một đối tượng, tạo ra các đối tượng giống như lớp trong JavaScript.
