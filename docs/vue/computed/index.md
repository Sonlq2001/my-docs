---
sidebar_position: 4
---

# Computed

`computed` là một tính năng cho phép bạn định nghĩa các thuộc tính (computed properties) dựa trên dữ liệu hiện có trong trạng thái (state) của ứng dụng.

Các thuộc tính này được tính toán tự động khi dữ liệu phụ thuộc của chúng thay đổi và được lưu vào bộ nhớ đệm (cached), giúp tối ưu hiệu suất.

## Lợi ích của `computed`

1.  **Tối ưu hiệu suất:**

    - Giá trị của một computed property chỉ được tính lại khi dữ liệu phụ thuộc của nó thay đổi. Nếu không có thay đổi, Vue sẽ trả về giá trị đã được lưu trong bộ nhớ đệm.

2.  **Dễ bảo trì:**

    - Code trở nên rõ ràng hơn vì tách biệt logic tính toán khỏi template.

3.  **Tự động reactivity (tính phản ứng):**

    - Vue tự động theo dõi các dependencies (dữ liệu phụ thuộc) và cập nhật computed property khi cần.

4.  **Giảm lặp code:**

    - Các phép tính phức tạp hoặc dữ liệu đã xử lý chỉ cần viết một lần và có thể sử dụng lại.

```js
import { reactive, computed } from "vue";

const info = reactive({
  firstName: "John",
  lastName: "Doe",
});

const dataComputed = computed(() => {
  return `${info.firstName} ${info.lastName}`;
});
```

**Giải thích:**

- `fullName` là một computed property. Nó phụ thuộc vào `firstName` và `lastName`.
- Khi `firstName` hoặc `lastName` thay đổi, `fullName` sẽ tự động cập nhật.

## Computed nâng cao

### **Computed `Getter` và `Setter`**

Theo mặc định `computed` chỉ thực hiện việc `getter`, tức là tính toán và trả về giá trị, nên việc cố gắng gán lại 1 giá trị sẽ nhận được 1 cảnh báo.

Để có thể thực hiện cả việc `getter` và `setter` cho computed, cần cung cấp 2 hàm cho `computed`

```js
import { ref, computed } from "vue";

const info = reactive({
  firstName: "John",
  lastName: "Doe",
});

const dataComputed = computed({
  get() {
    return `${info.firstName} ${info.lastName}`;
  },

  set(newValue: string) {
    // newValue = 'Mie'
    info.firstName = newValue;
  },
});

dataComputed.value = "Mie";

console.log(dataComputed.value); // Mie Doe
```

**Giải thích:**

- `get` là hàm đọc giá trị.
- `set` là hàm ghi giá trị, cho phép bạn thay đổi `fullName` và đồng thời cập nhật `firstName` và `lastName`.

### **Dependency Tracking:**

- Vue tự động theo dõi các `reactive` hoặc `ref` sử dụng trong `computed`. Bạn không cần khai báo dependencies một cách thủ công.

### **Lazy Evaluation (Đánh giá lười):**

- Computed chỉ được tính toán lại khi cần, giúp tiết kiệm tài nguyên.

## Lấy giá trị trước đó

```js
import { computed, ref } from "vue";
const count = ref(0);

const dataComputed = computed((prevValue) => {
  console.log("prevValue", prevValue);
  return count.value;
});
```
