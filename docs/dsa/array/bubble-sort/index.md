---
sidebar_position: 1
---

# Bubble sort

Sắp xếp nổi bọt là một thuật toán sắp xếp đơn giản, hoạt động bằng cách so sánh các cặp phần tử liền kề trong mảng và hoán đổi chúng nếu chúng không theo thứ tự mong muốn (tăng dần hoặc giảm dần). Thuật toán này tiếp tục lặp đi lặp lại quá trình này cho đến khi không còn phần tử nào cần hoán đổi.

![ex3](../../images/ex3.png)

**Cách hoạt động**

- `Bước 1`: So sánh hai phần tử liên tiếp trong mảng.
- `Bước 2`: Nếu phần tử đầu tiên lớn hơn phần tử thứ hai, hoán đổi chúng.
- `Bước 3`: Tiếp tục so sánh các phần tử liền kề trong mảng, làm cho phần tử lớn nhất "nổi lên" cuối mảng sau mỗi vòng lặp.
- `Bước 4`: Lặp lại bước 1 và 2 cho đến khi mảng được sắp xếp hoàn chỉnh.

**Ý tưởng**

- `Vòng lặp ngoài`: Lặp qua danh sách nhiều lần cho đến khi danh sách được sắp xếp hoàn toàn.
- `Vòng lặp trong`: Lặp qua từng cặp phần tử liền kề trong danh sách.
- `So sánh và đổi chỗ`: Nếu phần tử bên trái lớn hơn phần tử bên phải, thì đổi chỗ chúng cho nhau.
- `Kết thúc`: Sau mỗi vòng lặp ngoài, phần tử lớn nhất sẽ "nổi bọt" lên vị trí cuối cùng của danh sách chưa được sắp xếp.

:::info
Sau mỗi lần lặp ít nhất 1 phần tử sẽ được đứng đúng vị trí.
:::

## Example explanation

```js title="Example"
const nums = [5, 3, 6, 4, 2, 1];
let n = nums.length;
for (let i = 0; i < n - 1; i++) {
  for (let j = 0; j < n - 1 - i; j++) {
    // So sánh hai phần tử liền kề
    if (nums[j] > nums[j + 1]) {
      // Hoán đổi chúng nếu sai thứ tự
      let temp = nums[j];
      nums[j] = nums[j + 1];
      nums[j + 1] = temp;
    }
  }
}
console.log(nums); // [1, 2, 3, 4, 5, 6]
```

### 1. Vòng lặp ngoài:

```js
for (let i = 0; i < n - 1; i++)
```

- Vòng lặp ngoài sẽ lặp tối đa n - 1 lần (khi `i` chạy từ `0` đến `n - 2`).

**Tại sao không phải `n` lần mà lại là `n - 1`?**

- `Giải thích`: Mỗi lần chạy vòng lặp ngoài, phần tử lớn nhất trong mảng (hoặc dãy con đang xem xét) sẽ "nổi lên" cuối mảng sau vòng lặp trong. Sau mỗi lần lặp, phần tử lớn nhất này đã ở vị trí đúng của nó, và do đó không cần phải kiểm tra nó nữa trong các vòng lặp tiếp theo.
  - `Ví dụ`: Sau lần lặp đầu tiên, phần tử lớn nhất sẽ nằm ở cuối mảng, sau lần lặp thứ hai, phần tử lớn thứ hai sẽ ở đúng vị trí cuối cùng ngoài cùng, và cứ như vậy. Do đó, sau `n - 1` lần, mảng sẽ được sắp xếp hoàn toàn.

Vì vậy, vòng lặp ngoài chỉ cần chạy n - 1 lần để sắp xếp mảng. Nếu chạy n lần, sẽ có một vòng lặp thừa mà không cần thiết, vì mảng sẽ đã được sắp xếp hoàn toàn từ lần lặp thứ n - 1.

### 2. Vòng lặp trong:

```js
for (let j = 0; j < n - 1 - i; j++)
```

- Vòng lặp trong chạy từ `0` đến `n - 1 - i`, tức là vòng lặp trong giảm dần số lượng phần tử phải so sánh và hoán đổi trong mỗi lần lặp ngoài.

**Giải thích cụ thể:**

- Ở vòng lặp ngoài, sau mỗi lần lặp (khi `i` tăng lên), các phần tử lớn nhất đã "nổi lên" cuối mảng. Vì vậy, phần tử cuối cùng trong mảng đã ở đúng vị trí, và không cần phải so sánh nữa.

  - Ví dụ: Ở lần lặp đầu tiên (`i = 0`), vòng lặp trong sẽ so sánh từ phần tử đầu tiên đến phần tử thứ `n-1`. Sau vòng lặp đầu tiên, phần tử lớn nhất đã được đưa về cuối mảng.
  - Ở lần lặp thứ hai (`i = 1`), vòng lặp trong chỉ cần so sánh từ phần tử đầu tiên đến phần tử thứ `n-2`, vì phần tử cuối cùng đã ở đúng vị trí.
  - Cứ như vậy, khi `i` tăng lên, số phần tử cần phải so sánh giảm dần đi.

Vì vậy, số lần so sánh trong vòng lặp trong là `n - 1 - i`, đảm bảo rằng không có phần tử nào đã được sắp xếp hoàn toàn (tức là phần tử lớn nhất) được xét lại.

**Tóm tắt:**

- Vòng lặp ngoài (`for (let i = 0; i < n - 1; i++)`) lặp `n - 1` lần vì sau mỗi lần lặp, một phần tử lớn nhất sẽ "nổi lên" cuối mảng, không cần phải so sánh nữa.
- Vòng lặp trong (`for (let j = 0; j < n - 1 - i; j++)`) lặp số lần giảm dần (từ `n - 1` xuống `1`) vì mảng ngày càng được sắp xếp và các phần tử lớn nhất đã ở đúng vị trí cuối cùng.

**Ví dụ:**

Giả sử mảng là `[5, 3, 8, 4, 2]` và ta muốn sắp xếp mảng theo thứ tự tăng dần.

Vòng lặp 1 (i = 0):

- Vòng lặp trong sẽ so sánh và hoán đổi các cặp phần tử:
  - So sánh 5 và 3 → Hoán đổi → Mảng thành [3, 5, 8, 4, 2]
  - So sánh 5 và 8 → Không hoán đổi
  - So sánh 8 và 4 → Hoán đổi → Mảng thành [3, 5, 4, 8, 2]
  - So sánh 8 và 2 → Hoán đổi → Mảng thành [3, 5, 4, 2, 8]

Sau vòng lặp đầu tiên, phần tử lớn nhất (8) đã ở vị trí cuối cùng.

Vòng lặp 2 (i = 1):

- Vòng lặp trong chỉ cần so sánh các phần tử từ 0 đến n - 2 - 1 = 3:

  - So sánh 3 và 5 → Không hoán đổi
  - So sánh 5 và 4 → Hoán đổi → Mảng thành [3, 4, 5, 2, 8]
  - So sánh 5 và 2 → Hoán đổi → Mảng thành [3, 4, 2, 5, 8]

Sau vòng lặp này, phần tử lớn thứ hai (5) đã ở đúng vị trí.

Vòng lặp 3 (i = 2):

- Vòng lặp trong chỉ cần so sánh các phần tử từ 0 đến n - 3 - 1 = 2:
  - So sánh 3 và 4 → Không hoán đổi
  - So sánh 4 và 2 → Hoán đổi → Mảng thành [3, 2, 4, 5, 8]

Sau vòng lặp này, phần tử lớn thứ ba (4) đã ở đúng vị trí.

Vòng lặp 4 (i = 3):

- Vòng lặp trong chỉ cần so sánh các phần tử từ 0 đến n - 4 - 1 = 1:
  - So sánh 3 và 2 → Hoán đổi → Mảng thành [2, 3, 4, 5, 8]

Sau vòng lặp thứ 4, mảng đã được sắp xếp hoàn toàn.
