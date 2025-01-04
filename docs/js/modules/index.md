---
sidebar_position: 14
---

# Modules

**Modules** (module) là một tính năng quan trọng trong JavaScript giúp tổ chức, quản lý và tái sử dụng mã một cách hiệu quả. Một module là một khối mã độc lập, có thể chứa các biến, hàm, lớp hoặc đối tượng, và thường được xuất ra (export) để sử dụng trong các tệp khác.

## Lợi ích của modules

1.  **Tổ chức mã tốt hơn:**

    - Giúp chia nhỏ ứng dụng lớn thành các tệp nhỏ hơn, dễ quản lý.
    - Mỗi module tập trung vào một nhiệm vụ hoặc chức năng cụ thể.

2.  **Tái sử dụng mã:**

    - Một module có thể được sử dụng lại ở nhiều nơi khác nhau trong dự án.

3.  **Tránh xung đột tên:**

    - Các biến, hàm trong module có phạm vi riêng (scope), giảm nguy cơ xung đột với các phần khác trong ứng dụng.

4.  **Dễ bảo trì:**

    - Khi cần sửa đổi hoặc nâng cấp, bạn chỉ cần tập trung vào module tương ứng mà không ảnh hưởng đến toàn bộ ứng dụng.

## Export

Để một module có thể được sử dụng ở nơi khác, bạn cần xuất (export) các phần tử trong module.

### Named Export

Đặc điểm:

- Có thể export nhiều giá trị từ một file.
- Khi import, bạn cần sử dụng đúng tên hoặc sử dụng đổi tên.
  - Sử dụng từ khóa `as` để đổi tên.

```js
import { add as addition } from "./math.js";
console.log(addition(2, 3)); // 5
```

- Có thể kết hợp với `import *` để nhập tất cả giá trị export

Ví dụ

```js
// file: math.js

export const pi = 3.14;

export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}
```

**Có thể viêt theo kiểu**

```js
const APP_CONSTANTS = {
  APP_NAME: "My App",
  APP_VERSION: "1.0.0",
  API_URL: "https://api.example.com",
};

const DEFAULT_PER_PAGE = 20;

export { APP_CONSTANTS, DEFAULT_PER_PAGE };
```

```js
import { APP_CONSTANTS, DEFAULT_PER_PAGE } from "...";
```

### Default Export

Đặc điểm:

- Sử dụng từ khóa `default`
- Chỉ có một giá trị duy nhất được export mặc định từ mỗi file.
- Khi import, tên có thể tùy ý
- Export mặc định thường dùng khi module đại diện cho một chức năng chính hoặc một đối tượng chính.

```js
// file: math.js
export default function add(a, b) {
  return a + b;
}
```

```js
// file: main.js
import addFunction from "./math.js"; // Tên có thể tùy ý
console.log(addFunction(5, 3)); // 8
```

**Có thể viêt theo kiểu**

```js
const APP_CONSTANTS = {
  APP_NAME: "My App",
  APP_VERSION: "1.0.0",
  API_URL: "https://api.example.com",
};

const DEFAULT_PER_PAGE = 20;

export default { APP_CONSTANTS, DEFAULT_PER_PAGE };
```

```js
import CONSTANTS from "...";
console.log(CONSTANTS); // {APP_CONSTANTS: {...}, DEFAULT_PER_PAGE: 20}
```

## Import

Để sử dụng các phần tử từ module khác, bạn cần nhập (import) chúng.

### Import with Default export

Có thể đổi tên tùy ý.

```js
// main.js
import add from "./math.js";
console.log(add(2, 3)); // 5
```

### Import with Named export

Muốn đổi tên phải dùng từ khóa `as`

```js
// main.js
import { pi, multiply as multiplyFunc } from "./math.js";
console.log(pi); // 3.14
console.log(multiplyFunc(2, 3)); // 6
```

### Import \*

Dùng để import tất cả

```js
// main.js
import * as math from "./math.js";
console.log(math.pi); // 3.14
console.log(math.multiply(2, 3)); // 6
```

## Kết hợp Export có tên và Export mặc định

```js
// file: math.js
export const pi = 3.14;
export default function add(a, b) {
  return a + b;
}
```

```js
// file: main.js
import add, { pi } from "./math.js";
console.log(pi); // 3.14
console.log(add(5, 3)); // 8
```

## Hỗ trợ modules trong trình duyệt

Trình duyệt hiện đại hỗ trợ modules thông qua thuộc tính `type="module"` trong thẻ `<script>`

```js
<script type="module">import {pi} from './math.js'; console.log(pi);</script>
```
