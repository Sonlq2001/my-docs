---
sidebar_position: 1
title: Debounce / Throttle
---

## Debounce

Debounce là một kỹ thuật lập trình dùng để kiểm soát tần suất thực thi của một hàm, đặc biệt khi hàm đó được gọi liên tục trong một khoảng thời gian ngắn.

Mục tiêu chính của debounce là giảm tải cho hệ thống bằng cách trì hoãn việc gọi hàm cho đến khi người dùng ngừng kích hoạt sự kiện trong một khoảng thời gian nhất định

### Một số trường hợp thực tế khi dùng debounce

- **Khi người dùng nhập vào ô tìm kiếm (autocomplete):**
  - Hạn chế việc gửi quá nhiều yêu cầu đến server mỗi khi người dùng gõ phím.
- **Cửa sổ thay đổi kích thước (resize):**
  - Chỉ thực hiện tính toán hoặc vẽ lại sau khi người dùng ngừng thay đổi kích thước cửa sổ.
- **Cuộn trang (scroll):**
  - Giảm số lần gọi hàm xử lý khi người dùng cuộn trang.

### Cách hoạt động

- Mỗi lần sự kiện được kích hoạt, debounce sẽ:
  - Hủy bỏ việc thực thi hàm đã lên lịch trước đó (nếu có).
  - Lên lịch một hàm mới sau một khoảng thời gian cố định (e.g., 300ms).
- Nếu không có sự kiện mới trong khoảng thời gian đó, hàm sẽ được thực thi.

### Triển khai code

```js
function debounce(func, delay) {
  let timeoutId; // Biến lưu trữ ID của bộ hẹn giờ
  return function (...args) {
    // Hủy bỏ hàm trước đó nếu timeoutId đã tồn tại
    clearTimeout(timeoutId);

    // Đặt lại bộ hẹn giờ mới
    timeoutId = setTimeout(() => {
      func.apply(this, args); // Thực thi hàm với ngữ cảnh và tham số ban đầu
    }, delay);
  };
}
```

**Sử dụng debounce**

```js
const debounce = (func, delay = 300) => {
  let timeOut;
  return function (...args) {
    clearTimeout(timeOut);

    timeOut = setTimeout(() => {
      func.apply(this, args);
    }, delay);
  };
};

const handleInit = () => {
  const elButton = document.querySelector("button");

  if (elButton) {
    elButton.addEventListener(
      "click",
      debounce((e) => {
        console.log(e, "debounce click");
      })
    );
  }
};

document.addEventListener("DOMContentLoaded", handleInit);
```

## Throttle

Throttle là một kỹ thuật lập trình dùng để giới hạn số lần thực thi của một hàm trong một khoảng thời gian cố định, ngay cả khi hàm đó được gọi liên tục.

Kỹ thuật này thường được sử dụng để cải thiện hiệu suất trong các trường hợp sự kiện xảy ra liên tục (như cuộn trang, thay đổi kích thước cửa sổ, hoặc kéo thả).

### Một số trường hợp thực tế khi dùng throttle

- **Sự kiện cuộn trang (scroll):**
  - Hạn chế việc gọi hàm khi người dùng cuộn trang liên tục.
- **Sự kiện kéo chuột (drag):**
  - Cập nhật vị trí của phần tử chỉ một lần mỗi khoảng thời gian cố định.
- **Sự kiện resize:**
  - Tính toán kích thước cửa sổ sau mỗi khoảng thời gian nhất định thay vì mỗi lần sự kiện xảy ra.

### Cách hoạt động

- Hàm được thực thi đều đặn sau mỗi khoảng thời gian cố định (ví dụ: 100ms).

- Nếu sự kiện xảy ra liên tục, hàm chỉ được thực thi tối đa một lần trong khoảng thời gian cố định đó.

### Triển khai code

```js
function throttle(func, limit) {
  let lastCall = 0; // Lưu thời gian lần cuối hàm được gọi

  return function (...args) {
    const now = Date.now();

    // Nếu đã qua thời gian giới hạn, thực thi hàm
    if (now - lastCall >= limit) {
      lastCall = now;
      func.apply(this, args); // Thực thi hàm với ngữ cảnh và tham số ban đầu
    }
  };
}
```

## So sánh

| **Tiêu chí**           | **Throttle**                                                 | **Debounce**                                                              |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------------------- |
| **Mục đích**           | Giới hạn tần suất thực thi hàm, đảm bảo nó được gọi đều đặn. | Chỉ thực thi hàm sau khi sự kiện ngừng xảy ra trong một khoảng thời gian. |
| **Ví dụ điển hình**    | Cuộn trang (scroll), kéo chuột (drag).                       | Tìm kiếm (search), resize cửa sổ.                                         |
| **Thời gian thực thi** | Theo chu kỳ cố định.                                         | Chỉ thực thi sau khi sự kiện kết thúc.                                    |
