---
sidebar_position: 1
---

# JSX

## What is JSX ?

JSX (JavaScript XML) là một phần mở rộng của ngôn ngữ JavaScript.

Được sử dụng chủ yếu trong các thư viện và framework JavaScript như React. JSX giúp tạo ra cú pháp giống HTML để mô tả cấu trúc và giao diện người dùng trong các ứng dụng web. JSX cho phép việc viết mã JavaScript và HTML trong một file duy nhất, tạo ra mã nguồn dễ đọc và hiểu hơn.

```jsx
const element = <h1>Hello, world!</h1>;
```

:::warning Lưu ý
JSX không phải là HTML
:::

```jsx
// HTML
<div class="container"></div>

// JSX
<div className="container"></div>

// Khi viết JSX class -> className
```

`HTML` tag không cần đóng cũng được nhưng `JSX` cần thiết phải đóng tag.

## Why use JSX ?

Không bắt buộc phải dùng `JSX` trong react. Nhưng có nhiều lý do khiến chúng trở nên phổ biến:

- JSX với cú pháp gần giống XML, cấu trúc cây khi biểu thị các attributes, điều đó giúp ta dễ dàng định nghĩa, quản lý được các component phức tạp, thay vì việc phải định nghĩa và gọi ra nhiều hàm hoặc object trong javascript. Code JSX ngắn hơn, dễ hiểu hơn code JS.

- JSX không làm thay đổi ngữ nghĩa của Javascript

- Cách viết gần với các thẻ HTML, giúp đọc code một cách dễ dàng, debug, sửa nhanh chóng hơn.

```jsx
// Code viết bằng JSX

<DashboardUnit data-index="2">
  <h1>Scores</h1>
  <Scoreboard className="results" scores={gameScores} />
</DashboardUnit>
```

```jsx
// Code viết bằng JS
React.createElement(
  DashboardUnit,
  { "data-index": "2" },
  React.createElement("h1", null, "Scores"),
  React.createElement(Scoreboard, { className: "results", scores: gameScores })
);
```

:::info Thông tin
JSX dùng `Babel` để thông dịch biên dịch ra các mã JS hợp lệ chạy trên trình duyệt.
:::
