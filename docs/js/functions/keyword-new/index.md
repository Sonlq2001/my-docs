---
sidebar_position: 3
sidebar_label: "Keyword 'new'"
---

# The new keyword

Gọi một hàm bằng `new` sẽ tạo một đối tượng mới bằng cách sử dụng hàm được gọi làm "hàm tạo" cho đối tượng đó

```js
function MyFunction() {}
const myObject = new MyFunction();

console.log(typeof myObject); // object
```

Điều này cho phép cung cấp một mẫu để tạo các đối tượng theo cùng một mẫu cấu trúc. (Tương tự như cách viết `class`)

:::info[Thông tin]
Nên sử dụng `class` trong ES6 đầy đủ các tính năng hơn để tạo ra các lớp đối tượng.
:::

```js
function MyFunction() {
  this.myProperty = true;
}
const myObject = new MyFunction();

console.log(myObject.myProperty); // true
```

:::info[Thông tin]
Từ khóa `this` đề cập đến đối tượng được tạo từ hàm tạo.
:::
