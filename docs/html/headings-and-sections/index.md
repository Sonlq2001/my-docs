---
sidebar_position: 5
---

# Headings and sections

## Document structure

Bố cục layout với các thành phần cơ bản.

![base layout](../images/base-layout.png)

```html title="Example"
<body>
  <header>Header</header>
  <nav>Nav</nav>
  <main>Content</main>
  <aside>Aside</aside>
  <footer>Footer</footer>
</body>
```

Khi sử dụng các yếu tố ngữ nghĩa, trình duyệt có thể tạo các cây khả năng truy cập có ý nghĩa, cho phép người dùng trình đọc màn hình điều hướng dễ dàng hơn.

### `<header>`

```html
<header></header>
```

> Thẻ đầu trang, chủ yếu chứa một vài thông tin, tiêu đề, logo, liên hệ, ....

### `<main>`

```html
<main></main>
```

> Có một phần tử mốc `<main>` duy nhất. Phần tử `<main>` xác định nội dung chính của tài liệu. Chỉ nên có một `<main>` trên mỗi trang.

### `<aside>`

```html
<aside></aside>
```

> Dành cho nội dung có liên quan gián tiếp hoặc tiếp tuyến với nội dung chính của tài liệu.

### `<article>`

```html
<article></article>
```

> Được lồng bên trong thẻ `<main>`. Một `<article>` đại diện cho một phần nội dung hoàn chỉnh hoặc độc lập, về nguyên tắc, có thể tái sử dụng một cách độc lập.

### `<section>`

```html
<section></section>
```

> Được sử dụng để bao gồm các phần độc lập chung của tài liệu khi không còn phần tử ngữ nghĩa cụ thể nào để sử dụng. Các phần nên có tiêu đề, với rất ít trường hợp ngoại lệ.

### Headings: `<h1>-<h6>`

```html title="Example"
<h1></h1>
<!-- H1 cấp độ cao nhất -->
<h2></h2>
<h3></h3>
<h4></h4>
<h5></h5>
<h6></h6>
<!-- H6 cấp độ thấp nhất -->
```

Có sáu thành phần tiêu đề phần: `<h1>, <h2>, <h3>, <h4>, <h5> và <h6>`. Mỗi tiêu đề đại diện cho một trong sáu cấp độ của tiêu đề phần, trong đó `<h1>` là cấp độ phần cao nhất hoặc quan trọng nhất và `<h6>` là cấp độ thấp nhất.

Khi một tiêu đề được lồng trong biểu ngữ tài liệu `<header>`, đó là tiêu đề dành cho ứng dụng hoặc trang web. Khi được lồng trong `<main>`, cho dù nó có được lồng trong `<header>` trong `<main>` hay không thì đó là tiêu đề cho trang đó chứ không phải toàn bộ trang web. Khi được lồng trong `<article>` hoặc `<section>`, nó là tiêu đề cho phần phụ đó của trang.

Bạn nên sử dụng cấp độ tiêu đề tương tự như cấp độ tiêu đề trong trình soạn thảo văn bản: bắt đầu bằng `<h1>` làm tiêu đề chính, với `<h2>` làm tiêu đề cho các phần phụ và `<h3>` nếu các phần phụ đó có các phần, tránh bỏ qua các cấp độ tiêu đề. Có một bài viết hay về tiêu đề phần ở đây.

```html title="Example"
<article>
  <h1>Title main</h1>
  <div>
    <h2>Sub title</h2>
  </div>
</article>
<!-- Nên sử dụng theo cấp độ thẻ từ H1 -> H6 -->
```

### `<footer>`

```html
<footer></footer>
```

> Thẻ chân trang, chứa thông tin bản quyền, liên hệ, tác giả,
