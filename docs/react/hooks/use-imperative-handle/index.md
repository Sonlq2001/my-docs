---
sidebar_position: 8
---

# useImperativeHandle

`useImperativeHandle` là một **React Hook** được sử dụng để tùy chỉnh giá trị tham chiếu (`ref`) được exposed (công khai) từ một component con đến component cha.

Nó đặc biệt hữu ích khi bạn muốn kiểm soát các hành vi hoặc thuộc tính cụ thể của một component con mà không làm lộ toàn bộ DOM hoặc component nội bộ.

## Cách hoạt động

- Mặc định, khi sử dụng **`ref`**, React trả về **thành phần DOM gốc** hoặc **instance của một class component**.
- `useImperativeHandle` cho phép bạn kiểm soát những gì được exposed khi một `ref` được truyền đến một **functional component**.
- Hook này được sử dụng kết hợp với `React.forwardRef` để truyền `ref` từ cha xuống con.

## Cú pháp

```jsx
useImperativeHandle(ref, createHandle, [dependencies]);
```

- **`ref`**: Tham chiếu (ref) được truyền từ component cha thông qua `React.forwardRef`.
- **`createHandle`**: Một hàm trả về đối tượng mà bạn muốn expose (công khai).
- **`dependencies`** _(tùy chọn)_: Mảng phụ thuộc để kiểm soát khi nào đối tượng được cập nhật.

## Khi nào nên dùng `useImperativeHandle`?

`useImperativeHandle` được sử dụng khi:

- Bạn cần cung cấp các phương thức hoặc thuộc tính tùy chỉnh từ component con để component cha sử dụng.
- Bạn muốn hạn chế hoặc điều chỉnh quyền truy cập vào các thuộc tính bên trong của component con.

```jsx
import React, { useRef, useImperativeHandle, forwardRef } from "react";

// Component con
const CustomInput = forwardRef((props, ref) => {
  const inputRef = useRef();

  // Tùy chỉnh giá trị được exposed qua ref
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    },
    clear: () => {
      inputRef.current.value = "";
    },
  }));

  return <input ref={inputRef} {...props} />;
});

// Component cha
function App() {
  const inputRef = useRef();

  return (
    <div>
      <CustomInput ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>Focus Input</button>
      <button onClick={() => inputRef.current.clear()}>Clear Input</button>
    </div>
  );
}

export default App;
```

- `CustomInput` sử dụng useImperativeHandle để expose hai phương thức focus và clear thay vì expose toàn bộ DOM của `<input>`
- `App` (component cha) có thể gọi các phương thức này thông qua ref.

## Ưu điểm của `useImperativeHandle`

- **Kiểm soát quyền truy cập**:

  - Cho phép bạn expose chỉ các thuộc tính hoặc phương thức cần thiết, giúp bảo vệ tính đóng gói (encapsulation) của component.

- **Tích hợp với DOM**:

  - Dễ dàng cung cấp các phương thức hoặc hành vi tương tác trực tiếp với DOM (như focus, scroll, v.v.).

- **Linh hoạt**:

  - Bạn có thể expose các logic phức tạp hoặc trạng thái bên trong của component con mà không cần thay đổi cấu trúc component.

## Hạn chế

- **Chống lại triết lý React**:

  - React hướng đến cách tiếp cận **declarative** (khai báo), trong khi `useImperativeHandle` thiên về **imperative** (mệnh lệnh). Sử dụng không đúng cách có thể làm phức tạp ứng dụng.

- **Phức tạp hơn `ref` thông thường**:

  - Đối với các trường hợp đơn giản, sử dụng trực tiếp `ref` là đủ. Sử dụng `useImperativeHandle` có thể không cần thiết.

- **Phụ thuộc vào `React.forwardRef`**:

  - Bạn phải bọc component con bằng `React.forwardRef`, điều này có thể gây khó hiểu cho người mới.
