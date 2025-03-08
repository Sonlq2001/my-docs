---
sidebar_position: 1
title: Image layers
---

Trong Docker, **Image Layer (tầng ảnh)** là các lớp thành phần giúp cấu trúc nên một Docker Image.

Hiểu đơn giản: 👉 Docker Image không phải là một file duy nhất, mà được tạo thành từ nhiều **layer chồng lên nhau**.\
👉 Mỗi layer đại diện cho **một thay đổi (command)** được thực hiện trong file **Dockerfile**.

### 🔑 **Cách hoạt động của Image Layers**

Docker sử dụng hệ thống **Union File System (UnionFS)** để kết hợp các layer lại với nhau.

Mỗi layer trong Image là:

- **Read-only (Chỉ đọc)**: Không thể thay đổi được.
- Được tạo ra bởi các lệnh trong **Dockerfile** như:
  - `FROM`
  - `RUN`
  - `COPY`
  - `ADD`
- Layer mới chỉ lưu lại **phần thay đổi** so với layer trước đó.

```dockerfile
# Layer 1
FROM node:18    # Base image (Layer 1)

# Layer 2
WORKDIR /app    # Tạo thư mục làm việc

# Layer 3
COPY package.json .  # Copy file package.json

# Layer 4
RUN npm install      # Cài đặt dependencies

# Layer 5
COPY . .            # Copy toàn bộ source code

# Layer 6
EXPOSE 3000         # Mở cổng 3000

# Layer 7
CMD ["node", "index.js"]  # Chạy ứng dụng
```

### 🔥 **Docker sẽ tạo ra các layer như sau:**

| Layer   | Nội dung          | Loại Layer | Ghi chú                              |
| ------- | ----------------- | ---------- | ------------------------------------ |
| Layer 1 | node:18           | Read-only  | Base Image                           |
| Layer 2 | `/app`            | Read-only  | Tạo thư mục làm việc                 |
| Layer 3 | Copy package.json | Read-only  | Chỉ copy file                        |
| Layer 4 | npm install       | Read-only  | Cài đặt dependencies (tốn thời gian) |
| Layer 5 | Copy source code  | Read-only  | Copy toàn bộ mã nguồn                |
| Layer 6 | Expose port       | Read-only  | Chỉ định port chạy app               |
| Layer 7 | Chạy ứng dụng     | Read-only  | Lệnh CMD                             |

### 🔥 **Layer Caching (Tối ưu hóa Build)**

Docker có khả năng **cache lại các layer** để tối ưu tốc độ build.

Ví dụ:

- Nếu bạn chỉ thay đổi code trong layer 5, Docker sẽ không build lại từ đầu.
- Nó chỉ build lại từ **layer 5 trở đi**.

### 🧠 **Mẹo tối ưu Image với Layers**

1.  Đưa những lệnh ít thay đổi lên trên.
2.  COPY package.json và `npm install` **trước** khi copy toàn bộ code (để cache dependencies).
3.  Xóa các file không cần thiết (node_modules, logs,...) trước khi build.

```dockerfile
FROM node:18

WORKDIR /app

# Copy và cài đặt dependencies trước
COPY package.json package-lock.json ./
RUN npm install --production

# Copy toàn bộ source code
COPY . .

# Expose port và chạy app
EXPOSE 3000
CMD ["node", "index.js"]
```

### 🎯 **Tóm tắt quy tắc**

| Hành động | Layer mới | Cache                            |
| --------- | --------- | -------------------------------- |
| FROM      | ✅        | ❌                               |
| WORKDIR   | ✅        | ✅                               |
| COPY      | ✅        | ✅ (Nếu nội dung không thay đổi) |
| RUN       | ✅        | ✅ (Nếu lệnh giống nhau)         |
| CMD       | ✅        | ❌                               |

### 🧐 **Lợi ích của Image Layer là gì?**

| Lợi ích              | Giải thích                       |
| -------------------- | -------------------------------- |
| Tối ưu tốc độ        | Chỉ build lại các layer thay đổi |
| Tiết kiệm dung lượng | Tái sử dụng layer chung          |
| Triển khai nhanh     | Image nhỏ hơn, build nhanh hơn   |
