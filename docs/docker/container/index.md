---
sidebar_position: 3
title: Container
---

**Container** là một đơn vị phần mềm nhẹ, độc lập, chứa tất cả các thành phần cần thiết để chạy một ứng dụng, bao gồm mã nguồn, thư viện, công cụ và các phụ thuộc.

Container được tạo ra từ **Docker Image** và chạy như một tiến trình độc lập trên hệ thống.

Mỗi container được cô lập với các container khác và với hệ thống host, nhưng có thể giao tiếp với bên ngoài thông qua các cổng mạng hoặc volume.

![ex3](../images/ex3.png)

### So sánh Container với Máy ảo (VM)

| Đặc điểm               | Container                           | Máy ảo (VM)                       |
| ---------------------- | ----------------------------------- | --------------------------------- |
| **Cô lập**             | Cô lập ở mức tiến trình (process)   | Cô lập ở mức phần cứng (hardware) |
| **Hiệu suất**          | Nhẹ, khởi động nhanh                | Nặng, khởi động chậm hơn          |
| **Tài nguyên**         | Chia sẻ kernel với host             | Cần hệ điều hành riêng            |
| **Kích thước**         | Nhỏ (MB)                            | Lớn (GB)                          |
| **Khả năng di chuyển** | Dễ dàng di chuyển giữa các hệ thống | Phức tạp hơn do kích thước lớn    |

### Lợi ích của Container

1.  **Tính nhất quán**:

    - Ứng dụng chạy nhất quán trên mọi môi trường (development, testing, production).

2.  **Tính di động**:

    - Container có thể dễ dàng di chuyển giữa các hệ thống khác nhau.

3.  **Hiệu suất cao**:

    - Container nhẹ hơn máy ảo, khởi động nhanh và tiêu thụ ít tài nguyên hơn.

4.  **Cô lập**:

    - Mỗi container chạy độc lập, không ảnh hưởng đến các container khác hoặc hệ thống host.

5.  **Dễ dàng mở rộng**:

    - Có thể dễ dàng mở rộng ứng dụng bằng cách chạy nhiều container cùng lúc.
