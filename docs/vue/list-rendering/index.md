---
sidebar_position: 6
---

# List Rendering

## v-for

Là một `directive` trong Vue.js dùng để lặp qua một mảng (`array`), một đối tượng (`object`), hoặc một số nguyên để render danh sách các phần tử.

### Lặp với `object`

```html
<template>
  <li v-for="(value, key, index) in user" :key="index">
    {{ key }}: {{ value }}
  </li>
</template>

<script>
  import { reactive } from "vue";

  const user = reactive({
    name: "John Doe",
    age: 30,
    email: "john@example.com",
  });
</script>
```

Kết quả

```bash
name: John Doe
age: 30
email: john@example.com
```

### Lặp với `số nguyên`

```html
<ul>
  <li v-for="n in 5" :key="n">Item {{ n }}</li>
</ul>
```

Kết quả

```bash
Item 1
Item 2
Item 3
Item 4
Item 5
```

### Lặp với `Component`

```jsx
<MyComponent v-for="item in items" :key="item.id" />
```

Muốn truyển dữ liệu xuống `Component` cần sử dụng `props`

```jsx
<MyComponent
  v-for="(item, index) in items"
  :item="item"
  :index="index"
  :key="item.id"
/>
```

### Sử dụng thuộc tính `key` trong `v-for`

#### **Tại sao cần dùng `key`?**

- `key` giúp Vue xác định duy nhất mỗi phần tử trong danh sách.
- Điều này giúp cải thiện hiệu suất render vì Vue có thể theo dõi chính xác những phần tử nào đã thay đổi, thêm, hoặc xóa.

#### **Cách sử dụng `key`:**

- Giá trị của `key` thường là một giá trị duy nhất như ID hoặc chỉ số (index).
- Tốt nhất nên sử dụng một thuộc tính duy nhất

## v-for với v-if

Có thể kết hợp `v-for` với `v-if`, nhưng cần chú ý về thứ tự ưu tiên:

- Khi chúng tồn tại trên cùng một nút, `v-if` **có mức độ ưu tiên cao hơn** `v-for`. Điều đó có nghĩa là điều kiện `v-if` sẽ không có quyền truy cập vào các biến trong phạm vi của `v-for`
- Nên sử dụng `computed` để lọc danh sách thay vì lồng ghép.

```html
<!-- Không nên sử dụng, item.active sẽ báo lỗi -->
<ul>
  <li v-for="item in items" v-if="item.active" :key="item.id">
    {{ item.name }}
  </li>
</ul>

<!-- Nên sử dụng -->
<ul>
  <li v-for="item in activeItems" :key="item.id">{{ item.name }}</li>
</ul>

<!-- Hoặc -->
<template v-for="item in items">
  <li v-if="item.active">{{ item.name }}</li>
</template>

<script>
  import { computed, reactive } from "vue";

  const items = reactive([
    { name: 1, active: true },
    { name: 2, active: false },
    { name: 3, active: true },
  ]);

  const activeItems = computed(() => {
    return items.filter((item) => item.active);
  });
</script>
```

## Điều cần tránh khi dùng `v-for`

1.  **Không quên thuộc tính `key`:**

    - Nếu không có `key`, Vue có thể gặp khó khăn khi tối ưu hóa hiệu suất.

2.  **Không sử dụng chỉ số làm `key` nếu không cần thiết:**

    - Sử dụng chỉ số (`index`) làm `key` có thể dẫn đến kết quả không mong muốn khi dữ liệu thay đổi.

3.  **Tránh lồng quá nhiều vòng `v-for`:**

    - Việc lồng `v-for` phức tạp có thể gây khó hiểu và giảm hiệu suất. Hãy cân nhắc tái cấu trúc dữ liệu để đơn giản hóa.
