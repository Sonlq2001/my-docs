---
sidebar_position: 3
---

# Swap variable

Trong lập trình, **swap variable** (hoán đổi biến) là một thao tác thay đổi giá trị giữa hai biến. Điều này có nghĩa là giá trị của biến này sẽ được gán cho biến kia, và ngược lại.

Ví dụ, giả sử ta có hai biến `a` và `b`, với giá trị ban đầu của chúng là:

```js
let a = 5;
let b = 10;
```

Sau khi thực hiện thao tác swap, giá trị của a và b sẽ hoán đổi:

```js
let a = 10;
let b = 5;
```

## How to do it

### Temporary variable

Sử dụng 1 biến tạm (`temp variable`), đây là phương pháp phổ biến nhất, sử dụng một biến tạm thời để lưu giá trị của một biến trong quá trình hoán đổi.

```js
let a = 1;
let b = 2;

// sử dụng biến tạm
let temp;

temp = a;
a = b;
b = temp;

console.log(a); // => 2
console.log(b); // => 1
```

### Destructuring assignment

```js
let a = 1;
let b = 2;

[a, b] = [b, a];

console.log(a); // => 2
console.log(b); // => 1
```

`[a, b] = [b, a]` là phép gán phá hủy hoán đổi các biến `a` và `b`

Nó hoạt động với mọi loại dữ liệu: `boolean`, `string`, `number`, `object`

> Ưu tiên cách sử dụng này trong mọi trường hợp

### Addition and subtraction

```js
let a = 1;
let b = 2;

a = a + b;
b = a - b;
a = a - b;

console.log(a); // => 2
console.log(b); // => 1
```
