---
sidebar_position: 5
---

# Break and Continue

`break` và `continue` là hai từ khóa dùng để kiểm soát luồng của các vòng lặp.

Chúng giúp điều chỉnh hành vi của vòng lặp mà không cần đợi đến khi điều kiện lặp kết thúc.

## Break

Từ khóa `break` được sử dụng để thoát hoàn toàn khỏi vòng lặp hiện tại.

Khi gặp `break`, chương trình sẽ dừng ngay lập tức vòng lặp và tiếp tục thực thi mã sau vòng lặp đó.

```js
if (condition) {
  break;
}
```

```js
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    console.log("Dừng vòng lặp tại i = 5");
    break;
  }
  console.log(i);
}
// 0
// 1
// 2
// 3
// 4
// Dừng vòng lặp tại i = 5
```

## Continue

Từ khóa `continue` được sử dụng để bỏ qua phần còn lại của khối mã trong vòng lặp hiện tại và chuyển ngay sang lần lặp tiếp theo.

Vòng lặp sẽ không kết thúc, chỉ bỏ qua lần lặp đó.

```js
if (condition) {
  continue;
}
```

```js
for (let i = 0; i < 10; i++) {
  if (i % 2 === 0) continue; // Bỏ qua số chẵn
  console.log(i);
}

// 1
// 3
// 5
// 7
// 9
```

## Use in nested loops

Khi sử dụng `break` hoặc `continue` trong vòng lặp lồng nhau, chúng chỉ áp dụng cho vòng lặp gần nhất.

Để thoát khỏi vòng lặp bên ngoài, bạn cần sử dụng nhãn (`label`).

```js
outerLoop: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (i === 1 && j === 1) break outerLoop; // Thoát khỏi cả hai vòng lặp
    console.log(`i = ${i}, j = ${j}`);
  }
}

outerLoop: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (i === 1 && j === 1) continue outerLoop; // Chuyển ngay tới lần lặp kế tiếp của vòng lặp ngoài
    console.log(`i = ${i}, j = ${j}`);
  }
}
```

## Compare

| Đặc điểm              | break                            | continue                |
| --------------------- | -------------------------------- | ----------------------- |
| Chức năng             | Thoát khỏi vòng lặp ngay lập tức | Bỏ qua lần lặp hiện tại |
| Vòng lặp kết thúc?    | Có                               | Không                   |
| Tiếp tục lần lặp sau? | Không                            | Có                      |
