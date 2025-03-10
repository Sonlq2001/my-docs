---
title: Reactivity advanced
---

## `shallowRef`

`shallowRef` là một hàm được sử dụng để tạo một reactive reference (tham chiếu phản ứng) cho một giá trị, nhưng không thực hiện việc theo dõi sâu (shallow tracking) các thay đổi bên trong đối tượng hoặc mảng.

Điều này có nghĩa là `shallowRef` chỉ theo dõi sự thay đổi của chính giá trị đó, chứ không theo dõi sự thay đổi của các thuộc tính bên trong đối tượng hoặc các phần tử bên trong mảng.

> ref() mặc định sẽ là deep tracking

### Khi nào sử dụng `shallowRef`?

- Khi bạn chỉ quan tâm đến việc thay đổi giá trị của reference chứ không quan tâm đến việc thay đổi các thuộc tính bên trong đối tượng hoặc mảng.

- Khi bạn muốn tối ưu hiệu suất bằng cách giảm bớt việc theo dõi các thay đổi không cần thiết.

```js title='Example shallowRef'
const user = shallowRef({
  name: "John",
  age: 25,
});

watchEffect(() => {
  console.log("User changed:", user.value.age);
});

user.value.age = 31;

/*
 + console.log sẽ chỉ được chạy 1 lần cho dù đã thay đổi giá trị age
 + vì nó chỉ quan tâm đến sự thay đổi của giá trị ( tham chiếu ) chứ không phải là thuộc tính của object
*/
// "User changed:" 25
```

```js title='Example ref'
const user = ref({
  name: "John",
  age: 25,
});

watchEffect(() => {
  console.log("User changed:", user.value.age);
});

user.value.age = 31;

// console.log sẽ sẽ chạy 2 lần vì đã thay đổi giá trị age, và kích hoạt lại phản ứng.
// "User changed:" 25
// "User changed:" 31
```
