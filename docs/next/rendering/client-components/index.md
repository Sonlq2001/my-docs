# Client Component

Cho phép viết giao diện người dùng tương tác được hiển thị trước trên máy chủ và có thể sử dụng JavaScript máy khách để chạy trong trình duyệt. ( Kết xuất giao diện phía client )

### Benefits of Client Rendering

- `Interactivity`: có thể sử dụng được các hook, side effect của react, hiệu ứng và sự kiện, tương tác phản hồi trực tiếp với người dùng.
- `Browser APIs`: có quyền truy cập vào API trình duyệt ( `localStorage, sessionStorage` )

### Using Client Components in Next.js

Thêm `"use client"` vào đầu tệp tin, phía trên các mục nhập của bạn. Được sử dụng để phân biệt giữa các thành phần `Client component ( "use client" )` và `Server Component ( "use server" )`

```tsx
"use client";
// Khai báo "use client"

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

:::tip[Lưu ý]
Có thể thêm nhiều `"use client"` trong thành phần React, cho phép chia nhỏ ứng dụng thành nhiều Client component.

> Khi dùng các `hook` trong React, truy cập `localStorage` bắt bược phải thêm `"use client"`, nếu không sẽ bị lỗi.

:::

### Client Components Rendered ?

:::info[Thông tin thêm]
Hydrat hóa là quá trình gắn trình xử lý sự kiện vào DOM để làm cho HTML tĩnh có tính tương tác
:::

1. Lần render đầu tiên sẽ được render phía server.
2. Thực thiện hydration trên Client, quá trình này gắn thêm các logic, event JavaScript, vào phần HTML tĩnh đã render sẵn.
3. Sau khi hydration hoàn tất, người dùng có thể tương tác với component, như thay đổi state, gửi form, click, v.v
4. Các lần render tiếp theo phía client sẽ chịu trách nghiệm.
