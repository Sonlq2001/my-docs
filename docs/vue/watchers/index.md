---
sidebar_position: 7
---

# Watchers

Watchers dùng để lắng nghe và phản ứng khi giá trị của một `reactive state` hoặc `computed property` thay đổi.

Cần thực hiện một tác vụ phụ thuộc vào sự thay đổi của dữ liệu

Vue 3 cung cấp 2 cách chính để sử dụng Watchers:

- **`watch` API**
- **`watchEffect` API**

## watch

- `watch` lắng nghe một hoặc nhiều **reactive state** (hoặc **ref/computed**) và thực thi một callback mỗi khi giá trị thay đổi.

```js
import { watch } from "vue";

const count = ref(0);

watch(count, (newValue, oldValue) => {
  console.log(`Giá trị thay đổi từ ${oldValue} thành ${newValue}`);
});
```

- **Target:** Biến hoặc getter reactive cần lắng nghe.
- **Callback:** Hàm thực thi mỗi khi giá trị thay đổi.

  - `newValue`: Giá trị mới.
  - `oldValue`: Giá trị cũ.

- **Options**: Các tùy chọn

**Theo dõi nhiều giá trị bằng cách sử dụng 1 mảng.**

```js
const firstName = ref("John");
const lastName = ref("Doe");

watch([firstName, lastName], ([newFirst, newLast], [oldFirst, oldLast]) => {
  console.log(
    `Tên thay đổi: ${oldFirst} -> ${newFirst}, ${oldLast} -> ${newLast}`
  );
});
```

### Các options trong watch

#### `immediate`

Thực thi callback ngay lập tức khi watch được thiết lập.

```js
watch(count, (newValue) => console.log(`Giá trị hiện tại: ${newValue}`), {
  immediate: true,
});
```

#### `deep`

Theo dõi các thay đổi sâu trong đối tượng hoặc mảng (theo mặc định, Vue chỉ theo dõi cấp đầu tiên).

```js
const user = ref({ name: "Alice", age: 25 });

watch(user, (newValue) => console.log("Thông tin user thay đổi:", newValue), {
  deep: true,
});
```

#### `once`

Theo dõi các thay đổi chỉ **1 lần duy nhất**.

```js
watch(
  source,
  (newValue, oldValue) => {
    // when `source` changes, triggers only once
  },
  { once: true }
);
```

#### `flush`

Kiểm soát thời điểm callback được thực thi:

- `pre` (mặc định): Thực hiện trước khi DOM cập nhật.
- `post`: Thực hiện sau khi DOM cập nhật.
- `sync`: Thực hiện đồng bộ ngay lập tức.

## watchEffect

`watchEffect` tự động theo dõi tất cả các `reactive dependencies` trong hàm callback mà không cần chỉ định rõ ràng.

```js
import { ref, watchEffect } from "vue";

const count = ref(0);

watchEffect(() => {
  console.log(`Giá trị hiện tại của count là: ${count.value}`);
});
```

- Không cần khai báo `target`, Vue tự động xác định các reactive dependencies bên trong hàm callback.

:::info
Chỉ theo dõi các phần phụ thuộc trong quá trình thực thi đồng bộ của nó. Khi sử dụng nó với lệnh gọi lại không đồng bộ, chỉ các thuộc tính được truy cập trước `await` đầu tiên mới được theo dõi.
:::

## watch với watchEffect

| **Đặc điểm**            | **`watch`**                               | **`watchEffect`**               |
| ----------------------- | ----------------------------------------- | ------------------------------- |
| **Khai báo target**     | Phải chỉ định rõ biến reactive            | Tự động theo dõi dependencies   |
| **Truy cập giá trị cũ** | Có (qua `oldValue`)                       | Không                           |
| **Thích hợp dùng**      | Khi cần so sánh giá trị mới và giá trị cũ | Khi theo dõi phụ thuộc đơn giản |

## cleanup

Khi sử dụng **`watch`** hoặc **`watchEffect`**, Vue cung cấp cơ chế **dọn dẹp (cleanup)** để đảm bảo rằng các tài nguyên hoặc hiệu ứng phụ (side effects) không cần thiết sẽ được giải phóng khi watcher hoặc effect bị kích hoạt lại hoặc bị huỷ

- `onCleanup`

```js
watch(id, (newId, oldId, onCleanup) => {
  // ...
  onCleanup(() => {
    // cleanup logic
  });
});

watchEffect((onCleanup) => {
  // ...
  onCleanup(() => {
    // cleanup logic
  });
});
```

#### Cách hoạt động:

- `onCleanup` được sử dụng để thực hiện các thao tác dọn dẹp khi watcher được kích hoạt lại (do sự thay đổi của dependencies) hoặc khi component bị huỷ (destroyed).
- Thích hợp để dọn dẹp các tài nguyên như:
  - Bộ hẹn giờ (timers).
  - Lắng nghe sự kiện (event listeners).
  - Kết nối với API hoặc WebSocket.

```js
import { ref, watchEffect } from "vue";

const count = ref(0);

watchEffect((onCleanup) => {
  const interval = setInterval(() => {
    console.log(`Count hiện tại: ${count.value}`);
  }, 1000);

  // Dọn dẹp khi watcher bị kích hoạt lại
  onCleanup(() => {
    clearInterval(interval);
    console.log("Interval đã được dọn dẹp");
  });
});
```

**Cách hoạt động**:

1.  Khi `count.value` thay đổi, `watchEffect` sẽ kích hoạt lại.
2.  Trước khi thực thi lại logic, Vue gọi hàm `onCleanup` để dọn dẹp tài nguyên.

### Tại sao cần `onCleanup`?

1.  **Quản lý hiệu suất**:

    - Dọn dẹp tài nguyên không cần thiết để tránh rò rỉ bộ nhớ.
    - Tránh giữ các tham chiếu không còn được sử dụng.

2.  **Quản lý logic phức tạp**:

    - Hỗ trợ hủy các tác vụ dài hạn hoặc không đồng bộ (như `fetch`, `setInterval`, `WebSocket`).
