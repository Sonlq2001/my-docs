---
sidebar_position: 8
---

# Primitive and Reference

Các kiểu dữ liệu nguyên thủy và tham chiếu trong JavaScript

## Primitive

Các kiểu dữ liệu tham trị bao gồm:

- Số (Number)
- Chuỗi (String)
- Boolean
- Null
- Undefined
- Symbol

**Định nghĩa**

Khi khởi tạo 1 biến giả trị, thì bản sao của giá trị sẽ được tạo ra khi bạn gán giá trị từ một biến này sang một biến khác.

Mỗi biến sẽ có một bản sao độc lập của giá trị, vì vậy nếu bạn thay đổi giá trị của một biến, biến khác sẽ không bị ảnh hưởng.

> Khi thực hiện gán thay đổi giá trị, giá trị ban đầu của biến sẽ không bị thay đổi theo giá trị gán.

```js
let a = 10; // Khai báo một biến a với giá trị 10
let b = a; // Gán giá trị của a cho b (sao chép giá trị, không phải tham chiếu)

b = 20; // Thay đổi giá trị của b

console.log(a); // 10, a không thay đổi
console.log(b); // 20, b đã thay đổi
```

> Trong ví dụ trên, `a` có giá trị là 10, và khi gán giá trị của `a` cho `b`, JavaScript tạo một bản sao của giá trị 10 và gán cho `b`. Sau đó, khi thay đổi giá trị của `b` thành 20, `a` không bị ảnh hưởng.

## Reference

Các kiểu dữ liệu tham chiếu bao gồm:

- Đối tượng (Object)
- Mảng (Array)
- Hàm (Function)

**Định nghĩa**

JavaScript sẽ lưu trữ một tham chiếu tới vị trí bộ nhớ chứa dữ liệu, thay vì sao chép chính dữ liệu đó.

Do đó, nếu bạn thay đổi giá trị trong một đối tượng hoặc mảng thông qua một biến, các biến khác trỏ tới cùng một đối tượng hoặc mảng đó cũng sẽ bị ảnh hưởng.

```js
let obj1 = { name: "Alice", age: 25 }; // Tạo một đối tượng obj1
let obj2 = obj1; // gán obj2 bằng obj1

obj2.age = 30; // Thay đổi giá trị thuộc tính 'age' của obj2

console.log(obj1.age); // 30, obj1 cũng bị thay đổi vì obj2 trỏ đến cùng một đối tượng
console.log(obj2.age); // 30, obj2 thay đổi giá trị
```

> Trong ví dụ trên, `obj1` là một đối tượng, và khi gán `obj1` cho `obj2`, cả hai biến `obj1` và `obj2` đều trỏ đến cùng một đối tượng trong bộ nhớ. Do đó, khi thay đổi thuộc tính age của `obj2`, `obj1` cũng bị ảnh hưởng.

## Compare Primitive and Reference

Sự khác biệt chính giữa tham chiếu và tham trị:

| Đặc điểm             | Tham Trị (Value)                            | Tham Chiếu (Reference)                                        |
| -------------------- | ------------------------------------------- | ------------------------------------------------------------- |
| Kiểu dữ liệu         | Số, Chuỗi, Boolean, Null, Undefined, Symbol | Mảng, Đối tượng, Hàm                                          |
| Hành vi khi gán      | Sao chép giá trị thực                       | Sao chép tham chiếu (vị trí bộ nhớ)                           |
| Thay đổi sau khi gán | Không ảnh hưởng đến biến ban đầu            | Thay đổi sẽ ảnh hưởng đến mọi biến trỏ đến cùng một đối tượng |

## Shallow copy

`Shallow copy` là khi bạn sao chép một đối tượng hoặc mảng nhưng chỉ sao chép bản sao của các tham chiếu của các đối tượng con, không sao chép sâu các đối tượng con đó.

Nghĩa là nếu đối tượng con bên trong bị thay đổi, các bản sao (và bản gốc) sẽ bị ảnh hưởng vì chúng đều trỏ đến cùng một đối tượng trong bộ nhớ.

:::info Thông tin

- Nếu bạn sao chép một đối tượng hoặc mảng có các giá trị kiểu nguyên thủy (số, chuỗi, boolean), những giá trị đó sẽ được sao chép hoàn toàn.

- Nếu đối tượng hoặc mảng chứa các đối tượng con (như đối tượng lồng nhau hoặc mảng lồng nhau), thì các đối tượng con chỉ được sao chép tham chiếu (vị trí bộ nhớ), thay vì sao chép toàn bộ giá trị của chúng.

:::

### Spread operator (...)

```js
const obj = { a: 1, b: 2, c: { d: 3 } };
const shallowClone = { ...obj };

obj.c.d = 34; // chúng ta thay đổi giá trị d của object gốc

console.log(obj); // kết quả cho chúng ta thấy {a:1,b:2,c:{d:34}}
console.log(shallowClone);
```

> Chúng ta thay đổi giá trị `d` của object gốc `d = 34`, nhưng object mà chúng ta clone ra cũng bị thay đổi theo `{a:1,b:2,c:{d:34}}`, Đơn giản đó là nó vẫn giữ những giá trị reference của object gốc là obj.

## Depp copy

`Deep copy` là khi sao chép một đối tượng hoặc mảng và tất cả các đối tượng con của nó. Điều này có nghĩa là bạn sẽ có một bản sao hoàn toàn độc lập với bản gốc, không có sự tham chiếu chung.

Nếu thay đổi bất kỳ đối tượng con nào trong bản sao, bản gốc sẽ không bị ảnh hưởng.

:::info Thông tin

- Deep copy sao chép toàn bộ giá trị của đối tượng hoặc mảng, bao gồm tất cả các đối tượng con hoặc mảng con bên trong chúng.

- Mỗi đối tượng con và mảng con được sao chép hoàn toàn, do đó, chúng không chia sẻ tham chiếu bộ nhớ với bản gốc.

:::

### JSON.parser and JSON.stringify

```js
const obj = { a: 1, b: 2, c: { d: 3 } };
const deepClone = JSON.parse(JSON.stringify(obj));

obj.c.d = 34;

console.log(obj); // {a:1,b:2,c:{d:34}}
console.log(deepClone); // {a:1,b:2,c:{d:3}}
```

> khi update `d = 34` thì object gốc đã thay đổi nhưng object clone thì không bởi vì nó không phải là reference type của object gốc nữa rồi.

:::warning Lưu ý

Phương pháp `JSON.parse()` và `JSON.stringify()` không thể sao chép các thuộc tính như undefined, Function, Date, v.v.

:::

### structuredClone

Phương thức `StructuredClone()` của `Window` tạo một bản sao sâu của một giá trị nhất định bằng thuật toán sao chép có cấu trúc.

```js
structuredClone(value);
structuredClone(value, options);
```
