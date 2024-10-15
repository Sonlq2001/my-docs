---
sidebar_position: 2
---

# Asynchronous

- `sync (Đồng bộ)` chạy từ trên xuống dưới theo đúng thứ tự viết.

- `async (Bất đồng bộ)` không chạy theo đúng thứ tự viết.

```js title="Example"
function fn1() {
  setTimeout(() => {
    console.log("1");
  }, 1000); // 1s
}

function fn2() {
  console.log("2");
}

fn1();
fn2();
```

Ở ví dụ trên, ta sẽ nghĩ giá trị hiển thị sẽ được in là `1` xong mới đến `2` ( chạy đồng bộ ), nhưng do hàm `fn1` có sử dụng `setTimeout` nên logic code đã chạy khác đi ( chạy bất đồng bộ ).

Sau khi hàm `fn2` được gọi xong thì `1s` sau hàm `fn1` mới được gọi.

Kết quả: `2` xong mới đến `1`.

> Việc chạy bất đồng bộ sẽ giúp cho các task vụ của ta sẽ không bị dừng lại mà tiếp tục chạy song song các tác vụ khác.
