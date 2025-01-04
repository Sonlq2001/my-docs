---
sidebar_position: 9
---

# Condition statements

Câu lệnh có điều kiện xác định liệu mã có nên được thực thi dựa trên một hoặc nhiều điều kiện hay không.

Một câu lệnh có điều kiện sẽ được thực thi nếu điều kiện `true`, sẽ bị bỏ qua nếu điều kiện `false`.

```js
if (condition) {
  // Mã sẽ được thực thi nếu điều_kiện đúng
} else {
  // Mã sẽ được thực thi nếu điều_kiện sai
}
```

## if...else

Câu lệnh kiểm tra điều kiện

### Example

1. **Chỉ có mình câu điều kiện `if`**

```js
if (condition) {
  console.log("True.");
}
```

Kết hợp với cả `else if`

```js
if (condition1) {
  // Mã sẽ được thực thi nếu điều_kiện condition1 đúng
} else if (condition2) {
  // Mã sẽ được thực thi nếu điều_kiện condition1 sai và condition2 đúng
} else {
  // Mã sẽ được thực thi nếu điều_kiện của condition1 và condition2 đều sai
}
```

2. **Nếu viết theo cấu trúc nối đuôi nhau như này thì trường hợp**

Cả `condition1` và `condition2` đều thỏa mãn điều kiện `true`, thì sẽ ưu tiên điều kiện nào được thực thi và viết trước.

```js
const a = 10;

if (a > 5) {
  console.log("lon hon 5");
} else if (a > 7) {
  console.log("lon hon 7");
} else {
  console.log("nho hon 5");
}

/**
 * ở đây cả điều kiện a > 5 và a > 7 đều đúng
 * nhưng sẽ chỉ đoạn mã trong a > 5 được thực hiện vì điều kiện đó được kiểm tra trước và thỏa mãn
 * -> bỏ quan các điều kiện còn lại
 * /
```

3. **Viết tách điều kiện thành các đoạn mã riêng lẻ, sẽ không bị phụ thuộc nhau.**

```js
if (a > 5) {
  console.log("lon hon 5");
}

if (a > 7) {
  console.log("lon hon 7");
} else {
  console.log("nho hon 5");
}

// cả console.log "lon hon 5" và "lon hon 7" đều được hiển thị
```

## switch...case

Cấu trúc điều kiện theo trường hợp, các giá trị tương ứng với từng trường hợp.

Nó cung cấp cách tổ chức `logic` rõ ràng hơn khi bạn có nhiều trường hợp (case) cần xử lý thay vì sử dụng quá nhiều câu lệnh `if...else`.

```js
switch (expression) {
  case value1:
    // Code chạy nếu expression === value1
    break;
  case value2:
    // Code chạy nếu expression === value2
    break;
  default:
  // Code chạy nếu không có case nào khớp
}
```

- `expression`: Là biểu thức được so sánh với các giá trị trong từng case.
- `case value`: Xác định giá trị mà expression sẽ được so sánh. Nếu khớp, code bên trong case sẽ chạy.
- `break`: Dùng để thoát khỏi khối switch. Nếu không có break, chương trình sẽ tiếp tục chạy các case bên dưới (gọi là "fall-through").
- `default`: Là tùy chọn, được thực thi nếu không có case nào khớp với expression.

```js
const day = 2;

switch (day) {
  case 1:
    console.log("Hôm nay là Thứ Hai");
    break;
  case 2:
    console.log("Hôm nay là Thứ Ba");
    break;
  case 3:
    console.log("Hôm nay là Thứ Tư");
    break;
  default:
    console.log("Không xác định");
}
// Hôm nay là Thứ Ba
```

### Example

1. **Nếu không dùng break, các case bên dưới sẽ tiếp tục được thực thi:**

```js
const color = "red";

switch (color) {
  case "red":
    console.log("Màu đỏ");
  case "blue":
    console.log("Màu xanh");
  default:
    console.log("Không xác định");
}

/**
 * Màu đỏ
 * Màu xanh
 * Không xác định
 * /
```

Nếu không dùng `break` thì tất cả các `case` sẽ đều được chạy.

Sẽ chạy đến khi gặp `break` thì mới dừng lại.

```js
const color = "red";

switch (color) {
  case "red":
    console.log("Màu đỏ");
  case "blue":
    console.log("Màu xanh");
    break;
  default:
    console.log("Không xác định");
}
/**
 * Có từ break ở case blue nên sẽ dừng lại và không chạy tiếp xuống default
 * -> kết quả:
 * Màu đỏ
 * Màu xanh
 * /
```

2. **Nếu các case đều có chung 1 kết quả thì `Fall-through` lại rất hữu ích**

Kết hợp nhiều case lại và chạy chung 1 logic

```js
const grade = "B";
switch (grade) {
  case "A":
  case "B":
    console.log("Bạn đạt yêu cầu");
    break;
  case "C":
    console.log("Bạn cần cố gắng thêm");
    break;
  default:
    console.log("Không hợp lệ");
}

/**
 * khi giá trị grade = A hoặc B thì sẽ đều rơi vào
 * kết quả: Bạn đạt yêu cầu
 */
```

3. **switch...case so sánh nghiêm ngặt**

:::warning Lưu ý
`switch...case` sử dụng so sánh nghiêm ngặt (`===`), nên phải khớp cả kiểu dữ liệu và giá trị.
:::

```js
const x = "1";
switch (x) {
  case 1:
    console.log("Số 1");
    break;
  case "1":
    console.log("Chuỗi 1");
    break;
}
// Chuỗi 1
```

4. **default**

`default` được hiểu là trường hợp còn lại, nếu như tất cả các `case` trên không đúng thì sẽ rơi vào.

Tương dự như `else` trong cấu trúc `if`

:::tip
Mặc dù `default` không bắt buộc trong `switch..case` nhưng nên được bổ sung vào để đảm bảo hết các trường hợp có thể xảy ra.
:::

```js
const fruit = "banana";
switch (fruit) {
  case "apple":
    console.log("Táo");
    break;
  case "orange":
    console.log("Cam");
    break;
  default:
    console.log("Không biết loại trái cây này");
}
// Không biết loại trái cây này
```

## When to use switch..case

- Khi cần kiểm tra một giá trị cụ thể với nhiều trường hợp (nhiều case).
- Vượt quá 3 lần kiểm tra điều kiện với `if...else` và giá trị thuộc dạng cụ thể với nhiều trường hợp thì nên dùng `switch...case`
