---
sidebar_position: 4
---

# Method array

## Foreach

`forEach` là một phương thức được sử dụng để lặp qua từng phần tử của một mảng.

```js
array.forEach(callback(element, index, array) {
  // Khối mã cần thực thi
});
```

- `callback`: Là một hàm sẽ được gọi cho mỗi phần tử trong mảng.
  - `element`: Giá trị của phần tử hiện tại trong mảng.
  - `index` (tuỳ chọn): Chỉ số (index) của phần tử hiện tại.
  - `array` (tuỳ chọn): Chính mảng mà bạn đang lặp qua.
- `forEach` không trả về giá trị; nó chỉ thực hiện tác vụ trên mỗi phần tử.

**Thay đổi phần tử trong mảng**

```js
const numbers = [1, 2, 3];
numbers.forEach((num, index) => {
  numbers[index] = num * 2;
});
console.log(numbers);
```

`Không thể trực tiếp thay đổi giá trị của phần tử trong mảng bằng forEach`. Nếu cần thay đổi, bạn phải sử dụng một phương thức khác như map.

:::info Thông tin

1. Không trả về giá trị:

`forEach` chỉ thực hiện tác vụ, không trả về kết quả.

```js
const numbers = [1, 2, 3];
const doubled = numbers.forEach((num) => num * 2); // Sai
console.log(doubled); // Undefined
```

2. Không thể dừng vòng lặp:

Không thể sử dụng `break` hoặc `continue` để dừng hoặc bỏ qua một lần lặp trong `forEach`. Nếu cần tính năng này, bạn nên dùng for hoặc `for...of.`

```js
const numbers = [1, 2, 3, 4, 5];

numbers.forEach((num) => {
  if (num === 3) return; // Chỉ thoát khỏi callback, không dừng vòng lặp
  console.log(num);
});
// 1, 2, 4, 5
```

3. Không hỗ trợ async/await:

Các hàm bất đồng bộ trong `forEach` không hoạt động như mong muốn. Thay vào đó, bạn có thể dùng `for...of` để xử lý bất đồng bộ.

:::

## Map

`map` là một phương thức được sử dụng để lặp qua các phần tử của một mảng và `tạo ra một mảng mới`.

Có thể chuyển đổi hoặc biến đổi dữ liệu từ một mảng sang một mảng khác.

```js
const newArray = array.map(callback(currentValue, index, array) {
  // Giá trị trả về từ callback sẽ được thêm vào mảng mới
});
```

- `callback`: Hàm được gọi cho từng phần tử trong mảng.
  - `currentValue`: Phần tử hiện tại đang được xử lý.
  - `index` (tuỳ chọn): Chỉ số của phần tử hiện tại.
  - `array` (tuỳ chọn): Mảng gốc mà bạn đang lặp qua.
- `newArray`: Mảng mới được tạo ra từ kết quả của callback.

**Đặc điểm**

> Trả về một mảng mới: Mỗi giá trị được trả về từ callback sẽ được đưa vào mảng mới. Mảng gốc không bị thay đổi.

> Không thay đổi mảng gốc: map không sửa đổi mảng ban đầu, nó chỉ tạo ra mảng mới.

```js
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((num) => num * 2);

console.log(doubled); // [2, 4, 6, 8, 10]
console.log(numbers); // [1, 2, 3, 4, 5] (mảng gốc không bị thay đổi)
```

:::info Thông tin

1. Bắt buộc phải trả về giá trị từ callback:

Nếu callback không trả về gì, các phần tử trong mảng mới sẽ là undefined.

```js
const numbers = [1, 2, 3];
const results = numbers.map((num) => {
  num * 2; // Không có return
});

console.log(results); // [undefined, undefined, undefined]
```

2. Map không hỗ trợ trực tiếp async/await

`map` không "chờ" các `Promise` trong hàm `async` hoàn thành trước khi tiếp tục.

`map` được thiết kế để đồng bộ hóa, tức là nó không "biết" đến việc `callback` có trả về `Promise` hay không. Nếu callback trong map trả về một `Promise`, kết quả của map sẽ là một mảng các `Promise`, không phải kết quả đã được "giải quyết" (`resolved`).

```js
const promises = ids.map(async (id) => {
  const result = await fetchData(id);
  return result;
});

console.log(promises); // [Promise, Promise, Promise]
```

**Giải pháp**

Sử dụng `Promise.all` để chờ các Promise hoàn thành

```js
const ids = [1, 2, 3];

const results = await Promise.all(
  ids.map(async (id) => {
    const result = await fetchData(id);
    return result;
  })
);

console.log(results); // result đã được "resolved"
```

:::

**So sánh**

| Phương pháp                  | Ưu điểm                    | Nhược điểm                                 |
| ---------------------------- | -------------------------- | ------------------------------------------ |
| `map` + `Promise.all`        | Xử lý song song, nhanh hơn | Phức tạp hơn, cần thêm bước `Promise.all`. |
| `for...of` với `async/await` | Dễ đọc, xử lý tuần tự      | Chậm hơn vì không song song.               |

## Filter

Giúp lấy ra các phần tử thỏa mãn một điều kiện. Kết quả trả về là một mảng mới chứa tất các phần tử đáp ứng tiêu chí trong hàm callback.

```js
const newArray = array.filter(callback(element, index, array));
```

- `callback`: Hàm được gọi cho từng phần tử của mảng.
  - `element`: Phần tử hiện tại trong mảng.
  - `index` (tuỳ chọn): Vị trí (chỉ số) của phần tử hiện tại.
  - `array` (tuỳ chọn): Chính mảng gốc mà bạn đang lặp qua.
- `newArray`: Mảng mới gồm các phần tử thỏa mãn điều kiện trong callback.
  - Nếu không có phần tử nào thỏa mãn, filter sẽ trả về một mảng rỗng [].

:::info Thông tin

1. `filter` Phải trả về 1 giá trị `boolean`

`filter` sử dụng kết quả `true` hoặc `false` của callback để quyết định có giữ phần tử trong mảng mới hay không.

```js
const numbers = [1, 2, 3];
const result = numbers.filter((num) => {
  num > 2; // Không có `return`
});

console.log(result); // [] (mảng rỗng vì callback không trả về gì)
```

2. Không làm thay đổi mảng gốc mà sẽ tạo ra mảng mới.

:::

## Find

`find` là một phương thức được sử dụng trên mảng để tìm và trả về `phần tử đầu tiên` thỏa mãn điều kiện được cung cấp trong hàm callback.

```js
const foundElement = array.find(callback(element, index, array));
```

- `callback`: Hàm được gọi trên từng phần tử của mảng.
  - `element`: Phần tử hiện tại đang được xử lý.
  - `index` (tuỳ chọn): Vị trí (chỉ số) của phần tử trong mảng.
  - `array` (tuỳ chọn): Chính mảng mà bạn đang lặp qua.
- `foundElement`: Phần tử đầu tiên thỏa mãn điều kiện trong hàm callback. Nếu không có phần tử nào thỏa mãn, find sẽ trả về `undefined`.

:::info Thông tin

1. Trả về phần tử đầu tiên thỏa mãn điều kiện.
2. Không trả về mảng, chỉ trả về một phần tử hoặc `undefined`.
3. Không thay đổi mảng gốc.
4. Chỉ kiểm tra các phần tử cho đến khi tìm thấy phần tử phù hợp, sau đó dừng lại.

:::

### filter và find

**filter và find**

| Tiêu chí         | filter                              | find                                   |
| ---------------- | ----------------------------------- | -------------------------------------- |
| Kết quả trả về   | Mảng các phần tử thỏa mãn điều kiện | Phần tử đầu tiên thỏa mãn điều kiện.   |
| Số lượng kết quả | Có thể trả về nhiều phần tử         | Chỉ trả về một phần tử duy nhất.       |
| Hiệu suất        | Lặp qua toàn bộ mảng                | Dừng lại khi tìm thấy phần tử phù hợp. |

## Some

`some` là một phương thức được sử dụng trên mảng để kiểm tra xem ít nhất một phần tử trong mảng có thỏa mãn một điều kiện nhất định hay không.

Phương thức này trả về một giá trị `boolean` `(true hoặc false)`.

```js
const result = array.some(callback(element, index, array));
```

- `callback`: Hàm được gọi trên từng phần tử của mảng.
  - `element`: Phần tử hiện tại đang được kiểm tra.
  - `index` (tuỳ chọn): Vị trí (chỉ số) của phần tử trong mảng.
  - `array` (tuỳ chọn): Chính mảng mà bạn đang lặp qua.
- `result`: Trả về:
  - `true`: Nếu ít nhất một phần tử thỏa mãn điều kiện.
  - `false`: Nếu không có phần tử nào thỏa mãn điều kiện.

:::info Thông tin

1. Kiểm tra điều kiện trên từng phần tử:
2. Dừng lại ngay khi tìm thấy một phần tử thỏa mãn.
3. Không thay đổi mảng gốc.
4. Không cần kiểm tra toàn bộ mảng nếu đã tìm thấy kết quả true.

:::

## Every

`every` là một phương thức được sử dụng trên mảng để `kiểm tra` xem `tất cả các phần tử` trong mảng có thỏa mãn một điều kiện nhất định hay không.

Kết quả trả về là giá trị `boolean` `(true hoặc false)`.

```js
const result = array.every(callback(element, index, array));
```

- `callback`: Hàm được gọi trên từng phần tử của mảng.
  - `element`: Phần tử hiện tại đang được kiểm tra.
  - `index` (tuỳ chọn): Vị trí (chỉ số) của phần tử trong mảng.
  - `array` (tuỳ chọn): Chính mảng mà bạn đang lặp qua.
- `result`: Trả về:
  - `true`: Nếu tất cả các phần tử thỏa mãn điều kiện.
  - `false`: Nếu có bất kỳ một phần tử nào không thỏa mãn.

:::info Thông tin

1. Kiểm tra từng phần tử trong mảng

- Nếu bất kỳ phần tử nào không thỏa mãn, `every` sẽ dừng lại và trả về `false`.

2. Không thay đổi mảng gốc.
3. Không cần kiểm tra toàn bộ mảng nếu đã tìm thấy phần tử không phù hợp.

:::

### some và every

**filter và find**

| Tiêu chí           | some                                          | every                                         |
| ------------------ | --------------------------------------------- | --------------------------------------------- |
| Mục đích           | Kiểm tra xem ít nhất một phần tử thỏa mãn.    | Phần tử đầu tiên thỏa mãn điều kiện.          |
| Kết quả trả về     | `true` hoặc `false`.                          | `true` hoặc `false`.                          |
| Kiểm tra điều kiện | Chỉ cần một phần tử phù hợp để trả về `true`. | Tất cả phần tử phải phù hợp để trả về `true`. |

## Reduce

Là một phương thức được sử dụng trên mảng để lần lượt xử lý từng phần tử và tích lũy kết quả vào một giá trị duy nhất. Đây là một công cụ rất mạnh mẽ, thường được sử dụng để tính tổng, nhân, gom nhóm dữ liệu, hoặc chuyển đổi mảng thành một cấu trúc khác.

```js
array.reduce(callback(accumulator, currentValue, index, array), initialValue);
```

- `callback`: Hàm xử lý từng phần tử trong mảng.
  - `accumulator`: Giá trị tích lũy được từ lần lặp trước.
  - `currentValue`: Phần tử hiện tại trong lần lặp.
  - `index` (tuỳ chọn): Chỉ số của phần tử hiện tại.
  - `array` (tuỳ chọn): Mảng đang được lặp qua.
- `initialValue` (tuỳ chọn): Giá trị khởi tạo cho accumulator. Nếu không được cung cấp, phần tử đầu tiên của mảng sẽ được sử dụng làm initialValue, và vòng lặp bắt đầu từ phần tử thứ hai.

- **Kết quả trả về: Một giá trị duy nhất được tính toán từ mảng.**

```js
const people = [
  { name: "Alice", age: 25 },
  { name: "Bob", age: 30 },
  { name: "Alice", age: 35 },
];

const grouped = people.reduce((acc, person) => {
  const key = person.name;
  if (!acc[key]) {
    acc[key] = [];
  }
  acc[key].push(person);
  return acc;
}, {});

console.log(grouped);
/*
{
  Alice: [{ name: "Alice", age: 25 }, { name: "Alice", age: 35 }],
  Bob: [{ name: "Bob", age: 30 }]
}
*/
```

:::info Thông tin

1. Không cung cấp `initialValue`:

Nếu không truyền `initialValue`, phần tử đầu tiên của mảng sẽ được sử dụng làm giá trị khởi tạo, và vòng lặp bắt đầu từ phần tử thứ hai.
Điều này có thể gây lỗi khi mảng rỗng.

```js
const numbers = [];
const sum = numbers.reduce((acc, curr) => acc + curr, 0); // Không lỗi
const sumNoInit = numbers.reduce((acc, curr) => acc + curr); // Lỗi!
```

2. Hiệu suất:

Vì reduce duyệt qua từng phần tử, với mảng lớn, nó có thể tốn thời gian nếu logic phức tạp.

3. Dùng reduce khi bạn cần tạo ra một giá trị duy nhất.

:::

**Compare**

| Phương thức | Mục đích                                                     | Kết quả trả về                                              |
| ----------- | ------------------------------------------------------------ | ----------------------------------------------------------- |
| `reduce`    | Tính toán hoặc xử lý để tạo ra một giá trị duy nhất từ mảng. | Một giá trị duy nhất (có thể là số, mảng, đối tượng, v.v.). |
| `map`       | Biến đổi từng phần tử của mảng thành một giá trị khác.       | Mảng mới.                                                   |
| `filter`    | Lọc ra các phần tử thỏa mãn điều kiện.                       | Mảng mới.                                                   |
| `forEach`   | Lặp qua từng phần tử để thực hiện thao tác.                  | Không trả về giá trị.                                       |
