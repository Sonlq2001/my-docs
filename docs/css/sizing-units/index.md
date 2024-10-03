---
side_position: 6
---

# Sizing Units

## Numbers

Các số được sử dụng để xác định độ mờ (`opacity`), chiều cao dòng (`line-height`), cho các giá trị màu trong `rgb` và rất nhiều thuộc tính css sử dụng giá trị số.

Số là số nguyên (`1, 2, 100 ...`) hoặc số thập phân (`0.2, 0.4 ...`).

```css title="Example"
p {
  line-height: 1.5;
  opacity: 0.5;
}
```

## Percentages

Đơn vị phần trăm (`%`) trong css. Được tính toán tỷ lệ dựa trên kích thước của phần tử cha.

```css title="Example"
div {
  width: 100px;
  height: 100px;
  background-color: #7e60bf;
}
p {
  width: 50%; /* Chiếm 1 nửa chiều rộng so với phần tử cha  */
  height: 50%; /* Chiếm 1 nửa chiều cao so với phần tử cha  */
  background-color: #e4b1f0;
}
/* 
  - Kích thước chiều rộng = 50px (100 / 2)
  - Kích thước chiều cao = 50px (100 / 2)
  */
```

```html title="Example"
<div>
  <p></p>
</div>
```

![size1](../images/size1.png)

<!-- ![inheritance](../images/inheritance1.png) -->

## Dimensions and lengths

### Absolute lengths

Tất cả độ dài tuyệt đối đều phân giải dựa trên cùng một cơ sở, giúp chúng có thể dự đoán được ở bất kỳ nơi nào chúng được sử dụng trong CSS của bạn. Ví dụ: nếu bạn sử dụng cm để định cỡ phần tử của mình rồi in, thì kết quả sẽ chính xác nếu bạn so sánh nó với thước kẻ.

> Độ dài tuyệt đối thực sự có thể có ích khi thiết kế để in.

| Unit | Name        | Equivalent to       |
| ---- | ----------- | ------------------- |
| cm   | Centimeters | 1cm = 96px/2.54     |
| mm   | Millimeters | 1mm = 1/10th of 1cm |
| in   | Inches      | 1in = 2.54cm = 96px |
| pt   | Points      | 1pt = 1/72th of 1in |
| px   | Pixels      | 1px = 1/96th of 1in |
| ...  | ...         | ...                 |

**Đơn vị tuyệt đối hay dùng**

`px`: là đơn vị 1 điểm ảnh trên màn hình. Mành mình có độ phân giải càng cao, càng nhiều điểm pixel.

### Relative lengths

- Độ dài tương đối được tính theo giá trị cơ bản, giống như tỷ lệ phần trăm. Sự khác biệt giữa tỷ lệ này và tỷ lệ phần trăm là bạn có thể định cỡ các phần tử theo ngữ cảnh. Điều này có nghĩa là CSS có các đơn vị như ch sử dụng kích thước văn bản làm cơ sở và vw dựa trên chiều rộng của khung nhìn (cửa sổ trình duyệt của bạn). Độ dài tương đối đặc biệt hữu ích trên web do tính chất đáp ứng của nó.

#### Font-size-relative units

| Unit | relative to:                                                                        |
| ---- | ----------------------------------------------------------------------------------- |
| em   | Nó sẽ được tính toán theo phần tử gần nhất có thuộc tính `font-size`                |
| rem  | Nó sẽ được tính toán font-size dựa theo phần tử `root` (`html`) (mặc định là 16px). |
| ...  | ...                                                                                 |

**Đơn vị tương đối hay dùng**

`rem`: Nó sẽ được tính toán font-size dựa theo phần tử `root` (`html`) (mặc định là 16px).

```css title="Example"
html {
  font-size: 20px;
}

p {
  font-size: 2rem;
}
/* 2rem => 40px */
```

:::tip[Tip]

Sử dụng `html{ font-size: 62.5%; }`, nó sẽ tương đương `10px` và bằng `1rem`

VD: `2rem => 20px`

:::

#### Viewport-relative units

| Unit | relative to:                       |
| ---- | ---------------------------------- |
| vw   | dựa trên chiều rộng của khung nhìn |
| vh   | dựa trên chiều cao của khung nhìn  |
| ...  | ...                                |

## Miscellaneous units

### Angle units

`deg` đơn vị góc

```css title="Example"
div {
  transform: rotate(60deg);
}
/* 60deg tương đương 60 độ */
```
