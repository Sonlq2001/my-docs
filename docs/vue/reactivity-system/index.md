---
sidebar_position: 2
---

# Reactivity system

Reactivity System trong Vue.js là một hệ thống phản ứng tự động giúp theo dõi và cập nhật giao diện người dùng (UI) khi trạng thái dữ liệu thay đổi. Điều này là cốt lõi trong Vue.js, giúp bạn không cần thao tác DOM trực tiếp mà vẫn có thể xây dựng giao diện động, dễ bảo trì.

## 1. **Cách Vue theo dõi và phản ứng với dữ liệu**

Vue sử dụng hệ thống reactivity để "quan sát" các thay đổi trên dữ liệu. Khi dữ liệu thay đổi:

- Vue phát hiện sự thay đổi thông qua các getter và setter được cài đặt khi dữ liệu được khởi tạo.
- Các thành phần giao diện (UI) phụ thuộc vào dữ liệu đó sẽ được cập nhật tự động.

---

## 2. **Nguyên lý hoạt động của Reactivity System**

#### a) **Proxy API (Vue 3)**

Trong Vue 3, hệ thống reactivity được xây dựng dựa trên **`Proxy`**, một tính năng của JavaScript hiện đại. Vue dùng Proxy để theo dõi đọc/ghi dữ liệu:

- Khi bạn đọc giá trị, Vue "theo dõi" (track) rằng giá trị đó đã được sử dụng.
- Khi bạn ghi giá trị mới, Vue sẽ "kích hoạt" (trigger) việc cập nhật lại bất kỳ phần nào của giao diện phụ thuộc vào giá trị đó.

#### b) **Object.defineProperty (Vue 2)**

Trong Vue 2, reactivity được triển khai qua **`Object.defineProperty`**:

- Vue thêm các getter và setter vào mỗi thuộc tính trong object khi khởi tạo.
- Điều này cho phép Vue theo dõi các thay đổi nhưng có hạn chế với việc thêm/xóa thuộc tính động.

## `ref()`

- **`ref`** được sử dụng để tạo giá trị phản ứng cho **dữ liệu nguyên thủy** (primitive values) như `string`, `number`, `boolean`, hoặc cả **dữ liệu phức tạp** (object, array).
- Khi bạn sử dụng `ref`, Vue sẽ theo dõi giá trị của nó và tự động cập nhật giao diện nếu giá trị thay đổi.

```js
import { ref } from "vue";
const count = ref(0);
count.value++; // Truy cập giá trị qua .value
```

Không cần sử dụng `.value` trong `template`

```html
<button @click="count++">{{ count }}</button>
```

### Cách hoạt động:

- Giá trị của `ref` được truy cập thông qua **`.value`**.
- Khi giá trị `.value` thay đổi, các thành phần phụ thuộc sẽ tự động được cập nhật.

> `ref` Có thể chứa bất kỳ loại giá trị nào, bao gồm các đối tượng, mảng được lồng sâu hoặc cấu trúc dữ liệu tích hợp JavaScript như `Map`.

```js
import { ref } from "vue";

const obj = ref({
  nested: { count: 0 },
  arr: ["foo", "bar"],
});

function mutateDeeply() {
  // these will work as expected.
  obj.value.nested.count++;
  obj.value.arr.push("baz");
}
```

Mặc dù cấu trúc trạng thái rất phức tạp và lồng nhau, nhưng các thay đổi vẫn sẽ được phát hiện.

### Khi nào sử dụng `ref`?

- Khi làm việc với **dữ liệu đơn giản** (string, number, boolean) hoặc **giá trị riêng lẻ**.
- Khi bạn muốn sử dụng **cú pháp rõ ràng** thông qua `.value`.

### DOM Update Timing

Khi bạn thay đổi trạng thái phản ứng, DOM sẽ được cập nhật tự động.

Tuy nhiên, cần lưu ý rằng các bản cập nhật DOM không được áp dụng đồng bộ.

Thay vào đó, Vue lưu chúng vào bộ đệm cho đến "dấu tiếp theo" trong chu kỳ cập nhật để đảm bảo rằng mỗi thành phần chỉ cập nhật một lần cho dù bạn đã thực hiện bao nhiêu thay đổi trạng thái.

**Để đợi quá trình cập nhật DOM hoàn tất sau khi thay đổi trạng thái: dùng `nextTick()`**

```js
import { nextTick } from "vue";

async function increment() {
  count.value++;
  await nextTick();
  // Now the DOM is updated
}
```

## `reactive()`

- **`reactive`** được sử dụng để tạo **đối tượng phản ứng** (reactive objects).
- Vue sẽ theo dõi toàn bộ đối tượng (hoặc mảng) và tự động cập nhật giao diện nếu bất kỳ thuộc tính nào thay đổi.

```js
import { reactive } from 'vue'

const state = reactive({ count: 0 })

<button @click="state.count++">
  {{ state.count }}
</button>
```

### Cách hoạt động:

- Không cần `.value`. Bạn truy cập và thay đổi trực tiếp các thuộc tính của đối tượng.
- Vue sử dụng **Proxy** để theo dõi mọi thay đổi trong đối tượng.

:::warning
`reactive` chỉ hoạt động với các loại đối tượng (`object`, `array`, `Map`, `Set`). Nó không thể chứa các kiểu nguyên thủy `string`, `boolean`, `number`
:::

**Không nên dùng `destrucruring` với các giá trị của `reactive` và `ref`, vì khi đó giá trị sẽ không được theo dõi nữa**

```js title="reactive"
import { reactive } from "vue";

const state = reactive({ count: 10 });

let { count } = state;
count++;

console.log(count); // 11
console.log(state.count); // 10
```

```js title="ref"
import { ref } from "vue";

const state = ref(0);

let { value } = state;
value++;

console.log(value); // 1
console.log(state.value); // 0
```

### Khi nào sử dụng `reactive`?

- Khi bạn làm việc với **đối tượng phức tạp** (object, array).
- Khi muốn tránh sử dụng `.value` trong các thuộc tính con của object.

## **So sánh `ref` và `reactive`**

| **Tiêu chí**         | **`ref`**                                                   | **`reactive`**                                    |
| -------------------- | ----------------------------------------------------------- | ------------------------------------------------- |
| **Dữ liệu hỗ trợ**   | Dữ liệu đơn giản (primitive) hoặc phức tạp (object, array). | Chỉ hỗ trợ object và array.                       |
| **Truy cập giá trị** | Sử dụng `.value` cho mọi giá trị.                           | Truy cập trực tiếp các thuộc tính.                |
| **Reactivity sâu**   | Không theo dõi sâu (nested objects không reactive).         | Theo dõi sâu toàn bộ đối tượng.                   |
| **Cú pháp**          | Rõ ràng hơn nhưng cần `.value`.                             | Ngắn gọn, tự nhiên khi làm việc với object/array. |
| **Khi nào sử dụng?** | Dữ liệu đơn giản hoặc biến độc lập.                         | Đối tượng hoặc mảng phức tạp.                     |
