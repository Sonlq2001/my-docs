---
sidebar_position: 5
---

# Conditional Rendering

## `v-if` và `v-show`

Cả `v-if` và `v-show` đều được sử dụng để điều khiển hiển thị các phần tử trong DOM, nhưng chúng hoạt động theo cách khác nhau.

### **1\. Cách hoạt động**

#### **`v-if`**

- Phần tử **được thêm hoặc xóa khỏi DOM** dựa trên điều kiện.
- Nếu điều kiện là `false`, phần tử sẽ không tồn tại trong DOM.

#### **`v-show`**

- Phần tử **luôn tồn tại trong DOM**, nhưng thuộc tính CSS `display` của nó sẽ được điều chỉnh:
  - Khi điều kiện là `true`, CSS: `display: block;`
  - Khi điều kiện là `false`, CSS: `display: none;`

---

### **2\. Hiệu suất**

#### **`v-if`**

- Có chi phí hiệu suất cao hơn khi điều kiện thay đổi liên tục, vì nó phải thực hiện việc thêm hoặc xóa phần tử khỏi DOM.
- Thích hợp cho các trường hợp mà điều kiện hiếm khi thay đổi.

#### **`v-show`**

- Có chi phí ban đầu cao hơn vì phần tử luôn được thêm vào DOM, bất kể điều kiện.
- Thích hợp cho các trường hợp mà điều kiện thay đổi thường xuyên, vì chỉ cần điều chỉnh thuộc tính CSS.

| **Đặc điểm**           | **`v-if`**                                     | **`v-show`**                                   |
| ---------------------- | ---------------------------------------------- | ---------------------------------------------- |
| **Hiển thị trong DOM** | Có/Không (Thêm hoặc xóa khỏi DOM)              | Luôn tồn tại, điều chỉnh bằng CSS.             |
| **Chi phí hiệu suất**  | Cao hơn khi điều kiện thay đổi liên tục.       | Cao hơn khi tải ban đầu.                       |
| **Thích hợp khi**      | Điều kiện thay đổi ít.                         | Điều kiện thay đổi thường xuyên.               |
| **Điểm mạnh**          | Loại bỏ hoàn toàn phần tử khi không cần thiết. | Ẩn/hiện nhanh chóng mà không cần thao tác DOM. |

:::info

- Sử dụng `v-if` khi bạn muốn tiết kiệm tài nguyên và phần tử chỉ được hiển thị khi thật sự cần thiết.
- Sử dụng `v-show` khi bạn cần hiển thị/ẩn phần tử thường xuyên mà không cần thao tác DOM.

:::
