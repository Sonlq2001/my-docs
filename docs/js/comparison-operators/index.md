---
sidebar_position: 3
---

# Comparison operators

Các toán tử so sánh so sánh là sự so sánh giá trị của hai toán hạng và đánh giá xem câu lệnh mà chúng tạo ra là đúng hay sai. Kết quả thể hiện giá trị `Boolean`.

```js
2 == "2"; // true

2 === "2"; // false

2 == 2; // true
```

## Type coercion and equality

| Operator | Description                  | Usage       | Result |
| -------- | ---------------------------- | ----------- | ------ |
| `===`    | Toán tử bằng ( nghiêm ngặt ) | `2 === "2"` | false  |
| `!==`    | Toán tử khác ( nghiêm ngặt ) | `2 !== "2"` | true   |
| `==`     | Toán tử bằng (lỏng lẻo)      | `2 === "2"` | false  |
| `!=`     | Toán tử khác (lỏng lẻo)      | `2 != "2"`  | false  |
| `>`      | Toán tử lớn hơn              | `3 > 2`     | true   |
| `>=`     | Toán tử lớn hơn hoặc bằng    | `2 >= 2`    | true   |
| `<`      | Toán tử nhỏ hơn              | `2 < 3`     | true   |
| `<=`     | Toán tử nhỏ hơn hoặc bằng    | `2 <= 2`    | true   |

:::info[Thông tin]

- `===` và `!==` so sánh cả giá trị và kiểu giữ liệu của giá trị.
- `==` và `!=` chỉ so sánh giá trị và không so sánh kiểu giữ liệu.

:::

## Truthy and falsy

Tất cả các giá trị trong JavaScript đều hoàn toàn đúng hoặc sai và có thể bị ép buộc theo giá trị `boolean` tương ứng.

Có 5 kiểu giá trị dưới đây sẽ luôn được coi là `falsy` khi sử dụng:

- 1 chuỗi rỗng `""`
- `0`
- `null`
- `undefined`
- `NaN`

```js
null == undefined; // true
"" == 0; // true
```

## Logical operators

| Operator | Description                                         | Usage                 | Result |
| -------- | --------------------------------------------------- | --------------------- | ------ |
| `&&`     | Toán tử và (kết hợp 2 hay nhiều về của điều kiện)   | `2 == 3 && 0 == ""`   | false  |
| `\|\|`   | Toán tử hoặc (kết hợp 2 hay nhiều về của điều kiện) | `2 == 3 \|\| 0 == ""` | true   |
| `!`      | Toán tử phủ định (Đảo ngược)                        | `!false `             | true   |

### AND ( && )

### OR ( | | )

Chỉ trả về toán hạng đầu tiên trong hai toán hạng của nó nếu toán hạng đó đánh giá là `true` và toán hạng thứ hai nếu ngược lại. Trong các phép so sánh đánh giá theo giá trị `boolean`, điều này có nghĩa là nó trả về `true` nếu một trong hai toán hạng đánh giá là `true` và nếu không bên nào đánh giá là đúng thì nó sẽ trả về `false`.

```js
true || false; // true
false || true; // true
true || true; // true
false || false; // false
```

Khi sử dụng `||` với hai toán hạng không phải boolean, nó trả về toán hạng đầu tiên không thay đổi nếu nó có thể bị ép buộc thành đúng. Nếu toán hạng đầu tiên có thể bị ép buộc thành sai thì toán hạng thứ hai sẽ được trả về không thay đổi.

```js
false || "My string"; // "My string"
null || "My string"; // "My string"

"My string" || false; // "My string"
"My string" || "My second string"; // "My second string"

2 === 2 || "My string"; // true
```

:::info[Thông tin]

Các toán tử logic AND và OR không tự thực hiện bất kỳ sự ép buộc nào. Chúng trả về giá trị của một trong hai toán hạng đang được đánh giá, với toán hạng được chọn được xác định bởi đánh giá đó.

`&&`

- Khi tất cả các vế điều kiện cũng trả về `true`, thì giá trị sẽ trả về `true`, giá trị trả về là vế cuối cùng trong biểu thức điều kiện.
- Nếu có vế điều kiện nào trả về `false`, sẽ dừng lại quá trình kiểm tra điều kiện và trả về kết quả `false` luôn, mà không cần quan tâm đến các về điều kiện còn lại.

`||`

- Chỉ cần ít nhất 1 về trả về `true` thì điều kiện sẽ trả về `true`.
- Sẽ tiếp tục kiểm tra đến hết các vế còn lại, nếu chưa thấy về nào trả về `true`, sẽ chỉ dừng lại tại vế có giá trị trả về `true`.

```js
2 + 2 === 4 && 2 != "2"; // false
2 >= 2 && 2 <= 2 && 0; // 0

0 || NaN || "" || 6; // 6, giá trị mang tính truthy

!true; // false

!""; // true
```

:::

### NOT ( ! )

:::tip[Chú ý]
Nếu sử dụng 2 dấu `!!` thì sẽ ép kiểu dữ liệu đó sang kiểu `truthy` hoặc `falsy` tương ứng.

```js
!!0; // false;
!!1; // true;
```

:::
