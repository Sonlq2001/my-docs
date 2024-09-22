# Metadata

Thẻ siêu dữ liệu được nằm trong thẻ `<head>` cung cấp các thông tin, thông số kĩ thuật, tối ưu hóa công cụ tìm kiếm ... cho ứng dụng.

## The required `<meta>` tags

### Meta Charset Tag

```html title='Example'
<meta charset="UTF-8" />
```

> Thẻ meta charset, cụ thể là meta charset=”UTF-8″>, có liên quan chặt chẽ hơn đến việc phát triển web và đảm bảo rằng trang web có mã hóa ký tự phù hợp hơn là SEO (tối ưu hóa công cụ tìm kiếm). Nhưng bằng cách đảm bảo rằng nội dung được hiển thị chính xác, điều này có thể ảnh hưởng đến trải nghiệm người dùng và việc thu thập dữ liệu của công cụ tìm kiếm, nó sẽ gián tiếp ảnh hưởng đến SEO.

### Meta Title Tag

```html title='Example'
<title>My docs</title>
```

![Caching next](../images/title-tab.png)

> Cung cấp tiêu đề của trang web trong kết quả tìm kiếm. Thẻ tiêu đề phải rõ ràng và ngắn gọn và phù hợp với nội dung của trang. Đây là yếu tố quan trọng nhất mà các công cụ tìm kiếm xem xét khi xếp hạng các trang của bạn.

### Meta Viewport Tag

```html title='Example'
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

> Thẻ khung nhìn được sử dụng để đo kích thước và chia tỷ lệ nhằm mang lại trải nghiệm người dùng tốt hơn trên các kích thước màn hình khác nhau. Nên sử dụng thẻ `<viewport>` trong tài liệu vì thẻ khung nhìn là yếu tố xếp hạng trong kết quả tìm kiếm.

## Important meta tags

### Meta description tag

```html title='Example'
<meta name="description" content="Short Description" />
```

> Là yếu tố cơ bản trong tối ưu hóa công cụ tìm kiếm (SEO) và phát triển web. Nó là một thuộc tính HTML cung cấp bản tóm tắt ngắn gọn và súc tích về nội dung trên trang web. Các công cụ tìm kiếm như Google thường hiển thị mô tả này trong kết quả tìm kiếm của họ để giúp người dùng hiểu nội dung của một trang web cụ thể.

### Meta keyword tag

```html title='Example'
<meta name="keywords" content="HTML, SEO" />
```

> Thẻ từ khóa meta cung cấp các từ khóa về nội dung của trang web được sử dụng để lập chỉ mục và xếp hạng trang web trong kết quả tìm kiếm.

### Meta Robots Meta Tag

```html title='Example'
<meta name="robots" content="index, follow" />
```

> Thẻ robot được sử dụng để hướng dẫn công cụ tìm kiếm lập chỉ mục và theo dõi các liên kết trên trang. Các hướng dẫn quan trọng trên thẻ robot bao gồm:
>
> - "index": Chỉ mục trang
> - "follow": Thực hiện theo các liên kết
> - "noindex": Không lập chỉ mục trang
> - "nofollow": Đừng theo các liên kết

### Meta Canonical Tag

```html title='Example'
<link rel="canonical" href="URL_of_preferred_page" />
```

> Khi có nhiều phiên bản của cùng một thông tin, thẻ chuẩn, còn được gọi là thẻ “rel=canonical”, là một thành phần HTML được sử dụng trong tối ưu hóa công cụ tìm kiếm (SEO) để chỉ định phiên bản chuẩn hoặc phiên bản ưa thích của một trang web. Nó hỗ trợ các công cụ tìm kiếm xác định phiên bản của trang cần được lập chỉ mục và hiển thị trong kết quả tìm kiếm. Thẻ canonical đặc biệt hữu ích trong việc giải quyết những khó khăn với nội dung trùng lặp.

### Meta Hreflang Tag

```html title='Example'
<link rel="alternate" href="URL_of_alternate_page" hreflang="language_code" />
```

> Một phần tử HTML thiết yếu để tối ưu hóa công cụ tìm kiếm (SEO) là thẻ hreflang, thẻ này xác định ngôn ngữ và nhắm mục tiêu theo địa lý của các trang trực tuyến. Thẻ này hữu ích cho các trang web nước ngoài hoặc đa ngôn ngữ vì nó cho phép các công cụ tìm kiếm hiểu ngôn ngữ và nhắm mục tiêu theo địa lý của nội dung trang.

### Meta Author Tag

```html title='Example'
<meta name="author" content="Author's Name" />
```

> Thẻ `<meta name=”author”>` là một thành phần HTML có thể được sử dụng để chỉ định tác giả của nội dung trang web. Mặc dù thẻ này không phải là yếu tố xếp hạng chính trong SEO nhưng nó vẫn có thể mang lại một số lợi ích, đặc biệt là về mặt phân bổ và độ tin cậy.

### Social Media Meta Tags

`1. og:title`

```html title='Example'
<meta
  property="og:title"
  content="Search Engine Journal - Marketing News, Interviews and How-to Guides"
/>
```

> Tiêu đề mà bạn muốn hiển thị khi trang của bạn được liên kết.

`2. og:url`

```html title='Example'
<meta property="og:url" content="https://www.example.com/" />
```

> Đặt tiêu đề bạn muốn hiển thị khi trang của bạn được liên kết. Nó thường có cùng giá trị với thẻ meta chuẩn.

`3. og:description`

```html title='Example'
<meta
  property="og:description"
  content="Best-in-industry guides and information while cultivating a positive community."
/>
```

> Mô tả trang của bạn. Hãy nhớ rằng Facebook sẽ chỉ hiển thị khoảng 300 ký tự mô tả.

`4. og:image`

```html title='Example'
<meta property="og:image" content="https://www.example.com/sample.jpg" />
```

> Đặt URL của hình ảnh bạn muốn hiển thị khi trang của bạn được liên kết đến.
