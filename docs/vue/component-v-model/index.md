---
sidebar_position: 9
---

# Component v-model

`v-model` là một cú pháp rút gọn để tạo hai chiều dữ liệu (two-way data binding) giữa một thuộc tính trong component cha và component con.

`v-model` cung cấp khả năng đồng bộ dữ liệu hai chiều giữa:

1.  Một thuộc tính trong component cha.
2.  Một giá trị trong component con.

#### **Cách hoạt động cơ bản**

- Trong **component cha**, bạn sử dụng `v-model` để liên kết với một thuộc tính.
- Trong **component con**, bạn sử dụng `props` để nhận giá trị và `emit` để thông báo cập nhật giá trị đó.

## `v-model` làm việc với các thẻ trong form

`v-model` là một cú pháp được tối ưu hóa cho các thẻ HTML như `input`, `textarea`, và `select`...

Vue tự động đồng bộ giữa giá trị nhập từ người dùng và giá trị lưu trữ `state` khởi tạo.

```html
<template>
  <input type="email" v-model="email" />

  <button @click="email = 'default@gmail.com'">Default email</button>
</template>

<script>
  import { ref } from "vue";
  const email = ref("");
</script>
<!-- Khi dùng v-model giá trị giữa ô input và giá trị email trong ref sẽ luôn đồng bộ với nhau -->
```

- Khi người dùng nhập dữ liệu vào thẻ `<input>`, giá trị `email` sẽ tự động được cập nhật.
- Vue xử lý sự kiện `input` cho `input`/`textarea` và sự kiện `change` cho `select` để cập nhật giá trị.

## `v-model` với Component

Khi sử dụng `v-model` với một **component**, bạn cần định nghĩa cách component xử lý giá trị và thông báo khi có sự thay đổi.

Trong Vue 3, `v-model` mặc định liên kết với thuộc tính `modelValue` và sự kiện `update:modelValue`.

```html
<!-- Parent component -->
<template>
  <children-component v-model="count" />
</template>

<script>
  import { ref } from "vue";
  const count = ref(0);
</script>
```

```html
<!-- Children component -->
<template>
  <h2>{{ props.modelValue }}</h2>
  <button @click="handleUpdateCount">Click</button>
</template>

<script>
  const emit = defineEmits<{
    (eventName: "update:modelValue", payload: number): void;
  }>();

  const props = definedProps();

  const handleUpdateCount = () => {
    emit("update:modelValue", props.modelValue + 1);
  };
</script>
```

- Khi thực hiện bấm `click` giá trị `count` sẽ thay đổi, giá trị `count` sẽ được đồng bộ 2 chiều:
  - `Component cha` thực hiện truyền dữ liệu xuống `Component con`.
  - `Component con` thay đổi giữ liệu và `Component cha` cũng cập nhập theo dữ liệu.

### `defineModel`

Trong Composition API, có thể sử dụng `defineModel` để định nghĩa và xử lý `v-model` trực tiếp trong setup mà không cần phải cấu hình `props` và `emit`.

```html
<!-- Parent component -->
<template>
  <children-component v-model="count" />
</template>

<script>
  import { ref } from "vue";
  const count = ref(0);
</script>
```

```html
<!-- Children component -->
<template>
  <h2>{{ count }}</h2>
  <button @click="handleUpdateCount">Click</button>
</template>

<script>
  const count = defineModel();
  const handleUpdateCount = () => {
    count.value += 1;
  };
</script>
```

#### Sử dụng nhiều `v-model` trong component

```html
<!-- Parent component -->
<script setup>
  import { ref } from "vue";

  const name = ref("");
  const email = ref("");
</script>

<template>
  <children-component v-model:name="name" v-model:email="email" />
</template>
```

```html
<!-- Children component -->
<script setup>
  const name = defineModel("name", {
    type: String,
  });
  const email = defineModel("email", {
    type: String,
  });
</script>

<template>
  <input type="text" v-model="name" />
  <input type="text" v-model="email" />
</template>
```

**Hoặc có thể sử dụng 1 object để gộp nhiều state lại**

```html
<!-- Parent component -->
<script setup>
  import { reactive } from "vue";
  const info = reactive({
    name: "",
    email: "",
  });
</script>

<template>
  <children-component v-model="info" />
</template>
```

```html
<!-- Children component -->
<script setup>
  const info = defineModel({
    type: Object,
  });
</script>

<template>
  <input type="text" v-model="info.name" />
  <input type="text" v-model="info.email" />
</template>
```
