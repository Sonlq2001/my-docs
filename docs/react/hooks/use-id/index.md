---
sidebar_position: 7
---

# useId

`useId` là một **React Hook** cung cấp cách tạo **ID duy nhất** để sử dụng trong các component React.

Mục đích chính của `useId` là đảm bảo rằng mỗi ID được tạo là **duy nhất** và **ổn định** giữa các lần render, ngay cả khi render trên server (Server-Side Rendering - SSR).

## Cách hoạt động của `useId`

- **ID duy nhất**: `useId` tạo ra một chuỗi duy nhất cho mỗi component.
- **Ổn định**: ID được tạo ra bởi `useId` không thay đổi giữa các lần render.
- **SSR-friendly**: Khi render trên server, React đảm bảo rằng ID được tạo ra phù hợp để đồng bộ hóa với client, tránh lỗi "hydration mismatch".

```jsx
const id = useId();
```

- `id`: Một chuỗi ID duy nhất mà bạn có thể sử dụng trong DOM, thuộc tính, hoặc bất kỳ nơi nào yêu cầu định danh.

## **Khi nào nên dùng `useId`?**

- **Gắn ID vào các phần tử DOM**: Khi bạn cần một ID duy nhất để liên kết các phần tử trong HTML (ví dụ: `<label>` và `<input>`).

- **Tạo ID cho nhiều phần tử**: Trong danh sách hoặc các component động, bạn có thể cần tạo nhiều ID duy nhất.

- **Kết hợp với SSR**: `useId` đảm bảo rằng ID nhất quán giữa server và client, tránh lỗi "hydration".

```jsx
import React, { useId } from "react";

function FormField() {
  const id = useId(); // Tạo ID duy nhất
  return (
    <div>
      <label htmlFor={id}>Enter your name:</label>
      <input id={id} type="text" />
    </div>
  );
}

export default FormField;
```

**Tạo nhiều ID duy nhất trong danh sách**

```jsx
import React, { useId } from "react";

function ItemList() {
  const id = useId(); // Base ID duy nhất
  const items = ["Apple", "Banana", "Cherry"];

  return (
    <ul>
      {items.map((item, index) => (
        <li key={`${id}-${index}`}>{item}</li>
      ))}
    </ul>
  );
}

export default ItemList;
```

## Thêm `prefix`

```js
const root = createRoot(document.getElementById("root"), {
  identifierPrefix: "my-first-app-",
});
root.render(<App />);
```

## Ưu điểm

- **Đảm bảo duy nhất**:

  - ID được tạo bởi `useId` là duy nhất trong toàn bộ ứng dụng React.

- **Thân thiện với SSR**:

  - ID được đồng bộ giữa server và client, tránh lỗi "hydration mismatch".

- **Sử dụng dễ dàng**:

  - Không cần quản lý thủ công các ID hoặc sử dụng các thư viện bên ngoài như `uuid`.

- **Ổn định**:

  - ID không thay đổi giữa các lần render, giúp giảm thiểu lỗi liên quan đến trạng thái.

##  Hạn chế

- **Không dành cho mọi trường hợp**:

  - `useId` không thay thế các thư viện tạo ID ngẫu nhiên như `uuid` trong các trường hợp ID cần được lưu trữ hoặc gửi đến server.

- **Không linh hoạt cho việc tùy chỉnh**:

  - ID được tạo theo một định dạng cố định, không phù hợp nếu bạn cần các ID có cấu trúc đặc biệt.

- **Không dành cho dữ liệu bên ngoài**:

  - Nếu bạn cần ID để định danh dữ liệu từ server, `useId` không phù hợp. Trong trường hợp đó, bạn nên sử dụng ID từ server hoặc tự tạo.
