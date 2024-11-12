---
sidebar_position: 1
---

# memo

Cho phép bỏ qua việc render, khi các `props` nhận vào của thành phần đó không có sự thay đổi

```jsx
const MemoizedComponent = memo(Component, arePropsEqual?)
```

## Reference

### Parameters

`Component`

- Thành phần mà muốn áp dụng ghi nhớ. Bản ghi nhớ không sửa đổi thành phần này mà thay vào đó trả về một thành phần mới đã được ghi nhớ. Mọi thành phần React hợp lệ, bao gồm các hàm và thành phần ForwardRef, đều được chấp nhận.

`arePropsEqual (optional)`

- Một hàm chấp nhận hai đối số: `props trước đó` của thành phần và `props mới` của nó. Nó sẽ trả về `true` nếu props cũ và props mới bằng nhau: nghĩa là nếu thành phần đó sẽ hiển thị cùng một đầu ra và hoạt động theo cách tương tự với props mới cũng như với props cũ. Nếu không nó sẽ trả về `false`.

- Thông thường, bạn sẽ không chỉ định chức năng này. Theo mặc định, React sẽ so sánh từng prop với `Object.is`.

### Returns

Trả về một thành phần React mới. Nó hoạt động giống như thành phần được cung cấp cho bản ghi nhớ ngoại trừ việc React sẽ không luôn hiển thị lại nó khi thành phần gốc của nó được kết xuất lại trừ khi đạo cụ của nó đã thay đổi.

```jsx
import { memo } from "react";

const SomeComponent = memo(function SomeComponent(props) {
  // ...
});
```

## When to use memo

Bất cứ khi nào thành phần cha render lại, thì thành phần con cũng sẽ bị render lại theo. Sử dụng `memo` hợp lý sẽ mang lại hiệu năng tốt cho ứng dụng.

Có 1 số trường hợp sử dụng `memo`:

- Thành phần của bạn không nhận bất kì 1 `props` nào và đang được `import` để sử dụng ở thành phần cha. Để đảm bảo khi thành phần cha render sẽ không ảnh hưởng đến.

```jsx
import { useState } from "react";
import ShowMessage from "./ShowMessage";

export default function App() {
  const [count, setCount] = useState(1);

  return (
    <div className="App">
      <ShowMessage />
      <p>Count: {count}</p>
      <button onClick={() => setCount((prev) => prev + 1)}>Click</button>
    </div>
  );
}
```

```jsx
import { memo } from "react";

/*
- ShowMessage không nhận 1 props nào, dùng memo
- Để đảm bảo khi thành phần cha render sẽ không ảnh hưởng đến
*/

const ShowMessage = () => {
  return <div className="App">Show message</div>;
};

export default memo(ShowMessage);
```

- Kết hợp sử dụng `useMemo` và `useCallback` với `memo`. Cả 2 `hook` đó đều lưu giá trị vào bộ nhớ đệm trường hợp các phụ thuộc không thay đổi.
