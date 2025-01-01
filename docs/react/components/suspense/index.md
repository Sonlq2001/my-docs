---
sidebar_position: 1
---

# `<Suspense>`

`Suspense` là một component tích hợp sẵn trong React, được thiết kế để xử lý việc chờ dữ liệu hoặc tài nguyên sẵn sàng trước khi hiển thị nội dung của ứng dụng.

Mục đích chính của `Suspense` là cải thiện trải nghiệm người dùng bằng cách hiển thị một giao diện chờ (fallback) trong khi ứng dụng tải dữ liệu, tải component, hoặc thực hiện một số tác vụ khác.

```jsx
<Suspense fallback={<Loading />}>
  <SomeComponent />
</Suspense>
```

## **Tính năng của `Suspense`**

1.  **Loading Indicator (Giao diện chờ)**: `Suspense` cho phép bạn định nghĩa một giao diện dự phòng (`fallback`) hiển thị trong khi dữ liệu hoặc component con đang được tải.

2.  **Kết hợp với `React.lazy`**: `Suspense` thường được sử dụng với `React.lazy` để tải component theo kiểu lazy-loading (tải khi cần).

3.  **Hỗ trợ cho `React Server Components` và `React Concurrent Features`**: `Suspense` làm việc tốt với các tính năng hiện đại của React, chẳng hạn như Concurrent Mode và Server Components.

### Kết hợp với `React.lazy`

`React.lazy` cho phép tải động các component, giảm kích thước gói bundle ban đầu của ứng dụng.

```jsx
import React, { Suspense } from "react";

// Tải động một component
const LazyComponent = React.lazy(() => import("./LazyComponent"));

function App() {
  return (
    <div>
      <h1>My App</h1>
      <Suspense fallback={<div>Loading...</div>}>
        <LazyComponent />
      </Suspense>
    </div>
  );
}

export default App;
```

**Giải thích:**

- `React.lazy(() => import('./LazyComponent'))`: Tải component `LazyComponent` khi cần thiết.
- `Suspense`: Bao bọc `LazyComponent` và hiển thị nội dung trong prop `fallback` (ở đây là `<div>Loading...</div>`) trong khi component đang tải.

### Những điểm cần lưu ý

1.  **Không dùng với mọi API tải dữ liệu**: `Suspense` không hỗ trợ trực tiếp việc chờ các lời hứa (Promise) thông thường. Nó yêu cầu sử dụng thư viện hỗ trợ (như Relay) hoặc bạn cần tự xây dựng cơ chế throwing Promise.

2.  **Chỉ hoạt động trên client-side**: Trong các ứng dụng server-side rendering (SSR), bạn cần một cách tiếp cận khác để xử lý trạng thái chờ.

3.  **Concurrent Mode**: `Suspense` mạnh mẽ hơn khi kết hợp với Concurrent Mode, cho phép React tạm dừng và hiển thị các phần khác của giao diện trong khi chờ dữ liệu.
