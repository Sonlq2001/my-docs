---
title: Q & A
---

# Q & A

## Sự khác nhau giữa `git merge` và `git pull`

![ex1](./images/ex1.avif)

- `git pull` sẽ tương tự như `git fetch` + `git merge`

```bash
git pull <remote> <branch>
```

Tương tự như

```bash
git fetch <remote>
git merge <remote>/<branch>
```

### **`git pull`**

- **Mục đích**: Kéo về các thay đổi mới nhất từ một nhánh trên **remote repository** và hợp nhất chúng vào nhánh hiện tại trong **local repository**.

- **Hoạt động**:

  - `git pull` thực chất là một lệnh **tổ hợp** của hai lệnh:
    1.  `git fetch` -- tải xuống (fetch) các thay đổi từ remote repository.
    2.  `git merge` -- hợp nhất (merge) những thay đổi đó vào nhánh hiện tại.

```bash
git pull origin master
```

- Lệnh này sẽ lấy tất cả các thay đổi từ nhánh `main` trên remote repository `origin` và hợp nhất chúng vào nhánh hiện tại trên local repository.

- **Đặc điểm nổi bật**:
  - Tương tác với **remote repository**.
  - Tự động thực hiện cả hai bước `fetch` và `merge` trong một lệnh.

### **`git merge`**

**Mục đích**: Hợp nhất (merge) hai nhánh trên **local repository**.

- **Hoạt động**:

  - `git merge` dùng để tích hợp các thay đổi từ một nhánh khác (ví dụ: `feature`) vào nhánh hiện tại (ví dụ: `main`).

```bash
git merge feature-branch
```

- Lệnh này sẽ hợp nhất các thay đổi từ nhánh `feature-branch` vào nhánh hiện tại.

- **Đặc điểm nổi bật**:

  - Chỉ hoạt động trên **local repository**.
  - Không liên quan đến remote repository.

### So sánh nhanh

| **Tiêu chí**              | **`git pull`**                              | **`git merge`**                          |
| ------------------------- | ------------------------------------------- | ---------------------------------------- |
| **Phạm vi**               | Tương tác với **remote repository**         | Chỉ trong **local repository**           |
| **Tác dụng**              | Fetch + Merge thay đổi từ remote repository | Hợp nhất hai nhánh trên local repository |
| **Khi nào dùng?**         | Khi muốn cập nhật local với remote          | Khi muốn hợp nhất các nhánh local        |
| **Thực hiện bước fetch?** | Có                                          | Không                                    |

**Lưu ý:**

- **`git pull`** có thể gây xung đột (conflict) nếu remote repository có những thay đổi không tương thích với local repository. Vì vậy, trong nhiều trường hợp, người ta thường dùng `git fetch` trước để kiểm tra các thay đổi và sau đó thực hiện `git merge` nếu cần.
- **`git merge`** không tải xuống dữ liệu từ remote repository, vì vậy nó chỉ thích hợp khi bạn đã có các nhánh cần thiết trên local.
