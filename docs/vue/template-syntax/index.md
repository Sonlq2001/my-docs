---
sidebar_position: 1
---

# Template Syntax

Template Syntax là cách Vue.js cho phép bạn định nghĩa giao diện HTML và kết nối dữ liệu với giao diện một cách dễ dàng. Vue.js sử dụng cú pháp dựa trên HTML với các biểu thức (expressions) và chỉ thị (directives) để kết nối dữ liệu từ thành phần (component) vào giao diện.

## Text Interpolation

Dùng để chèn dữ liệu vào giao diện HTML.

- Sử dụng cú pháp `{{ }}` để hiển thị dữ liệu từ thành phần Vue.
- Kết quả tự động cập nhật khi dữ liệu thay đổi.

```vue
<template>
  <p>{{ message }}</p>
</template>

<script>
export default {
  data() {
    return { message: "Hello, Vue!" };
  },
};
</script>
```

## Attribute Bindings

Vue.js cung cấp directive v-bind để liên kết (bind) thuộc tính với dữ liệu.

```bash
v-bind:attribute="expression"

# Viết ngắn gọn

:attribute="expression"
```

- **attribute**: Là thuộc tính HTML mà bạn muốn gắn dữ liệu (ví dụ: `href`, `src`, `class`, `style`, v.v.).
- **expression**: Là một biểu thức JavaScript hoặc giá trị từ data/component.

```vue
<template>
  <button :disabled="isDisabled">Click me</button>
  <img :src="imageUrl" alt="Example Image" />

  <div v-bind="{ id: dynamicId, class: dynamicClass }">Hello</div>
</template>

<script setup>
import { ref } from "vue";

const id = ref("id-vue");
const className = ref("className");
const imageUrl = ref("url");
const isDisabled = ref(true);
</script>
```

## Directives

Directives trong Vue.js là các thuộc tính đặc biệt được thêm vào các thẻ HTML để cung cấp chức năng hoặc logic động. Chúng cho phép bạn thao tác trực tiếp với DOM dựa trên dữ liệu hoặc trạng thái của Vue instance/component.

Directives được bắt đầu bằng từ khóa `v-` trong Vue.js. Mỗi directive có một mục đích cụ thể.

- `v-bind`
- `v-on`
- `v-if`
- `v-model`
- ...

```vue
<template>
  <a v-bind:href="url">Visit Vue.js</a>
  <a v-if="true"> Display content </a>
  <a v-on:click="handleClick"> Display content </a>
  <li v-for="(item, index) in items" :key="index">{{ item }}</li>
</template>

<script setup>
import { ref } from "vue";

const url = ref("url");
const items = ref(["Vue", "React", "Angular"]);
const handleClick = () => {
  // click
};
</script>
```
