---
sidebar_position: 2
title: Dockerfile
---

Dockerfile là một tệp văn bản (text file) chứa các hướng dẫn (instructions) để xây dựng một **Docker image**.

Docker image này sau đó có thể được sử dụng để chạy các **container**, là các môi trường độc lập để chạy ứng dụng hoặc dịch vụ.

Nói đơn giản, Dockerfile giống như một "công thức" hay "hướng dẫn nấu ăn" mà bạn cung cấp cho Docker để nó biết cách tạo ra một môi trường chạy ứng dụng của bạn, bao gồm hệ điều hành, phần mềm, thư viện, mã nguồn, và các thiết lập cần thiết.

![ex1](../images/ex4.png)

### Ví dụ về dockerfile

```dockerfile
# Sử dụng image Python chính thức làm nền tảng
FROM python:3.9-slim

# Thiết lập thư mục làm việc
WORKDIR /usr/src/app

# Sao chép file requirements.txt vào image
COPY requirements.txt ./

# Cài đặt các thư viện Python từ requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Sao chép toàn bộ mã nguồn vào image
COPY . .

# Chạy ứng dụng khi container khởi động
CMD ["python", "main.py"]
```

### Cấu trúc cơ bản của Dockerfile

Một Dockerfile bao gồm các lệnh được viết theo cú pháp cụ thể. Dưới đây là các lệnh phổ biến và ý nghĩa của chúng:

- **FROM**: Chỉ định image cơ sở (base image) để bắt đầu.

  - Ví dụ: `FROM` `ubuntu:20.04` nghĩa là image được xây dựng dựa trên Ubuntu phiên bản 20.04.
  - Đây thường là dòng đầu tiên trong Dockerfile.

- **RUN**: Thực thi các lệnh trong quá trình xây dựng image.

  - Ví dụ: `RUN apt-get update && apt-get install -y python3` sẽ cập nhật gói và cài Python 3.

- **COPY**: Sao chép tệp hoặc thư mục từ máy host (máy của bạn) vào image.

  - Ví dụ: `COPY . /app` sao chép toàn bộ nội dung thư mục hiện tại vào thư mục /app trong image.

- **WORKDIR**: Đặt thư mục làm việc mặc định cho các lệnh tiếp theo.

  - Ví dụ: `WORKDIR /app` đặt thư mục làm việc là /app.

- **EXPOSE**: Thông báo cổng mà container sẽ lắng nghe (không thực sự mở cổng, chỉ mang tính tài liệu).

  - Ví dụ: `EXPOSE 8080` cho biết container sẽ chạy trên cổng 8080.

- **CMD**: Chỉ định lệnh mặc định để chạy khi container khởi động.

  - Ví dụ: `CMD ["python3", "app.py"]` sẽ chạy tệp app.py bằng Python 3 khi container khởi động.
  - Chỉ có một CMD được thực thi; nếu có nhiều CMD, chỉ cái cuối cùng có hiệu lực.

- **ENTRYPOINT** (tuỳ chọn): Cung cấp lệnh chính để chạy, thường kết hợp với CMD để linh hoạt hơn.

  - Ví dụ: ENTRYPOINT `["python3"]` và CMD `["app.py"]` cho phép bạn chạy app.py hoặc tệp khác nếu cần.

- **ENV**: Thiết lập biến môi trường trong image.

  - Ví dụ: `ENV MY_VAR=value` tạo biến môi trường MY_VAR với giá trị value.

### Quy trình hoạt động của Dockerfile

1.  **Build**: Khi bạn chạy docker build, Docker thực thi từng lệnh trong Dockerfile từ trên xuống dưới.
2.  **Layering**: Mỗi lệnh tạo ra một "lớp" (layer) trong image. Nếu một lệnh không thay đổi, Docker sẽ dùng lại layer đã lưu trong cache để tăng tốc độ.
3.  **Container**: Image hoàn chỉnh được dùng để khởi tạo container.
