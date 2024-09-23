---
sidebar_position: 1
---

# Tổng quan

Ngôn ngữ đánh dấu siêu văn bản hay HTML là ngôn ngữ đánh dấu tiêu chuẩn để mô tả cấu trúc của tài liệu được hiển thị trên web. HTML bao gồm một loạt các thành phần và thuộc tính được sử dụng để đánh dấu tất cả các thành phần của tài liệu nhằm cấu trúc nó một cách có ý nghĩa.

Tài liệu HTML về cơ bản là một cây nút, bao gồm các phần tử HTML và nút văn bản. Các phần tử HTML cung cấp ngữ nghĩa và định dạng cho tài liệu, bao gồm tạo đoạn văn, danh sách và bảng cũng như nhúng hình ảnh và điều khiển biểu mẫu. Mỗi phần tử có thể có nhiều thuộc tính được chỉ định. Nhiều phần tử có thể có nội dung, bao gồm các phần tử và văn bản khác. Các phần tử khác trống, có thẻ và thuộc tính xác định chức năng của chúng.

## Element

Các phần tử HTML được mô tả bằng các thẻ, được viết bằng dấu ngoặc nhọn (< và >).

![Element image](./images/the-tags-content-make-10a59ba9efd26_856.png)

Thẻ đóng giống thẻ mở, có dấu gạch chéo trước. Trình duyệt không hiển thị các thẻ. Các thẻ được sử dụng để diễn giải nội dung của trang.

```html title="Dùng thẻ ul, li để mô tả 1 danh sách"
<ul>
  <li>Táo</li>
  <li>Chuối</li>
  <li>Mít</li>
</ul>
```

Các thẻ tự đóng.

```html title="Example"
<input type="range" />

<img src="switch.svg" alt="light switch" />
```

- `/>` chỉ ra rằng phần tử tự đóng và sẽ không có thẻ kết thúc hoặc thẻ đóng phù hợp.
- Để cung cấp thông tin về nội dung! Thông tin được cung cấp bởi các thuộc tính của phần tử.

VD: `<img />`, `<input />`, `<link />`, `<br />`, `<hr />`

## Attributes

Thuộc tính cung cấp thông tin về phần tử. Thuộc tính chỉ được viết trong thẻ mở của element. Được viết dạng `key="value"`.

![Element image](./images/an-opening-tag-attribute-363effa33af66_856.png)

:::tip[Lưu ý]

- `Thuộc tính toàn cục`: là có thể xuất hiện được bất cứ thẻ mở của phần tử nào.
- `Thuộc tính cục bộ`: chỉ áp dụng cho 1 số phần từ và một số khác là dành riêng cho một phần tử, chỉ liên quan đến một phần tử duy nhất.

:::

```html title="Example"
<p id="id-content"></p>

<img id="id-image" src="" alt="" />
<!-- 
  - thuộc tính id được dùng cho cả thẻ p và img
  - thuộc tính src và alt được dùng cho thẻ img
-->
```

Hầu hết các thuộc tính là cặp `key="value"`. Các thuộc tính Boolean, có giá trị đúng, sai hoặc giống với tên của thuộc tính, có thể được đưa vào chỉ như thuộc tính.

```html
<button disabled>Button</button>
<!-- 
  - thuộc tính disabled nhận vào giá trị boolean nên có thể viết trực tiếp mà không cần điền giá trị
  - tương đương với disabled="true" 
-->
```

HTML không phân biệt chữ hoa chữ thường, nhưng một số giá trị thuộc tính thì có. Các giá trị được xác định trong đặc tả không phân biệt chữ hoa chữ thường. Các chuỗi không được xác định làm từ khóa thường phân biệt chữ hoa chữ thường, bao gồm các giá trị `id` và `class`.

Lưu ý rằng nếu một giá trị thuộc tính phân biệt chữ hoa chữ thường trong HTML thì nó sẽ phân biệt chữ hoa chữ thường khi được sử dụng như một phần của bộ chọn thuộc tính ( attribute selector ) trong CSS và trong JavaScript.

> Nên đánh dấu HTML bằng chữ cái viết thường cho tất cả tên thành phần và tên thuộc tính trong thẻ của mình, nhưng không bắt buộc.
