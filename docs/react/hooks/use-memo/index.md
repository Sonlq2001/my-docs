---
sidebar_position: 4
---

# useMemo

Là một React Hook cho phép bạn lưu trữ kết quả tính toán giữa các lần kết xuất lại.

```jsx
const cachedValue = useMemo(calculateValue, dependencies);
```

## Reference

### Parameters

`calculateValue`:

- Là 1 hàm tính toán mà muốn lưu vào bộ nhớ đệm, hàm phải thuần túy không có đối số và phải trả về 1 giá trị bất kỳ.

- Trong lần render đầu tiên hàm sẽ được gọi. Lần kết xuất tiếp theo, React sẽ trả về cùng một giá trị nếu phần phụ thuộc không thay đổi kể từ lần kết xuất cuối cùng.

- Nếu không, nó sẽ gọi hàm `CalculateValue`, trả về kết quả và lưu trữ để có thể sử dụng lại sau này.

`dependencies`

- Danh sách tất cả các giá trị được tham chiếu bên trong mã `CalculateValue`

- React sẽ so sánh từng phần phụ thuộc với giá trị trước đó của nó bằng cách sử dụng phép so sánh `Object.is`.

```jsx
const cachedValue = useMemo(() => {
  // logic calculator
  return value;
}, [dep1, dep2, dep3 ...]);
```

### Returns

Trong lần đầu sẽ trả về kết quả của việc gọi hàm `CalculateValue`.

Trong mỗi lần kết xuất tiếp theo, React sẽ so sánh các phần phụ thuộc với các phần phụ thuộc mà bạn đã chuyển trong lần kết xuất gần đây nhất. Nếu không có phần phụ thuộc nào thay đổi (so với `Object.is`), useMemo sẽ trả về giá trị bạn đã tính toán trước đó. Nếu không, React sẽ chạy lại phép tính của bạn và trả về giá trị mới.

useMemo lưu trữ kết quả tính toán giữa các lần hiển thị lại cho đến khi các phần phụ thuộc của nó thay đổi.

> Giá trị được trả về từ `useMemo` sẽ được lưu vào bộ nhớ đệm.

## When to use useMemo

`useMemo` chỉ có giá trị trong một số trường hợp

- Quá trình tính toán ghi nhớ chậm đáng kể và các yếu tố phụ thuộc của nó hiếm khi thay đổi.

- Khi truyền giá trị đang dùng `useMemo` sang 1 component khác dưới dạng `props` và component nhận được `props` đó được bọc bởi `memo`. Muốn bỏ qua việc hiển thị lại nếu giá trị không thay đổi. Tính năng ghi nhớ cho phép thành phần của bạn chỉ hiển thị lại khi các phần phụ thuộc không giống nhau.

```jsx
const result = useMemo(() => {
  return value
},[dep1, dep2...])

<Component result={result} />
```

```jsx
import { memo } from "react";

const Component = ({ result }) => {
  return <div></div>;
};

export default memo(Component);
```

- Giá trị bạn truyền sau này được sử dụng làm phần phụ thuộc của một số Hook khác.
