---
sidebar_position: 8
---

# Props and Events

## Props

`props` là một cơ chế để truyền dữ liệu từ parent component (component cha) sang child component (component con).

Chúng được sử dụng để thiết lập `giao tiếp một chiều`, từ cha đến con,

### defineProps

`defineProps` là một API đặc biệt chỉ dùng trong **Composition API** với `script setup`. Nó được sử dụng để định nghĩa props trực tiếp trong phần `<script setup>`.

- **Cú pháp cơ bản**:

```js
defineProps({
  propName: {
    type: DataType,
    default: DefaultValue,
    required: Boolean,
  },
});
```

- **Truyền kiểu đơn giản**: Nếu chỉ cần định nghĩa kiểu dữ liệu, bạn có thể truyền trực tiếp dưới dạng một mảng:

```js
defineProps(["title", "count"]);
```

#### Các thuộc tính trong cấu hình props:

1.  **type**: Kiểu dữ liệu của prop (String, Number, Boolean, Array, Object, ...).
2.  **required**: Xác định prop có bắt buộc hay không (`true` hoặc `false`).
3.  **default**: Giá trị mặc định nếu không truyền prop.
4.  **validator**: Hàm để xác thực giá trị của prop.

### one way data flow

Luồng dữ liệu 1 chiều. Khi sử dụng props để truyền dữ liệu từ component cha đến component con, dữ liệu luôn chỉ di chuyển theo một chiều: từ cha đến con. Điều này giúp đảm bảo tính dễ dự đoán và đơn giản trong luồng dữ liệu.

- Dữ liệu chỉ đi theo một chiều: Cha → Con.
- Component con chỉ nhận dữ liệu qua props và không được phép thay đổi trực tiếp.
- Nếu cần cập nhật dữ liệu, con phải thông báo lại cho cha thông qua các sự kiện.

## events

### emit

Khi một component con (`child component`) cần thông báo một sự kiện hoặc gửi dữ liệu về cho component cha (`parent component`), ta sử dụng cơ chế `emit`.

`emit` được sử dụng để phát sự kiện từ component con đến component cha. Khi một sự kiện được phát, component cha có thể lắng nghe sự kiện đó và thực hiện một hành động tương ứng.

#### Cách sử dụng cơ bản:

- Từ component con, bạn gọi `emit` để phát một sự kiện.
- Component cha lắng nghe sự kiện bằng cú pháp `@eventName`.

```js
// ParentComponent
<template>
  <ChildComponent @custom-event="handleEvent" />
</template>

<script>
export default {
  setup() {
    handleEvent(data) {
      console.log('Event received from child:', data);
    }
  }
};
</script>
```

```js
// ChildComponent
<template>
  <button @click="sendEvent">Click me</button>
</template>

<script>
export default {
  emits: ['custom-event'],
  setup(props, { emit }) {
    emit('custom-event')
  }
}
</script>
```

### defineEmits

Trong Vue 3 với **Composition API**, bạn sử dụng `defineEmits` để khai báo các sự kiện mà component con có thể phát ra. Điều này giúp việc phát sự kiện được kiểm soát chặt chẽ hơn và dễ dàng hơn để quản lý.

```js
// Cơ bản
const emit = defineEmits(["eventName1", "eventName2"]);

// Kiểu dữ liệu với typescript
const emit = defineEmits<{
  (eventName: 'eventName1', payload: string): void;
  (eventName: 'eventName2', payload: number): void;
}>();
```
