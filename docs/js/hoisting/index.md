---
sidebar_position: 16
title: Hoisting
---

**Hoisting** là một cơ chế trong JavaScript mà **các khai báo biến, hàm, hoặc lớp** được "đưa lên đầu" phạm vi trước khi mã được thực thi. Điều này có nghĩa là bạn có thể sử dụng các biến hoặc hàm trong mã của mình trước khi chúng được khai báo.

Tuy nhiên, **hoisting không di chuyển mã thực sự lên trên**, mà chỉ là cách JavaScript xử lý ngầm các khai báo trong quá trình **compile** (giai đoạn chuẩn bị trước khi thực thi mã).

## Hoisting variable

- **Khai báo bằng `var`:** Khi bạn khai báo một biến bằng `var`, khai báo đó được "nâng" lên đầu phạm vi. Tuy nhiên, giá trị của biến vẫn là `undefined` cho đến khi dòng code gán giá trị được thực thi.

- **Khai báo bằng `let` và `const`:** Với `let` và `const`, biến cũng được hoisting, nhưng chúng không được khởi tạo với giá trị `undefined`. Nếu bạn cố gắng sử dụng biến `let` hoặc `const` trước khi khai báo, sẽ xảy ra lỗi `ReferenceError`.

```js
console.log(x); // undefined
var x = 10;

console.log(y); // lỗi
let y = 20;

console.log(z); // lỗi
const z = 30;
```

## Hoisting function

- **Function Declaration** (Khai báo hàm): Khai báo hàm cũng được hoisting lên đầu phạm vi. Điều này có nghĩa là bạn có thể gọi một hàm trước khi nó được khai báo trong mã.

- **Function Expression và Arrow Function** (Biểu thức hàm): Biểu thức hàm không được hoisting. Nếu bạn cố gắng gọi một biểu thức hàm trước khi nó được khai báo, sẽ xảy ra lỗi ReferenceError.

```js
// Function Declaration, vẫn hoạt động bình thường
myFunction();
function myFunction() {
  console.log("hi");
}

// Function Expression, xảy ra lỗi
myFunction();
const myFunction = function () {
  console.log("hi");
};

// Arrow Function, xảy ra lỗi
myFunction();
const myFunction = () => {
  console.log("hi");
};
```

:::warning

- Hoisting chỉ áp dụng cho các khai báo biến và hàm, không áp dụng cho các biểu thức hoặc câu lệnh khác.
- Hoisting có thể gây ra một số vấn đề khó hiểu nếu không được sử dụng đúng cách. Vì vậy, tốt nhất nên khai báo biến và hàm ở đầu phạm vi của chúng để tránh những bất ngờ không mong muốn.

:::
