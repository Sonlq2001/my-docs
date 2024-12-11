# Bubble sort

`Sắp xếp bong bóng` là 1 thuật toán dùng để sắp xếp 1 mảng từ giá trị thấp nhất đến giá trị cao nhất.

Là một trong những thuật toán sắp xếp đơn giản nhất, hoạt động bằng cách so sánh từng cặp phần tử liền kề trong một danh sách và đổi chỗ chúng nếu chúng ở thứ tự sai. Quá trình này được lặp đi lặp lại cho đến khi danh sách được sắp xếp hoàn toàn.

![ex3](../../images/ex3.png)

**Ý tưởng**

- `Vòng lặp ngoài`: Lặp qua danh sách nhiều lần cho đến khi danh sách được sắp xếp hoàn toàn.
- `Vòng lặp trong`: Lặp qua từng cặp phần tử liền kề trong danh sách.
- `So sánh và đổi chỗ`: Nếu phần tử bên trái lớn hơn phần tử bên phải, thì đổi chỗ chúng cho nhau.
- `Kết thúc`: Sau mỗi vòng lặp ngoài, phần tử lớn nhất sẽ "nổi bọt" lên vị trí cuối cùng của danh sách chưa được sắp xếp.

```js
const nums = [5, 3, 6, 4, 2, 1];
for (let i = 0; i < nums.length; i++) {}
```
