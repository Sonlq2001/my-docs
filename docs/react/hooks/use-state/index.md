---
sidebar_position: 1
---

# useState

```jsx
const [state, setState] = useState(initialState);
```

Là 1 `Hook` cho phép thêm các biến trạng thái vào trong thành phần.

## Reference

Phải gọi `useState` ở cấp cao nhất của thành phần để khai báo biến trạng thái.

```jsx
import { useState } from 'react';

function MyComponent() {
  const [name, setName] = useState('Taylor');
  // ...
```

> Quy ước là đặt tên các biến trạng thái như [something, setSomething] bằng cách sử dụng cấu trúc mảng.

### Parameters

`initialState` có thể truyền bất cứ giá trị nào làm giá trị khở tạo cho `state`

Nếu giá trị khởi tạo là 1 hàm, hàm đó phải thuần túy, không nhận đối số truyền vào và phải trả về giá trị.

```jsx
const [name, setName] = useState(() => {
  return "hello";
});
```

### Returns

`useState` trả về 1 mảng chứa 2 giá trị, dùng `array destructuring` để lấy.

```jsx
const [myString, setMyString] = useState("hello");
```

- giá trị đầu sẽ đại diện cho giá trị hiện tại của `state`. Trong lần đầu `render` sẽ là giá trị khởi tạo. (Ở đây sẽ là `hello`).
- giá trị thứ 2 là 1 `Function` cho phép bạn cập nhập giá trị trạng thái và `kích hoạt render lại`.

### set functions, like setSomething(nextState)

```jsx
const [name, setName] = useState('Edward');
const [sage, setAge] = useState(1);

function handleClick() {
  setName('Taylor');
  setAge(a => {
    // a = 1
    return a + 1;
  });
  // ...
```

Có thể truyền giá trị mới vào luôn trong hàm `set`, hoặc truyền 1 hàm tính toán trả về giá trị

React sẽ lưu trữ trạng thái tiếp theo, hiển thị lại thành phần của bạn với các giá trị mới và cập nhật giao diện người dùng.

**Lưu ý** đối số của hàm là giá trị trước của `state`

Nếu giá trị `set` trùng với giá trị hiện tại, sẽ bỏ qua việc hiển thị lại thành phần và các thành phần con của nó. Đây là một sự tối ưu hóa.

```jsx
const [sage, setAge] = useState(1);
setAge(1); // bỏ qua việc set và render lại
```

:::warning Lưu ý
Việc hiển thị giá trị ngay sau hàm `set` sẽ không nhận được giá trị mới nhất.

```jsx
const [age, setAge] = useState(42);

function handleClick() {
  setAge(50);
  console.log(age); // 42
}
```

:::

## Usage

### Updating state based on the previous state

```jsx
const [count, setCount] = useState(1);

const handleSetCount = () => {
  setCount(count + 1);
  setCount(count + 1);
  setCount(count + 1);
};
```

Giả sử đang thực hiện `set` 3 lần cho biến `count`.

Tuy nhiên sau mỗi lần `click` `setCount` giá trị `count` sẽ chỉ là `2` chứ không phải `4`. Điều này là do việc gọi hàm `set` không cập nhật biến trạng thái trong mã đã chạy.

Để giải quyết vấn đề, sử dụng hàm để cập nhập thay vì trạng thái tiếp theo.

```jsx
const handleSetCount = () => {
  setCount((prev) => prev + 1); // setAge(1 => 1 + 1) // 2
  setCount((prev) => prev + 1); // setAge(2 => 2 + 1) // 3
  setCount((prev) => prev + 1); // setAge(3 => 3 + 1) // 4
};
```

React đặt các chức năng cập nhật của bạn vào hàng đợi. Sau đó, trong lần kết xuất tiếp theo, nó sẽ gọi chúng theo cùng thứ tự

Không có bản cập nhật được xếp hàng đợi nào khác, vì vậy cuối cùng React sẽ lưu trữ `4` làm trạng thái hiện tại.

### Updating objects and arrays in state

Đối với dữ liệu là mảng hay object, sẽ không thể cập nhập theo cách thông thường, mà sẽ phải dùng hàm `set`

```jsx
const [object, setObject] = useState({ text: "hello" });
object.text = "hello world"; // không hợp lệ

setObject({ ...object, text: "hello world" }); // hợp lệ
```

:::info Thông tin

> Phải detructuring dữ liệu hiện tại trước khi set để đảm bảo những trường dữ liệu không được set sẽ vẫn giữ nguyên giá trị.

```jsx
setObject({ ...object, text: "hello world" }); // ...object
```

:::

### Avoiding recreating the initial state

React lưu trạng thái ban đầu một lần và bỏ qua nó trong lần hiển thị tiếp theo.

```jsx
const [todos, setTodos] = useState(createInitialTodos());
// truyền kết quả được hàm trả về, vì đang thực hiện gọi hàm ()
```

Mặc dù kết quả của `createInitialTodos()` chỉ được sử dụng cho lần kết xuất đầu tiên nhưng bạn vẫn gọi hàm này trên mỗi lần kết xuất. Dẫn đến mã kém và giảm hiệu năng.

Để giải quyết, sẽ truyền dưới dạng hàm tạo `createInitialTodos`

```jsx
const [todos, setTodos] = useState(createInitialTodos);
// truyền dưới dạng hàm tạo vì không gọi hàm
```

### Resetting state with a key

`key` sẽ thường được sử dụng trong danh sách, nhưng cũng được sử dụng trong vài mục đích khác:

Bạn có thể đặt lại trạng thái của thành phần bằng cách chuyển một khóa khác cho thành phần đó.

```jsx
const [version, setVersion] = useState(0);

<Form key={version} />;

// version thay đổi thì dữ liệu trong Form sẽ bị reset lại
```

### Storing information from previous renders
