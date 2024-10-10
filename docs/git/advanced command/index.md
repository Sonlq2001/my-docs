---
sidebar_position: 4
---

# Advanced command

## Git reset

Dùng để hoàn tác, hủy `commit` hoặc hủy đưa thay đổi từ `Staging area` sang `Working directory`

```bash
git reset
```

### Git reset HEAD~n

Hoàn tác quay trở lại với số lượng `commit` mà bạn muốn chỉ định.

```bash
git reset HEAD~n
```

- `n` số lượng `commit` là bạn muốn hoàn tác quay trở lại trước đó.

```bash title="Example"
git reset HEAD~2
# Hoàn tác trở lại 2 commit mới nhất
```

### --hard

`--hard` có nghĩa là bỏ commit đi và bỏ cả những thay đổi chưa được commit trong working space. Khi này môi trường sẽ hoàn toàn “sạch sẽ” như thời điểm trước khi commit.

```bash
git reset --hard HEAD^n
```

### --soft

`--soft` có nghĩa là bỏ commit đi nhưng giữ nguyên những thay đổi chưa được commit trong working space. --soft hữu dụng khi bạn muốn giữ lại những thay đổi chưa commit cho lần commit tiếp theo.

```bash
git reset --soft HEAD^n
```

## Git merge

## Git cherry pick

## Git revert

## Git stash

## Git rebase

## Git reflog
