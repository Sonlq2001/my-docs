# Variables

Biến là cấu trúc dữ liệu gán tên đại diện cho một giá trị. Chúng có thể chứa bất kỳ loại dữ liệu nào.

Tên của một biến được gọi là định danh. Phải được viết theo quy tắc:

- Có thể chứa các chữ cái `Unicode`, ký hiệu đô la (`$`), ký tự gạch dưới (`_`), chữ số (`0-9`) và thậm chí một số ký tự `Unicode`.
- Không thể chưa khoảng trắng trong tên biến
- Phải bắt đầu bằng một chữ cái, dấu gạch dưới (`_`) hoặc ký hiệu đô la (`$`). Không được bắt đầu bằng số.

```js title="Example"
var a = true;
var _b = "Hello";
var $c = [1, 2];
var 9d = {name: "Hi"} // sai quy tắc đặt tên
```
