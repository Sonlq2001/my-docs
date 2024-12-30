---
sidebar_position: 10
---

# Provide and Inject

`provide` và `inject` trong Vue 3 là cơ chế để chia sẻ dữ liệu giữa các component mà không cần phải truyền qua các cấp trung gian (props và emit).

Là một giải pháp hiệu quả khi bạn có một cấu trúc component phức tạp và cần chia sẻ dữ liệu giữa các thành phần không liên tiếp trong cây component.

![ex1](./images/ex1.png)

Khi sử dụng `provide` và `inject`:

- Có thể lấy trực tiếp dữ liệu từ component con, mà không phải thông qua bất cứ component trung gian nào hết.

![ex2](./images/ex2.png)

**Cách hoạt động của `provide` và `inject`**

- **`provide`**: Được sử dụng trong một component cha để cung cấp giá trị cho các component con.
- **`inject`**: Được sử dụng trong các component con để nhận giá trị từ component cha.

## provide

```html
<!-- Parent component -->
<template>
  <children-component />
</template>
<script>
  import { provide, reactive } from "vue";

  const listFruits = reactive([
    { name: "banana" },
    { name: "coconut" },
    { name: "watermelon" },
  ]);

  provide("listFruits", listFruits);
</script>
```

**Phạm vi chia sẻ**:

- `provide` cung cấp dữ liệu cho tất cả các component con trong cây của nó.
- Không cần truyền qua props ở các cấp trung gian.

## inject

```html
<!-- Children component -->
<template>
  <ul>
    <li v-for="fruit in listFruits" :key="fruit.name">{{fruit.name}}</li>
  </ul>
</template>
<script>
  import { inject } from "vue";

  const listFruits = inject("listFruits");
</script>
```

- Truyền đúng giá trị `key` (`listFruits`) mà `provide` đã cung cấp để nhận giá trị tương ứng.

- Nếu không tìm thấy giá trị `provide`, inject có thể sử dụng giá trị mặc định.

```js
inject("listFruits", []);
```

## provide/inject và các state management

| **Đặc điểm**         | **provide/inject**                          | **Vuex/Pinia**                           |
| -------------------- | ------------------------------------------- | ---------------------------------------- |
| **Mục đích**         | Chia sẻ dữ liệu giữa các component cụ thể.  | Quản lý trạng thái toàn cục.             |
| **Phạm vi sử dụng**  | Giới hạn trong cây component cụ thể.        | Áp dụng toàn bộ ứng dụng.                |
| **Phản ứng dữ liệu** | Cần dùng `ref` hoặc `reactive` để phản ứng. | Được tích hợp sẵn.                       |
| **Phức tạp**         | Đơn giản và nhẹ.                            | Cần thiết lập, nhiều tính năng phức tạp. |
