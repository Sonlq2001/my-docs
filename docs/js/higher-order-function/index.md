---
sidebar_position: 18
title: Higher order function
---

Trong JavaScript, **hàm bậc cao (higher-order function)** là một hàm có thể:

- **Nhận một hoặc nhiều hàm khác làm đối số:** Điều này có nghĩa là bạn có thể truyền một hàm vào một hàm khác như một tham số.
- **Trả về một hàm:** Hàm bậc cao có thể tạo ra và trả về các hàm mới.

> HOF là một phần quan trọng của lập trình hàm (functional programming) trong JavaScript, giúp viết mã ngắn gọn, dễ đọc và tái sử dụng cao

## Các đặc điểm chính

1.  **HOF nhận hàm làm tham số**

- Hàm được truyền vào (callback) sẽ được thực thi bên trong HOF.
- Ví dụ: `Array.prototype.map()` nhận một hàm callback làm tham số.

2.  **HOF trả về một hàm khác**

- HOF có thể tạo và trả về một hàm mới, thường kết hợp với closure.

3.  **Tái sử dụng logic**

- HOF cho phép bạn tách biệt các phần logic của chương trình, làm cho mã linh hoạt hơn.

### HOF nhận hàm làm tham số

```js
function higherOrderFunction(callback) {
  console.log("Before executing the callback");
  callback();
  console.log("After executing the callback");
}

function sayHello() {
  console.log("Hello, world!");
}

higherOrderFunction(sayHello);
```

- `higherOrderFunction` nhận hàm `callback` làm tham số.
- Hàm `sayHello` được truyền vào như một callback và được thực thi bên trong `higherOrderFunction`.

### HOF trả về một hàm khác

```js
function createMultiplier(factor) {
  return function (number) {
    return number * factor;
  };
}

const double = createMultiplier(2); // Trả về một hàm nhân đôi
const triple = createMultiplier(3); // Trả về một hàm nhân ba

console.log(double(5)); // Output: 10
console.log(triple(5)); // Output: 15
```

- `createMultiplier` trả về một hàm mới.
- Hàm trả về sử dụng closure để truy cập biến `factor` từ phạm vi của `createMultiplier`.

### HOF với các phương thức tích hợp sẵn

JavaScript cung cấp nhiều HOF tích hợp sẵn để làm việc với mảng, như: map, filter, reduce, forEach

```js
const numbers = [1, 2, 3, 4];
const squared = numbers.map((num) => num * num);

console.log(squared); // Output: [1, 4, 9, 16]
```

- `map` là một HOF.
- Nó nhận một hàm callback làm tham số, áp dụng callback này lên từng phần tử của mảng và trả về một mảng mới.
