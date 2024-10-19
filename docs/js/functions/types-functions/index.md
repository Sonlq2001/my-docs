---
sidebar_position: 2
---

# Function types

## Function expression

Gán biểu thức hàm vào 1 biến.

```js
const myFn = function () {
  console.log("Hi");
};
myFn();
```

Có thể vừa đặt tên cho hàm và vừa gán biểu thức đó vào biến.

```js
const myVariable = function myFunction() {
  console.log("Hi");
};

myVariable(); // Hi
```

> Chỉ sử dụng tên biến để gọi hàm, tên hàm lúc này sẽ không có tác dụng gọi hàm.

**Có thể tự gọi hàm bên trong thân hàm (Đệ quy)**

```js
const myVariable = function myFunction() {
  console.log("One second elapsed.");
  setTimeout(myFunction, 1000);
};
setTimeout(myVariable, 1000);
```

## Arrow function

Được giới thiệu trong `ES6`, với cú pháp ngắn gọn.

```js
const myFunction = () => {
  console.log("Hi");
};
myFunction();
```

Trường hợp muốn trả về luôn giá trị, có thể viết, không cần phải thêm dấu ngoặc nhọn `{}`

```js
const myFunction = () => 2 + 2;
myFunction(); // 4
```

:::info[Thông tin]
`Arrow function` sẽ không có `this`, thay vào đó nó sẽ kế thừa từ môi trường bao quanh hàm `arrow`, hàm bao quanh gần nhất cung cấp các ngữ cảnh đó.

JS được chạy phía `client` thì `Arrow function` có `this` là đối tượng `window`
:::

```js
function myParentFunction() {
  this.myProperty = true;
  let myFunction = () => {
    console.log(this);
  };
  myFunction();
}

let myInstance = new myParentFunction();
console.log(myInstance); // { myProperty: true }
```

### Call arrow functions

Hàm mũi tên không liên kết các đối số giống như các loại hàm khác. Một đối tượng `arguments` trong phần thân của `hàm mũi` tên kế thừa giá trị của nó từ môi trường bao quanh gần nhất của hàm mũi tên đó.

```js
// 1. arrow function
function myFunction() {
  let myArrowFunction = () => {
    // arguments được kế thừa từ đối số truyền trong hàm myFunction
    console.log(arguments[0]);
  };
  myArrowFunction(true); // gọi hàm arrow function và truyền đối số
}

myFunction(false); // false

// 2. loại function khác
function myFunction() {
  let myArrowFunction = function () {
    console.log(arguments[0]);
  };
  myArrowFunction(true); // gọi hàm function và truyền đối số
}

myFunction(false); // true
```

**Trường hợp không kế thừa được từ, nhưng vẫn cố gắng truy cập, sẽ gặp ra lỗi.**

```js
let myArrowFunction = () => {
  console.log(arguments);
};
myArrowFunction(true); // error
```

## Anonymous function

## Immediately Invoked Function Expressions (IIFE)

Hàm tự gọi

```js
(function (msg) {
  console.log(msg);
})("IIFE"); // IIFE
```
