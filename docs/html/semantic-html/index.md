---
sidebar_position: 4
---

# Semantic HTML

`Semantic` có nghĩa là "liên quan đến ý nghĩa". Viết HTML ngữ nghĩa có nghĩa là sử dụng các phần tử HTML để cấu trúc nội dung của bạn dựa trên ý nghĩa của từng phần tử chứ không phải hình thức của nó.

Sử dụng `<div>` và `<span>`, hai phần tử không có giá trị ngữ nghĩa.

```html title='Example'
<!-- Dùng các thẻ không có giá trị bổ nghĩa -->
<div>
  <span>Three words</span>
  <div>
    <a>one word</a>
    <a>one word</a>
    <a>one word</a>
    <a>one word</a>
  </div>
</div>
<div>
  <div>
    <div>five words</div>
  </div>
  <div>
    <div>three words</div>
    <div>forty-six words</div>
    <div>forty-four words</div>
  </div>
  <div>
    <div>seven words</div>
    <div>sixty-eight words</div>
    <div>forty-four words</div>
  </div>
</div>
<div>
  <span>five words</span>
</div>
```

Sử dụng các thẻ có ngữ nghĩa

```html title='Example'
<!-- Dùng các thẻ có ngữ nghĩa để mô tả bố cục -->
<header>
  <h1>Three words</h1>
  <nav>
    <a>one word</a>
    <a>one word</a>
    <a>one word</a>
    <a>one word</a>
  </nav>
</header>
<main>
  <header>
    <h1>five words</h1>
  </header>
  <section>
    <h2>three words</h2>
    <p>forty-six words</p>
    <p>forty-four words</p>
  </section>
  <section>
    <h2>seven words</h2>
    <p>sixty-eight words</p>
    <p>forty-four words</p>
  </section>
</main>
<footer>
  <p>five words</p>
</footer>
```

Với các phần tử ngữ nghĩa, cung cấp đủ ngữ cảnh để người không phải là lập trình viên có thể giải mã mục đích và ý nghĩa mà không cần phải gặp phải thẻ HTML. Nó chắc chắn cung cấp đủ ngữ cảnh để nhà phát triển hiểu được bố cục của trang, ngay cả khi họ không hiểu nội dung, chẳng hạn như nội dung bằng tiếng nước ngoài.

## Accessibility object model (AOM)

Khi trình duyệt phân tích cú pháp nội dung nhận được, nó sẽ xây dựng mô hình đối tượng tài liệu (DOM) và mô hình đối tượng CSS (CSSOM). Sau đó nó cũng xây dựng một cây khả năng tiếp cận. Các thiết bị hỗ trợ, chẳng hạn như trình đọc màn hình, sử dụng AOM để phân tích và diễn giải nội dung. DOM là một cây gồm tất cả các nút trong tài liệu. AOM giống như một phiên bản ngữ nghĩa của DOM.

### The role attribute

Thuộc tính `role` mô tả vai trò của một phần tử trong ngữ cảnh của tài liệu. Thuộc tính `role` là thuộc tính toàn cục có nghĩa là nó hợp lệ trên tất cả các thành phần.

Mỗi phần tử ngữ nghĩa đều có một vai trò tiềm ẩn, một số tùy thuộc vào ngữ cảnh.

`role` của phần tử rất quan trọng trong việc xây dựng AOM. Ngữ nghĩa của một phần tử hoặc 'role' rất quan trọng đối với các công nghệ hỗ trợ và trong một số trường hợp là các công cụ tìm kiếm. Người dùng công nghệ hỗ trợ dựa vào ngữ nghĩa để điều hướng và hiểu ý nghĩa của nội dung. Vai trò của thành phần này cho phép người dùng truy cập vào nội dung họ tìm kiếm một cách nhanh chóng và có thể quan trọng hơn là vai trò này thông báo cho người dùng trình đọc màn hình cách tương tác với thành phần tương tác khi nó được tập trung.

Bằng cách sử dụng thuộc tính `role`, bạn có thể gán cho bất kỳ thành phần nào một vai trò, bao gồm một vai trò khác với vai trò mà thẻ ngụ ý:

```html title="Example"
<p role="button">Click Me</p>
<!-- Gán 1 vai trò khác cho thẻ <p> là button -->
```

Mặc dù việc thêm `role="button"` vào một phần tử sẽ thông báo cho trình đọc màn hình rằng phần tử đó là một nút nhưng việc này không làm thay đổi hình thức hoặc chức năng của phần tử đó.

Có thể làm cho các thẻ không có ngữ nghĩa (`div`, `span`) trở nên có ngữ nghĩa bằng cách gán cho mỗi thành phần một vai trò:

```html title="Example"
<div role="banner">
  <span role="heading" aria-level="1">Three words</span>
  <div role="navigation">
    <a>one word</a>
    <a>one word</a>
    <a>one word</a>
    <a>one word</a>
  </div>
</div>
```

> Mặc dù thuộc tính vai trò có thể được sử dụng để thêm ngữ nghĩa cho bất kỳ phần tử nào, nhưng thay vào đó, bạn nên sử dụng các phần tử có vai trò tiềm ẩn mà bạn cần.

## Semantic elements

HTML nên được sử dụng để cấu trúc nội dung chứ không phải để xác định hình thức của nội dung. Hãy chọn từng thành phần dựa trên ý nghĩa và chức năng ngữ nghĩa của thành phần đó. Mã hóa HTML theo cách hợp lý, ngữ nghĩa và có ý nghĩa giúp đảm bảo CSS được áp dụng như dự định.
