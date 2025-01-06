---
sidebar_position: 15
---

# JSON

**JSON** (JavaScript Object Notation) là một định dạng dữ liệu nhẹ, dễ đọc và ghi, được sử dụng phổ biến để trao đổi dữ liệu giữa các hệ thống, đặc biệt là trong các ứng dụng web.

JSON được thiết kế dựa trên cú pháp đối tượng của JavaScript nhưng độc lập với ngôn ngữ lập trình, tức là nó có thể được sử dụng bởi hầu hết các ngôn ngữ như `Python`, `Java`, `C#`, `PHP` ...

## Cấu trúc của JSON

Một đối tượng JSON bao gồm các cặp `"key-value"` (khóa-giá trị), được bao quanh bởi dấu ngoặc nhọn {}. Các key là các chuỗi (string) và được đặt trong dấu ngoặc kép. `JSON` hỗ trợ các loại dữ liệu sau:

- **String:** Đặt trong dấu ngoặc kép.
- **Number:** Số nguyên hoặc số thập phân.
- **Boolean:** True hoặc false.
- **Null:** Biểu thị giá trị null.
- **Array:** Một danh sách các giá trị, được bao quanh bởi dấu ngoặc vuông [].
- **Object:** Một đối tượng JSON khác.

### String

```json
{
  "name": "Apple"
}
```

### Number

```json
{
  "price": 1000
}
```

### Boolean

```json
{
  "isActive": true
}
```

### Null

```json
{
  "weight": null
}
```

### Array

```json
{
  "shop": ["shop1", "shop2"]
}
```

### Object

```json
{
  "info": {
    "color": "red",
    "weight": 0.5
  }
}
```

:::warning

- `function`, `Date`, `undefined` không được `JSON` hỗ trợ.

- JSON không hỗ trợ comment.
  :::

## JSON và JavaScript

JSON thường được sử dụng trong JavaScript để lưu trữ hoặc trao đổi dữ liệu. JavaScript cung cấp các phương thức để làm việc với JSON:

### `JSON.stringify`

Chuyển đổi một đối tượng JavaScript thành một chuỗi JSON.

```js
JSON.stringify(value, replacer, space);
```

- `value`: Đối tượng JavaScript cần chuyển đổi.
- `replacer`: (Tùy chọn) Một hàm hoặc một mảng các khóa. Dùng để thay thế hoặc loại bỏ các giá trị trước khi chuyển đổi.
- `space`: (Tùy chọn) Một số hoặc một chuỗi. Dùng để định dạng chuỗi JSON đầu ra cho dễ đọc.

```js
const obj = { name: "John", age: 30, isStudent: false };
const jsonString = JSON.stringify(obj);
console.log(jsonString);
// Output: {"name":"John","age":30,"isStudent":false}
```

#### `replacer` để lọc thuộc tính

có thể là một hàm hoặc mảng, cho phép bạn chỉ định các thuộc tính nào sẽ được bao gồm trong chuỗi JSON.

```js
// Với mảng
const obj = { name: "John", age: 30, isStudent: false };
const jsonString = JSON.stringify(obj, ["name", "age"]);

console.log(jsonString);
// Output: {"name":"John","age":30}

// Với hàm
const obj = { name: "John", age: 30, birthYear: 1993 };
const jsonString = JSON.stringify(obj, (key, value) => {
  if (key === "birthYear") {
    return undefined; // Loại bỏ birthYear
  }
  return value;
});

console.log(jsonString);
// Output: {"name":"John","age":30}
```

#### `space` để định dạng JSON

Tham số space cho phép bạn thêm thụt lề hoặc khoảng trắng để dễ đọc hơn.

```js
const obj = { name: "John", age: 30, skills: ["JavaScript", "HTML", "CSS"] };
const jsonString = JSON.stringify(obj, null, 2);

console.log(jsonString);
/* Output:
{
  "name": "John",
  "age": 30,
  "skills": [
    "JavaScript",
    "HTML",
    "CSS"
  ]
}
*/
```

### `JSON.parse`

Chuyển đổi một chuỗi JSON thành một đối tượng JavaScript.

```js
JSON.parse(text, reviver);
```

- **`text`**: Chuỗi JSON cần phân tích.
- **`reviver`** (tùy chọn): Một hàm để chỉnh sửa hoặc chuyển đổi các giá trị trong đối tượng JSON trước khi trả về.

```js
const jsonString = '{"name": "John", "age": 30, "isStudent": false}';
const obj = JSON.parse(jsonString);
// obj = {name: "John", age: 30, isStudent: false}
```

#### **Sử dụng `reviver` để tùy chỉnh kết quả**:

`reviver` là một hàm được gọi cho mỗi cặp `key:value` trong đối tượng JSON, cho phép bạn thay đổi giá trị khi parse.

```js
const jsonString = '{"name": "John", "age": 30, "birthYear": 1993}';
const obj = JSON.parse(jsonString, (key, value) => {
  if (key === "birthYear") {
    return 2025 - value; // Tính tuổi từ năm sinh
  }
  return value;
});

console.log(obj);
// Output: { name: "John", age: 30, birthYear: 32 }
```

## Ứng dụng của JSON

1.  **Trao đổi dữ liệu giữa client và server:**

    - JSON là định dạng phổ biến trong các API RESTful.
    - Ví dụ, khi một ứng dụng front-end gửi yêu cầu đến server, dữ liệu trả về thường ở dạng JSON.

2.  **Lưu trữ cấu hình:**

    - JSON thường được sử dụng trong các tệp cấu hình (e.g., `package.json` trong Node.js).

3.  **Lưu trữ dữ liệu:**

    - JSON có thể được sử dụng như một cơ sở dữ liệu đơn giản (e.g., Firebase, MongoDB).

4.  **Tương thích với nhiều ngôn ngữ lập trình:**

    - JSON được hỗ trợ natively bởi nhiều ngôn ngữ lập trình, giúp dễ dàng chia sẻ dữ liệu.

## JSON so với các định dạng khác

| **Đặc điểm**        | **JSON**                   | **XML**        | **YAML**         |
| ------------------- | -------------------------- | -------------- | ---------------- |
| **Đọc dễ dàng**     | Dễ đọc, gọn gàng           | Khó đọc hơn    | Dễ đọc hơn       |
| **Kích thước**      | Nhẹ hơn                    | Lớn hơn        | Nhẹ              |
| **Cú pháp**         | Sử dụng dấu ngoặc, dễ hiểu | Thẻ mở và đóng | Dấu cách và dòng |
| **Hỗ trợ ngôn ngữ** | Phổ biến                   | Phổ biến       | Ít phổ biến hơn  |
