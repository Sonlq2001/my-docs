---
sidebar_position: 4
sidebar_label: "Keyword 'return'"
---

# The return keyword

Sử dụng từ khóa `return` để chỉ định 1 hàm sẽ được trả về dưới 1 giá trị.

Khi trình thông dịch gặp `return`, hàm chứa câu lệnh đó ngay lập tức kết thúc và giá trị đã chỉ định sẽ được trả về ngữ cảnh nơi hàm được gọi.

```js
// function expression
const myFunction = function () {
  return 2 + 2;
};

// arrow function
const myFunction = () => 2 + 2;

myFunction(); //4
```

Một hàm trả về một giá trị có thể được coi như 1 biến

```js
const myFunction = function () {
  return 2 + 2;
};

myFunction() + myFunction(); // 4 + 4 = 8
```

Nếu `return` không có giá trị trả về, kết quả sẽ là `undefined`

```js
const myFunction = function () {
  return;
};

myFunction(); //undefined
```

Từ khóa `return` báo hiệu sự kết thúc của một hàm nên bất kỳ mã nào theo sau một `return` gặp phải sẽ không được thực thi.

```js
const myFunction = function () {
  return true;
  console.log("This is a string."); // câu lệnh console không được thực thi
};

myFunction(); // true
```

Việc kết thúc hàm chỉ áp dụng cho câu lệnh `return` gặp phải trong quá trình thực thi hàm, không áp dụng cho các `lệnh điều kiện`.

```js
const myFunction = function (flag) {
  if (flag) {
    return 1;
  }
  return 2;
};

myFunction(); // 2

myFunction(true); // 1
```

:::tip[Chú ý]
Khi thực hiện các điều kiện trong hàm và trả về giá trị, ưu tiên các trường hợp dễ cho lên trước, bởi vì nó sẽ tối ưu chương trình chạy của ta hơn.
:::

```js
function checkIsNumber(number) {
  // đưa điều kiện kiểm tra lên trước, nếu trường hợp không phải số sẽ dừng lại và trả vè kết quả luôn.
  if (typeof number !== "number") {
    return false;
  }

  return true;
}

checkIsNumber("5"); // false
checkIsNumber(5); // true
```
