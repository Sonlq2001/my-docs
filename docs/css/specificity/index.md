---
sidebar_position: 5
---

# Specificity

Độ ưu tiên bộ chọn trong css.

## Scoring each selector type

### !important

Mức độ ưu tiên cao nhất, với `10,000` điểm.

```css title="Example"
/* class 10 points */
.my-class {
  color: red !important; /* 10,000 points */
  background: white;
}
```

### Inline style attribute

Điểm ưu tiên `1,000`

```html title="Example"
<div style="color: red"></div>
```

### ID selector

Điểm ưu tiên `100`

> Chú ý, không phải `[id="myID"]` ( đây là chọn theo attribute )

```css title="Example"
#myID {
  color: red;
}
```

### Class, pseudo-class, or attribute selector

Điểm ưu tiên `10`

```css title="Example"
/* class selector */
.my-class {
  color: red;
}

/* pseudo-class */
:hover {
  color: red;
}

/* attribute selector */
[href="#"] {
  color: red;
}
```

### Element or pseudo-element selector

Điểm ưu tiên `1`

```css title="Example"
/* type selector */
div {
  color: red;
}

/* pseudo-element selector */
::selection {
  color: red;
}
```

### Universal selector

Điểm ưu tiên `0`

```css title="Example"
* {
  color: red;
}
```

## Specificity in context

```html title="Example"
<a class="my-class another-class" href="#">A link</a>
```

```css title="Example"
/* 1 point */
a {
  color: red;
}

/* 1 + 10 = 11 point */
a.my-class {
  color: blue;
}

/* 1 + 10 + 10 = 21 point */
a.my-class.another-class {
  color: rebeccapurple;
}

/* 1 + 10 + 10 + 10 = 31 point */
a.my-class.another-class[href] {
  color: goldenrod;
}

/* 
a = 1
.my-class = 10
.another-class = 10
[href] = 10
:hover = 10

=> 1 + 10 + 10 + 10 + 10 = 41 point
*/
a.my-class.another-class[href]:hover {
  color: lightgrey;
}
```

## Summary

Bảng sắp mức độ ưu tiên từ `cao` đến `thấp`

| Selector / type                      | Priority (Ưu tiên) | Point (Điểm tính) |
| ------------------------------------ | ------------------ | ----------------- |
| `!important`                         | 1                  | 10,000            |
| `inline style`                       | 2                  | 1,000             |
| `id`                                 | 3                  | 100               |
| `class`, `pseudo-class`, `attribute` | 4                  | 10                |
| `tag`, `pseudo-element`              | 5                  | 1                 |
| `*`                                  | 6                  | 0                 |

:::info[Thông tin]

- Bộ chọn nào có tổng điểm cao hơn sẽ được ưu tiên.

- Selector có cùng độ chi tiết, selector được khai báo và được chạy cuối cùng có độ ưu tiên cao nhất.

:::
