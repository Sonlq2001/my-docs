---
sidebar_position: 2
---

# Variables

## Naming convention

Biến là cấu trúc dữ liệu gán tên đại diện cho một giá trị. Chúng có thể chứa bất kỳ loại dữ liệu nào.

Tên của một biến được gọi là định danh. Phải được viết theo quy tắc:

- Có thể chứa các chữ cái `Unicode`, ký hiệu đô la (`$`), ký tự gạch dưới (`_`), chữ số (`0-9`) và thậm chí một số ký tự `Unicode`.
- Không thể chưa khoảng trắng trong tên biến
- Phải bắt đầu bằng một chữ cái, dấu gạch dưới (`_`) hoặc ký hiệu đô la (`$`). Không được bắt đầu bằng số.

```js title="Example"
var a = true;
var _b = "Hello";
var $c = [1, 2];
var 9d = {name: "Hi"} // sai quy tắc đặt tên
```

:::danger[Cảnh báo]
Đặt tên biến không được chứa các ký tự đặc biệt `! . , / \ + - * =`
:::

Sử dụng quy ước đặt tên phổ biến `camelCase`

```js
let camelCasedIdentifier = true;
```

Một số dự án sử dụng các quy ước đặt tên khác tùy thuộc vào ngữ cảnh và tính chất của dữ liệu. Sử dụng `Pascal` để đặt tên cho `class`

```js
class MyClass {}
```

## Variable declaration

Có 3 từ khóa dùng để khai báo biến `var`, `let` và `const`.

```js
let myVariable; //
// Khai báo biến nhưng không khởi tạo giá trị, giá trị lúc này của myVariable là undefined

let number = 5;
console.log(number + number); // 10
```

Khai báo theo danh sách liên kết:

```js
let firstVariable, secondVariable, thirdVariable;

var firstVariable = 1,
  secondVariable = "hello",
  thirdVariable = [1, 2];
```

### var

Từ khóa khai báo biến `var`, là từ khóa khai báo biến lỏng lẻo.

```js
var myString = "hello";
```

Bạn có thể khai báo lại tên biến, nhưng điều này `thực sự không tốt`.

```js
var myString = "hello";
var myString = 5;

console.log(myString); // 5

var greeting = "hey hi";
if (true) {
  var greeting = "say Hello instead";
}

console.log(greeting); //"say Hello instead"
```

Phạm vi của từ khóa `var` là `global`, không phân biệt phạm vi khai báo biến (ngoại trừ được khai báo trong phạm vi của `Function`). Ở bất kì vị trí nào trong file code đều có thể khai báo lại, gán lại và truy cập được.

> Đặc biệt, biến var còn có thêm tính chất hoisting: nghĩa là dù khai báo ở đâu thì biến đều sẽ được đem lên đầu scope trước khi code được thực hiện.

:::danger[Cảnh báo]
Khuyến nghị Không nên dùng từ khóa `var` để khai báo biến. Hãy dũng `let` và `const`.
:::

### let

Tương tự như với từ khóa `var`, nhưng từ khóa `let` có tính nghiêm ngặt hơn.

```js
let myBook = "book";
```

Bạn có thể gán lại giá trị, nhưng `không được phép` khai báo lại tên biến.

```js
let number = 10;
number = 20;

let number = 30; // error
```

Từ khóa `let` sẽ có `block scope`.

```js
if (true) {
  let number = 10;
  console.log(number); // 10
}

console.log(number); // error
```

Khác `block scope` thì vẫn hoàn toàn có thể khai báo `trùng với tên biến đã khai báo trước đó`, **Nhưng không khuyển nghị vì dễ dàng bị nhâm lẫn**.

```js
let greeting = "say Hi";
if (true) {
  let greeting = "say Hello instead";
  console.log(greeting); // "say Hello instead"
}
console.log(greeting); // "say Hi"
```

> `let` cũng có tính `hoisting` tuy nhiên lại khác nhau ở chỗ thay vì `var` được khởi tạo với giá trị là `undefined` thì `let` sẽ không có bất kỳ giá trị khởi tạo nào.

### const

Dùng từ khóa `const` để khai báo `hằng số`, một loại biến phải được khởi tạo ngay lập tức và sau đó `không thể thay đổi` giá trị.

```js
const keyword = "TODAY";
const options = [
  { label: "option 1", value: 1 },
  { label: "option 2", value: 2 },
];
```

Không thể khai báo một hằng số mà không gán ngay một giá trị cho nó.

```js
const name; // error
```

Không thể khai báo lại tên biến đã đặt và gán lại giá trị.

```js
const keyword = "TODAY";
keyword = "MONDAY"; // error
const keyword = 10; // error
```

Tuy nhiên khi `hằng số` được khai báo với các kiểu dữ liệu là `Tham chiếu (object, array)`, thì sẽ có thể `thêm, sửa, xóa` giá trị của đối tượng biến đó.

```js
const constantObject = { name: "A" };
constantObject.name = "B";
console.log(constantObject); // {name: "B"}

const arrayNumber = [1, 2, 3, 4];
arrayNumber.pop();
console.log(arrayNumber); // [1,2,3]
```

> Khác `block scope` thì vẫn hoàn toàn có thể khai báo `trùng với tên biến đã khai báo trước đó`, **Nhưng không khuyển nghị vì dễ dàng bị nhâm lẫn**.

:::tip[TIP]
Nên khai báo `const` khi không mong muốn giá trị của mình được gán lại.
:::

## Variable scope

### Block scope

Bất kỳ biến nào bạn khai báo bằng `let` hoặc `const` đều nằm trong phạm vi câu lệnh khối chứa gần nhất của nó, nghĩa là biến đó chỉ có thể được truy cập trong khối đó. Việc cố gắng truy cập biến đó sẽ gây ra lỗi.

```js
{
  let scopedVariable = true;
  console.log(scopedVariable);
}
console.log(scopedVariable); //error
```

Một biến nó chỉ tồn tại trong phạm vi của khối đó.

```js
{
  const myConstant = false;
  console.log(myConstant); // false
}
const myConstant = true;
console.log(myConstant); // true
```

### Function Scope

Khi khai báo biến trong `Function` phạm vi sử dụng chỉ ở trong `block scope` của `Function` đó, bên ngoài sẽ không thể truy cập được. Kể cả sử dụng từ khóa `var` thì cũng sẽ lỗi.

```js
function myFunction() {
  var scopedVariable = true;
  return scopedVariable;
}

console.log(scopedVariable); // error
```

### Global scope

Biến toàn cục cho phép bạn truy cập mọi nơi trong file code. Nhưng tránh lạm dụng dùng bất cứ khi nào. Đảm bảo code được tuần tự, dễ đọc, giảm thiểu vùng nhớ khai báo biến.

```js
let blockGlobal = true; // Global
if (true) {
  console.log(blockGlobal); // true
}

(function () {
  console.log(blockGlobal); // true
})();
```

Việc gán một giá trị cho một biến mà không khai báo nó một cách rõ ràng (nghĩa là không bao giờ sử dụng `var`, `let` hoặc `const` để tạo nó)
sẽ nâng một biến lên phạm vi toàn cục, ngay cả khi được khởi tạo bên trong hàm hoặc khối. Một biến được tạo bằng cách sử dụng này đôi khi được gọi là `"implied global"`.

```js
function myFunction() {
  globalVariable = "global";
  return globalVariable;
}

console.log(myFunction()); // global
console.log(globalVariable); // global
```

## Variable Hoisting

Các khai báo biến và hàm được đưa lên đầu phạm vi của chúng, nghĩa là trình thông dịch JavaScript xử lý bất kỳ biến nào được khai báo tại bất kỳ điểm nào
trong tập lệnh và di chuyển biến đó đến dòng đầu tiên trong phạm vi kèm theo của nó một cách hiệu quả trước khi thực thi tập lệnh.

Một biến được khai báo bằng `var` có thể được tham chiếu trước khi biến được khai báo mà không gặp lỗi

```js
console.log(hoistedVariable); // undefined
var hoistedVariable;
```

> chỉ áp dụng cho `var`, `let` hoặc `const` sẽ không được áp dụng.

`let` và `const` sẽ báo lỗi

```js
console.log(variableLet); // error
console.log(variableConst); // error

let variableLet = "hello";
const variableConst = "world";
```

## Note

####  Kiểu dữ liệu nguyên thủy (Primitive Types)

- Bao gồm: `number`, `string`, `boolean`, `null`, `undefined`, `symbol`, và `bigint`.
- Khi truyền vào hàm, JavaScript sử dụng cơ chế **truyền bằng giá trị** (pass-by-value).
  - Điều này có nghĩa là chỉ giá trị của biến được sao chép và truyền vào tham số của hàm.
  - Biến gốc không bị ảnh hưởng bởi thay đổi trong hàm.

```js
let number = 10;

function modify(value) {
  value = 20; // Thay đổi giá trị value
}

modify(value);
console.log(number); // Output: 10
```

#### Kiểu dữ liệu tham chiếu (Reference Types)

- Bao gồm: `object`, `array`, và `function`.
- Khi truyền vào hàm, JavaScript vẫn sử dụng **pass-by-value**, nhưng giá trị được sao chép là **tham chiếu** đến đối tượng.
  - Điều này có nghĩa là nếu thay đổi thuộc tính của đối tượng, đối tượng gốc cũng bị thay đổi.

```js
let obj = { value: 10 };

function modify(obj) {
  obj.value = 20; // Thay đổi thuộc tính của đối tượng
}

modify(obj);
console.log(obj.value); // Output: 20
```
