---
sidebar_position: 5
---

# useCallback

Là một React Hook cho phép bạn lưu vào bộ nhớ đệm định nghĩa hàm giữa các lần kết xuất lại.

```jsx
const cachedFn = useCallback(fn, dependencies);
```

## Reference

### Parameters

`fn`

- Giá trị hàm mà bạn muốn lưu vào bộ nhớ đệm. Có thể nhận bất kỳ đối số nào và trả về bất kỳ giá trị nào.

- React sẽ trả lại (không phải gọi!) chức năng của bạn cho bạn trong lần kết xuất đầu tiên.

  > Mỗi khi render, `Function` luôn tạo ra 1 context mới, địa chỉ mới cho ô nhớ.

- Các lần render tiếp theo, nếu các phụ thuộc không thay đổi kể từ lần render cuối cùng, React sẽ trả lại chức năng tương tự (`địa chỉ hàm đã ghi nhớ`).

- Nếu không, nó sẽ cung cấp cho bạn chức năng mà bạn đã truyền trong quá trình kết xuất hiện tại và lưu trữ nó trong trường hợp nó có thể được sử dụng lại sau này

- Hàm này được trả về cho bạn để bạn có thể quyết định khi nào và có nên gọi nó hay không.

`dependencies`

- Danh sách tất cả các giá trị được tham chiếu bên trong `useCallback`

- React sẽ so sánh từng phần phụ thuộc với giá trị trước đó của nó bằng cách sử dụng phép so sánh `Object.is`.

```jsx
const myFunction = useCallback((value) => {
  console.log(value); // hello world
}, [dep1, dep2, dep3 ...]);

myFunction('hello world'); // call function
```

### Returns

- Trong lần hiển thị đầu tiên, useCallback trả về hàm fn mà bạn đã chuyển.

- Trong các lần kết xuất tiếp theo, nó sẽ trả về hàm fn đã được lưu trữ từ lần kết xuất cuối cùng (nếu phần phụ thuộc không thay đổi) hoặc trả về hàm fn mà bạn đã chuyển trong lần kết xuất này.

## When to use useCallback

`useCallback` chỉ có giá trị trong một số trường hợp

- Khi truyền 1 hàm đang sử dụng `useCallback`, sang 1 component khác dưới dạng `props` và component nhận được `props` đó được bọc bởi `memo`. Muốn bỏ qua việc hiển thị lại nếu giá trị không thay đổi. Tính năng ghi nhớ cho phép thành phần của bạn chỉ hiển thị lại khi các phần phụ thuộc không giống nhau.

```jsx
const myFunction = useCallback(() => {},[dep1, dep2...])

<Component function={myFunction} />
```

```jsx
import { memo } from "react";

const Component = ({ function }) => {
  return <div></div>
};

export default memo(Component);
```

- Hàm bạn đang truyền sau này được sử dụng như một phần phụ thuộc của một số Hook

## Practice

### Optimizing a custom Hook

Nếu bạn đang viết một Hook tùy chỉnh, bạn nên gói bất kỳ hàm nào mà nó trả về `useCallback`

```jsx
function useRouter() {
  const { dispatch } = useContext(RouterStateContext);

  const navigate = useCallback(
    (url) => {
      dispatch({ type: "navigate", url });
    },
    [dispatch]
  );

  const goBack = useCallback(() => {
    dispatch({ type: "back" });
  }, [dispatch]);

  return {
    navigate,
    goBack,
  };
}
```
