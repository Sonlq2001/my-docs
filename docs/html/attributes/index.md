---
sidebar_position: 6
---

# Attributes

Thuộc tính cung cấp các chức năng, thông tin cho phần tử. Viết với cú pháp `name=value` được phân tách bằng dấu cách và `chỉ được viết trong thẻ mở`.

![base element](../images/an-opening-tag-attribute-363effa33af66_856.png)

Một số thuộc tính có tính `toàn cục`, nghĩa là chúng có thể xuất hiện trong thẻ mở của bất kỳ phần tử nào. Các thuộc tính khác áp dụng cho một số phần tử nhưng không phải tất cả, trong khi các thuộc tính khác dành riêng cho từng phần tử, chỉ liên quan đến một phần tử duy nhất.

Trong HTML, tất cả các thuộc tính ngoại trừ boolean và ở một mức độ nào đó thuộc tính được liệt kê, đều yêu cầu một giá trị.

:::warning[Chú ý]
Mặc dù HTML `không phân biệt chữ hoa chữ thường` nhưng một số giá trị thuộc tính lại có.
:::

```html title="Example"
<!-- thuộc tính "type" không phân biệt chữ hoa và chữ thường, 2 giá trị như nhau -->
<input type="text" />
<input type="TeXt" />

<!-- thuộc tính "id" có phân biệt chữ hoa và chữ thường, 2 giá trị khác nhau -->
<div id="myId">
  <div id="MyID"></div>
</div>
```

## Boolean attributes

Thuộc tính `Boolean` trong thẻ luôn `true`. Các thuộc tính `Boolean` bao gồm **autofocus, inert, checked, disabled, required, reversed, allowfullscreen, default, loop, autoplay, controls, muted, readonly, multiple, selected**

Các giá trị `Boolean` có thể được bỏ qua, đặt thành một chuỗi trống hoặc là tên của thuộc tính, nhưng giá trị không nhất thiết phải được đặt thành chuỗi đúng. Tất cả các giá trị, bao gồm `true`, `false` và `''`, dù không hợp lệ nhưng sẽ chuyển thành true.

```html title="Example"
<input required />
<input required="" />
<input required="required" />
<!-- cả 3 giá trị required này đều là "true" -->
```

:::tip[Tip]
Nếu giá trị thuộc tính là `false`, hãy bỏ qua thuộc tính, không điền vào trong thẻ.
:::

## Enumerated attributes

Các thuộc tính liệt kê đôi khi bị nhầm lẫn với các thuộc tính `boolean`. Chúng là các thuộc tính HTML có một tập hợp giới hạn các giá trị hợp lệ được xác định trước. Giống như các thuộc tính `boolean`, chúng có giá trị mặc định nếu thuộc tính đó có mặt nhưng giá trị bị thiếu.

```html title="Example"
<!-- Nếu bạn viết -->
<div contenteditable></div>

<!-- Mặc định nó sẽ là -->
<div contenteditable="true"></div>
```

Không giống như các thuộc tính boolean, việc bỏ qua thuộc tính không có nghĩa là nó `false`, thuộc tính hiện tại bị thiếu giá trị không nhất thiết là `true`
và mặc định cho các giá trị không hợp lệ không nhất thiết phải giống như chuỗi rỗng `""`. Không giống như các giá trị `boolean`, các thuộc tính không tự động `true` nếu có.

```html title="Example"
<div contenteditable=""></div>
<div contenteditable="value"></div>
<!-- 2 trường hợp trên đều không hoạt động, vì bị giới hạn các giá trị hợp lệ được xác định trước  -->
```

> Trong hầu hết các trường hợp có thuộc tính được liệt kê, giá trị bị thiếu và giá trị không hợp lệ đều giống nhau. Ví dụ: nếu thuộc tính loại trên `<input>` bị thiếu, xuất hiện nhưng không có giá trị hoặc có giá trị không hợp lệ thì thuộc tính đó sẽ mặc định là `text`. Mặc dù hành vi này là phổ biến nhưng nó không phải là một quy tắc.

## Global attributes

Thuộc tính chung là các thuộc tính có thể được đặt trên bất kỳ phần tử HTML nào, bao gồm các phần tử trong `<head>`. Nhưng thực tế, mặc dù tất cả những thuộc tính `global` có thể được thêm vào bất kỳ phần tử HTML nào, nhưng một số thuộc tính chung không có tác dụng khi được đặt trên một số phần tử.

```html title="Example"
<meta name="description" content="Short Description" hidden />
<!-- thuộc tính "hidden" không hoạt động -->

<input type="text" hidden />
<!-- thuộc tính "hidden" hoạt động -->
```

### id

Dùng để xác định mã định danh duy nhất cho 1 phần tử

:::danger[Cảnh báo]
`id` phải là duy nhất cho tài liệu. Bố cục trang của bạn có thể sẽ không bị hỏng nếu một id được sử dụng nhiều lần, nhưng các tương tác JavaScript, liên kết và phần tử của bạn có thể không hoạt động như mong đợi.
:::

#### Ứng dụng id

`1. CSS selectors`

Dùng ký tự `#` để chỉ định `id` trong `css`

```html title="Example"
<div id="id-tag"></div>
```

```css title="Example"
#id-tag {
  color: red;
}
```

`2. Scripting`

Truy cập phần từ qua `id`

```html title="Example"
<button id="btn"></button>
```

```js title="Example"
const button1 = document.getElementById("btn");
const button2 = document.querySelector("#btn");
```

`3. <label>`

Phần tử HTML `<label>` có thuộc tính `for` lấy giá trị của nó là `id` của điều khiển biểu mẫu mà nó được liên kết.

```html title="Example"
<label for="minutes">Send me a reminder</label>
<input type="number" name="min" id="minutes" />
<!-- click vào label, input sẽ được focus, khi giá trị thuộc tính "for" và "id" trùng nhau -->
```

:::tip[tip]
Thuộc tính `for` và `id` ứng dụng để tạo ra các `custom` về radio, checkbox hoặc tạo ra menu bar ở mobile, modal ...
:::

`4. Link fragment identifier`

Tạo ra các đoạn, nội dung liên kết trong trang. Khi bấm vào link liên kết sẽ được tự động cuộn xuống nội dung được chỉ định với giá trị `id` tương ứng.

```html title="Example"
<a href="#my-docs">Link docs</a>

<section id="my-docs">content</section>

<!-- Đặt giá trị link tương ứng với giá trị id -->
```

### class

Khác với `id`. Thuộc tính `class` mang tính nhất chất nhóm. Được sử dụng để truy vấn nhiều phần tử có cùng `class` hoặc `css` nhiều các phần tử có chung `class` với nhau.

### style

Thuộc tính `style` cho phép áp dụng kiểu css nội tuyến `inline styles`, là các kiểu được áp dụng cho một phần tử mà thuộc tính được đặt trên đó. Thuộc tính style lấy giá trị của nó là các cặp giá trị thuộc tính CSS, với cú pháp của giá trị giống với nội dung của khối kiểu CSS: các thuộc tính được theo sau bởi dấu hai chấm, giống như trong CSS và dấu chấm phẩy kết thúc mỗi khai báo, theo sau giá trị .

Chỉ được áp dụng cho phần tử mà thuộc tính được đặt.

> Không khuyến khích viết css kiểu này, khó bảo trì, và phát triển ...

```html
<section style="color:red; font-weight: 600"></section>
```

### tabindex

Thuộc tính tabindex có thể được thêm vào bất kỳ phần tử nào để cho phép nó nhận tiêu điểm.

Thuộc tính tabindex nhận vào `1 số nguyên`. Giá trị âm (quy ước sử dụng -1) làm cho một phần tử có khả năng nhận tiêu điểm, nhưng không thêm vào chuỗi tab.Giá trị tabindex bằng `0` làm cho phần tử có thể lấy tiêu điểm và truy cập được thông qua tính năng lập thẻ, thêm nó vào thứ tự tab mặc định của trang theo thứ tự mã nguồn. Giá trị từ 1 trở lên sẽ đặt phần tử vào chuỗi tiêu điểm được ưu tiên và không được khuyến nghị.

Khi người dùng nhấn phím `tab`, tiêu điểm sẽ di chuyển đến phần tử có thể lấy tiêu điểm tiếp theo như thể họ đã đặt `tabindex="0"`. Các phần tử khác không thể lấy nét theo mặc định. Việc thêm thuộc tính tabindex vào các phần tử đó sẽ cho phép chúng nhận được tiêu điểm trong khi lẽ ra chúng không nhận được tiêu điểm.

```html
<!-- Bấm vào input vào sau đó nhấn tab, các vị trí tab sẽ được di chuyển theo đúng thứ tự "tabindex" -->
<ol>
  <li><input tabindex="3" value="3" /></li>
  <li><input tabindex="2" value="2" /></li>
  <li><input tabindex="0" value="0" /></li>
  <li><input tabindex="0" value="0" /></li>
  <li><input tabindex="-1" value="-1" /></li>
  <li><input tabindex="0" value="0" /></li>
  <li><input tabindex="1" value="1" /></li>
</ol>
```

:::warning[Lưu ý]
Việc thay đổi thứ tự tab có thể tạo ra trải nghiệm người dùng thực sự tồi tệ. Không nên lạm dụng và sử dụng có mục đích và theo thứ tự nhất định.
:::

### role

Cung cấp ý nghĩa ngữ nghĩa cho nội dung, cho phép trình đọc màn hình thông báo cho người dùng trang web về tương tác người dùng dự kiến ​​của đối tượng.

```html title="Example"
<div role="button">Button</div>
<!-- thẻ div mang ý nghĩa là 1 button -->
```

### contenteditable

Cho phép biến 1 phần tử trở thành ô nhập văn bản

```html title="Example"
<div contenteditable></div>
<!-- thẻ div có thẻ nhập được nội dung văn bản -->
```

## Custom attributes
