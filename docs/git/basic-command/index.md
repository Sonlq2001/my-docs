---
sidebar_position: 3
---

# Basic command

## Git init

Khỏi tạo `git`, yêu theo dõi các sự thay đổi cho dự án.

```bash
git init
```

> Thường được dùng khi mới tạo repo dự án.

## Git config

Thiết lập `tên` và `email` đại diện.

```bash
git config --global user.name "User Name"
git config --global user.email "username@gmail.com"
```

**Lưu ý**:

> `--global` được sử dụng để áp dụng cho tất cả các projects. Nếu không sử dụng `--global` thì settings sẽ chỉ dùng cho riêng project đó.

## Git clone

Tải dự án từ trên remote về máy ở local.

```bash
git clone https://github.com/user/repository.git
```

## Git status

Kiểm tra những file đang được đánh dấu theo dõi do có sự thay đổi và trạng thái của các file đang ở `Working directory` hoặc `Staging area`

```bash
git status
```

## Git branch

Hiển thị tất cả các nhánh hiện đang có ở local

```bash
git branch
```
