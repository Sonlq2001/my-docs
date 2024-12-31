---
sidebar_position: 11
---

# KeepAlive

`keep-alive` là một **component tích hợp sẵn** (built-in component) được sử dụng để **lưu trạng thái** của các component con trong khi chuyển đổi giữa chúng ( lưu vào `cache` ).

Điều này giúp tránh việc phải khởi tạo lại component mỗi khi nó được hiển thị lại, từ đó cải thiện hiệu năng và giữ nguyên trạng thái của component.

### Cách hoạt động của `keep-alive`

- Khi một component được bọc trong `keep-alive`, Vue sẽ lưu trữ component đó vào bộ nhớ cache khi nó bị loại bỏ khỏi DOM thay vì phá hủy hoàn toàn.
- Khi component được hiển thị lại, Vue sẽ tái sử dụng component từ bộ nhớ cache thay vì tạo lại nó từ đầu.

```html
<template>
  <keep-alive>
    <my-component v-if="isToggle" />

    <button @click="isToggle = !isToggle">Toggle component</button>
  </keep-alive>
</template>

<script>
  import { ref } from "vue";

  const isToggle = ref(true);
</script>
```

### Khi nào sử dụng `keep-alive`

- Khi bạn muốn **giữ trạng thái của component** khi chuyển đổi qua lại giữa các component.
- Thường được dùng trong các ứng dụng có tính năng **routing**, ví dụ: `vue-router`, để lưu trạng thái của trang khi người dùng di chuyển qua lại giữa các trang.

### Thuộc tính của `keep-alive`

`keep-alive` hỗ trợ một số thuộc tính sau:

1.  **`include`**: Chỉ định các component được lưu trữ (bằng tên).
2.  **`exclude`**: Chỉ định các component không được lưu trữ.
3.  **`max`**: Giới hạn số lượng component được lưu trữ trong bộ nhớ cache.

```html
<template>
  <div>
    <button @click="current = TabTwo">TabTwo</button>
    <button @click="current = TabThree">TabThree</button>
  </div>
  <!-- Chỉ áp dụng cache với component TabThree -->
  <keep-alive :include="['TabThree']">
    <component :is="current" />
  </keep-alive>
</template>

<script setup>
  import { shallowRef } from "vue";
  import TabTwo from "./components/TabTwo.vue";
  import TabThree from "./components/TabThree.vue";

  const current = shallowRef(TabTwo);
</script>
```

- **`include`**: Chỉ lưu cache `TabThree`.

### Các hook liên quan

Khi sử dụng `keep-alive`, một số lifecycle hooks đặc biệt sẽ được kích hoạt:

- **`activated`**: Được gọi khi component được kích hoạt lại từ bộ nhớ cache.
- **`deactivated`**: Được gọi khi component bị đưa vào trạng thái không hoạt động và lưu trữ trong cache.

```html
<script>
  activated() {
    console.log('Component activated!');
  },
  deactivated() {
    console.log('Component deactivated!');
  },
</script>
```

### Lợi ích của `keep-alive`

1.  **Hiệu năng tốt hơn**: Giảm số lần khởi tạo component, đặc biệt hữu ích cho các component có logic phức tạp hoặc tải dữ liệu từ xa.
2.  **Trải nghiệm người dùng mượt mà hơn**: Giữ trạng thái giao diện (form, cuộn, v.v.) khi chuyển đổi qua lại giữa các trang.

### Khi không nên sử dụng

- Khi trạng thái hoặc dữ liệu của component không cần phải được lưu trữ lâu dài.
- Khi bạn cần đảm bảo rằng mỗi lần hiển thị lại là một trạng thái hoàn toàn mới.
