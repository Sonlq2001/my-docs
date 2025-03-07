---
sidebar_position: 4
title: Image
---

Docker Image là một **template bất biến (immutable)** chứa tất cả các thành phần cần thiết (code, thư viện, dependencies, cấu hình môi trường,...) để chạy một ứng dụng.

Hiểu đơn giản, **Image giống như một bản đóng gói hoàn chỉnh của ứng dụng**, đảm bảo rằng ứng dụng của bạn có thể chạy đồng nhất trên mọi môi trường (local, staging, production).

![ex1](../images/ex2.png)

### 🎯 **Đặc điểm của Docker Image**

- **Immutable (Bất biến)**: Khi Image được tạo ra, nó không thể thay đổi. Nếu cần chỉnh sửa, bạn phải tạo một Image mới (`build lại`) .
- **Layered Structure (Cấu trúc tầng)**:
  - Mỗi Image được xây dựng từ nhiều lớp (layer).
  - Mỗi lệnh trong Dockerfile (ví dụ: `FROM`, `RUN`, `COPY`) sẽ tạo ra một layer mới.
  - Các layer được cache lại giúp tăng tốc quá trình build.
- **Portable (Di động)**: Bạn có thể đẩy Image lên Docker Hub hoặc các registry khác và chạy ở bất kỳ đâu có Docker.

### 📌 **Image vs Container**

| Docker Image       | Docker Container               |
| ------------------ | ------------------------------ |
| Là template        | Là instance chạy từ Image      |
| Không thay đổi     | Có thể thay đổi trong khi chạy |
| Chỉ dùng để build  | Dùng để chạy ứng dụng          |
| Giống như file ISO | Giống như máy ảo đang chạy     |

### 🎯 **Tóm tắt**

👉 Docker Image là bản đóng gói đầy đủ của ứng dụng, đảm bảo tính đồng nhất trên mọi môi trường.\
👉 Từ một Image, bạn có thể tạo ra nhiều Container giống nhau.
