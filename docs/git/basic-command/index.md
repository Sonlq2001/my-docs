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

## Git version

Kiểm tra phiên bản của Git.

```bash
git -v
```

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

Kiểm tra những file đang được đánh dấu theo dõi các file đang ở `Working directory` hoặc `Staging area`

```bash
git status
```

## Git branch

Giúp chúng ta xác định được vị trí đang ở nhánh nào và hiển thị tất cả các nhánh hiện đang có ở local

```bash
git branch
```

### Git branch -m

Đổi tên nhánh ở local

```bash
git checkout -m <oldname> <newname>
```

- `oldname`: là nhánh mà bạn muốn đổi tên.
- `newname`: là nhánh mới mà bạn muốn đổi tên sang.

## Git add

Đưa những file từ `Working directory` sang trạng thái `Staging area`. Trạng thái `sẵn sàng để thực hiện commit`.

### Git add .

Đưa `tất cả các file` từ `Working directory` sang trạng thái `Staging area`.

```bash
git add .
```

### Git add path_file

Chỉ định file được để đưa sang trạng thái `Staging area`.

```bash
git add path_file
```

:::info[Thông tin]
`git add .` dấu (`.`) đằng sau sẽ áp dụng đưa tất cả những file đang được `git` đánh dấu theo dõi sang `Staging area`

`git add index.html` đường dẫn file đằng sau (vd: `index.html`), sẽ chỉ định những file cần được sang `Staging area`
:::

## Git show

Xem chi tiết mở rộng nội dung `commit`

```bash
git show id_commit
```

## Git diff

## Git commit

Ghi lại các thay đổi vào kho lưu trữ.

```bash
git commit -m "message"
```

:::tip[TIP]
Cách đặt tên branch hay commit nên rõ ràng, thể hiện branch đó, commit đó thực hiện feature gì hay là fix bug gì... (thường thì sẽ theo quy định của công ty)
:::

### Git commit --amend

Dùng để sửa đổi lại `commit` gần nhất, thay đổi lại `commit` mới gần nhất

```bash
git commit --amend -m "message"
```

> Sử dụng `git push origin branch_name -f` để hoàn tất việc đưa commit lên.

:::warning[Chú ý]
Việc sử dụng `--amend` có thể gây nguy hiểm, do đã xáo chộn lịch sử `commit`, tránh thực hiện các thay đổi ghi lại lịch sử vào kho lưu trữ từ xa, đặc biệt nếu đang làm việc chung dự án và cùng repo cũng các thành viên khác.
:::

## Git log

Xem lại lịch sử các `commit`

```bash
git log
```

## Git push

Đẩy các `commit` từ `local` lên trên `remote`

```bash
git push origin branch_mane
```

### Git push -f

## Git pull

Kéo các `commit` (code) từ trên `remote` về máy ở `local`

```bash
git pull origin branch_mane
```

## Git checkout

### Git checkout -b

Tạo ra 1 nhánh mới và chuyển sang nhánh đó

```bash
git checkout -b branch_mane
```

### Git checkout file

- Giúp sao chép, kiểm tra nội dung file trong 1 nhánh khác, `a` -> `b`
- Giúp hoàn nguyên lại nội dung đã sửa trong file ( khi đẩy nhầm file không liên quan vào trong `commit` )

```bash
git checkout branch_name path_file
```

> Khi thực hiện thành công, các file sẽ được ở sẵn trạng thái `Staging area`

## Git fetch

Dùng để tải các cập nhập thay đổi từ các nhánh trên `remote` về `local` mà không cần `merge`.

Cho phép bạn xem những thay đổi mới nhất mà không cần sửa đổi thư mục làm việc hiện tại của bạn.

```bash
git fetch
```
