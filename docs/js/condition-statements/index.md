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

Chỉ có mình câu điều kiện `if`

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

**Nếu viết theo cấu trúc nối đuôi nhau như này thì trường hợp**

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

**Viết tách điều kiện thành các đoạn mã riêng lẻ, sẽ không bị phụ thuộc nhau.**

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
