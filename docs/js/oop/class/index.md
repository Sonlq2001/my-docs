---
sidebar_position: 2
---

# Class

Là khuẩn mẫu để tạo ra đối tượng.

Sử dụng từ khóa `class` để tạo lớp

```js
class Animal {}

const dog = new Animal();
```

Có thể tạo `class` mà không cần định nghĩa tên cho nó

```js
class {
  constructor() {}
}
```

## Constructor

Hàm `constructor` được định nghĩa bên trong một class và luôn có tên là `constructor`

```js
class Animal {
  constructor() {}
}
```

Khi khởi tạo đối tượng với từ khóa `new` hàm `constructor` sẽ luôn được gọi.

### Key Features

- Khởi tạo các thuộc tính của đối tượng.
- Xử lý các logic cần thiết khi một đối tượng được tạo.
- Có thể nhận các tham số để tùy chỉnh đối tượng.

:::warning Chú ý
Mỗi `class` chỉ được phép có `một hàm constructor`. Nếu bạn định nghĩa nhiều hơn một, JavaScript sẽ báo lỗi.
:::

Nếu bạn không định nghĩa một hàm `constructor`, JavaScript sẽ cung cấp một `constructor` mặc định. `Constructor` mặc định này không làm gì ngoài việc tạo một đối tượng mới.

```js
class Animal {}
const dog = new Animal();
console.log(dog); // Animal {}
```

## Attribute

Định nghĩa các thuộc tính cho đối tượng trong hàm `constructor`.

Có thể nhận các tham số truyền vào.

```js
class Animal {
  constructor(name, weight, color) {
    this.name = name;
    this.weight = weight;
    this.color = color;
  }
}

const dog = new Animal("Pit", 5, "black");

// Animal { name: 'Pit', weight: 5, color: 'black' }
```

Các đối số truyền vào sẽ tương ứng với giá trị được định nghĩa trong hàm `constructor`

## Method

Định nghĩa các hành động trong `class`

```js
class Animal {
  // định nghĩa các thuộc tính cho đối tượng
  constructor(name, weight, color) {
    this.name = name;
    this.weight = weight;
    this.color = color;
  }

  // định nghĩa các hành động cho đối tượng
  getName() {
    return this.name;
  }
}

const dog = new Animal("Pit", 5, "black");

console.log(dog.getName()); // Pit
```

Để gọi các `method` trong `class`, sẽ tương tự như cách chúng ta gọi hàm thông thường.

Cũng có thể `truyền đối` và `nhận tham số`.

```js
class Animal {
  constructor(name, weight, color) {
    this.name = name;
    this.weight = weight;
    this.color = color;
  }

  eat(food) {
    return `${this.name} eat ${food}`;
  }
}

const dog = new Animal("Pit", 5, "black");

console.log(dog.eat("bone")); // Pit eat bone
```
