---
sidebar_position: 1
---

# Callback

Là 1 hàm (`Function`) được truyền dưới dạng là `đối số` cho hàm khác và được `gọi` trong chính cái `hàm nhận đối` số đó.

> Function callback sẽ được thực thi sau khi một function khác đã được thực thi xong.

## Function Sequence

Các hàm JavaScript được thực thi theo trình tự chúng được gọi. Không theo trình tự chúng được xác định.

```js
function myFirst() {
  console.log("Hello");
}

function mySecond() {
  console.log("Goodbye");
}

myFirst(); // Hello
mySecond(); // Goodbye
```

## Sequence Control

Kiểm soát thứ tự gọi hàm theo mong muốn

**Giả sử bạn muốn thực hiện một phép tính và sau đó hiển thị kết quả.**

```js
function display(value) {
  console.log(`Kết quả = ${value}`);
}

function sumNumber(a, b) {
  return a + b;
}

const result = sumNumber(1, 2);
display(result); // Kết quả = 3
```

Hoặc

```js
function display(value) {
  console.log(`Kết quả = ${value}`);
}

function sumNumber(a, b) {
  display(a + b); // gọi hàm display luôn trong hàm sumNumber
}

sumNumber(1, 2); // Kết quả = 3
```

## Callbacks

```js
function display(value) {
  return `Kết quả = ${value}`;
}

function sumNumber(a, b, callback) {
  return callback(a + b); // gọi hàm callback
}

sumNumber(1, 2, display); // truyền hàm display làm đối số cho hàm sumNumber
```

```js
// chọn ra các phần tử có giá trị chẵn
const numbers = [1, 20, 4, 6, 9];

const result = evenNumberFilter(numbers, (num) => num % 2 === 0);
console.log(result); // [20, 4, 6]

function evenNumberFilter(arrayNum, callback) {
  const array = [];
  for (const num of arrayNum) {
    if (callback(num)) {
      // mỗi lần vòng lặp chạy sẽ gọi call 1 lần
      array.push(num);
    }
  }
  return array;
}
```

:::warning[Chú ý]
Khi truyền `callback` làm đối số không được sử dụng dấu `()`

sumNumber(1, 2, display);

<del>sumNumber(1, 2, display());</del>
:::
