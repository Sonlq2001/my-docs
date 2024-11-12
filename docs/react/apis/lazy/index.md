---
sidebar_position: 2
---

# lazy

Cho phép bạn trì hoãn việc tải mã của thành phần cho đến khi nó được hiển thị lần đầu tiên.

```jsx
const SomeComponent = lazy(load);
```

## Reference

```jsx
import { lazy } from "react";

const MarkdownPreview = lazy(() => import("./MarkdownPreview.js"));
```

### Parameters

`load`

- Một hàm trả về một `Promise` hoặc một hàm khác có thể sử dụng được (một đối tượng giống như `Promise` với phương thức then).
- React sẽ không gọi tải cho đến lần đầu tiên bạn cố gắng hiển thị thành phần được trả về. Sau khi React gọi lần đầu tiên tải, nó sẽ đợi nó giải quyết và sau đó hiển thị .default của giá trị đã giải quyết dưới dạng thành phần React.
- Cả giá trị Promise được trả về và giá trị đã phân giải của Promise sẽ được lưu vào bộ đệm, do đó React sẽ không gọi tải nhiều lần. Nếu Promise từ chối, React sẽ ném lý do từ chối để Ranh giới lỗi gần nhất xử lý.

<!-- TODO: update later -->
