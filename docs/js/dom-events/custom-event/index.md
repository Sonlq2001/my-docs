---
sidebar_position: 1
---

# Custom event

`Custom events` (sự kiện tùy chỉnh) là các sự kiện do người dùng hoặc lập trình viên tự định nghĩa và kích hoạt, thay vì sử dụng các sự kiện sẵn có như `click`, `mouseover`, hoặc `keydown`.

`Custom events` giúp bạn tạo ra cơ chế giao tiếp hoặc thông báo giữa các phần khác nhau trong ứng dụng.

## Tạo custom event

Sử dụng constructor `CustomEvent` để tạo một sự kiện tùy chỉnh.

```js
const event = new CustomEvent(eventName, eventDetail);
```

- `eventName`: Tên sự kiện (chuỗi).

- `eventDetail`: Một đối tượng chứa thông tin bổ sung mà bạn muốn truyền kèm với sự kiện (không bắt buộc).

```js
const myEvent = new CustomEvent("greeting", {
  detail: { message: "Hello, world!" },
});
```

## Lắng nghe custom event

Dùng phương thức `addEventListener` để lắng nghe sự kiện tùy chỉnh trên một phần tử hoặc đối tượng.

```js
document.addEventListener("greeting", (event) => {
  console.log(event.detail.message); // "Hello, world!"
});
```

## Kích hoạt custom event

Dùng phương thức `dispatchEvent` để kích hoạt sự kiện trên một phần tử hoặc đối tượng.

```js
document.dispatchEvent(myEvent);
```

### Ví dụ đầy đủ

```js
// Tạo sự kiện tùy chỉnh
const customEvent = new CustomEvent("customAlert", {
  detail: { message: "This is a custom event!" },
});

// Thêm trình nghe sự kiện
document.addEventListener("customAlert", (event) => {
  console.log("Custom event triggered:", event.detail.message);
});

// Kích hoạt sự kiện
document.dispatchEvent(customEvent);
```

- Khi sự kiện được kích hoạt, trình nghe (`event listener`) sẽ xử lý nó.

## Ưu điểm của custom events

- **Modular**: Giúp các thành phần (components) giao tiếp với nhau mà không cần phải gắn kết chặt chẽ.
- **Reusable**: Dễ dàng tái sử dụng logic sự kiện trong các phần khác của ứng dụng.
- **Tùy chỉnh cao**: Bạn có thể truyền dữ liệu bổ sung qua thuộc tính `detail`.

## Lưu ý

- Sự kiện tùy chỉnh không có hành vi mặc định (default behavior), nên bạn không cần gọi `preventDefault`.
- Chúng hoạt động trên bất kỳ đối tượng nào hỗ trợ `EventTarget`, chẳng hạn như `window`, `document`, hoặc các phần tử DOM.

:::info
**Custom events** thường được sử dụng trong việc phát triển ứng dụng web phức tạp, đặc biệt là khi bạn cần giao tiếp giữa các thành phần trong các framework như `React`, `Vue`, hoặc `Angular`.
:::

## Ví dụ về cách sử dụng trong React

Có thể viết 2 hàm dùng chung:

- `sendEvent`: gửi đi sự kiện
- `listenEvent`: lắng nghe sự kiện

```ts
type SendEvent<T> = {
  eventName: string;
  data: T;
};

type ListenEvent<T> = {
  eventName: string;
  handleEvent: (detail: T) => void;
};

const sendEvent = <T>({ eventName, data }: SendEvent<T>) => {
  document.dispatchEvent(new CustomEvent(eventName, { detail: data }));
};

const listenEvent = <T>({ eventName, handleEvent }: ListenEvent<T>) => {
  const listener = (event: Event) => {
    const customEvent = event as CustomEvent<T>;
    handleEvent(customEvent.detail);
  };

  document.addEventListener(eventName, listener);
  return () => document.removeEventListener(eventName, listener);
};

export { sendEvent, listenEvent };
```

**Sử dụng**

```tsx
// Lắng nghe sự kiện
useEffect(() => {
  const handle = listenEvent<{ name: string }>({
    eventName: "btn:click",
    handleEvent: (data) => {
      console.log(data.name); // keep going
    },
  });
  return handle;
}, []);
```

```tsx
// Gửi sự kiện
<button
  onClick={() => {
    sendEvent({
      eventName: "btn:click",
      data: { name: "keep going" },
    });
  }}
>
  Click
</button>
```
