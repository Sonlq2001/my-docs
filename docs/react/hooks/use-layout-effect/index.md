---
sidebar_position: 9
---

# useLayoutEffect

`useLayoutEffect` là một React Hook hoạt động tương tự như useEffect, nhưng có sự khác biệt quan trọng về thời điểm thực thi.

Trong khi useEffect chạy sau khi render (khi giao diện đã được vẽ ra màn hình), useLayoutEffect chạy ngay sau khi DOM đã được cập nhật nhưng trước khi giao diện được vẽ.

<!-- 5 // 2. Cập nhật DOM (mutated)
23
2
3
// useEffect
4
// 1. Cập nhật lại state
6
// 3. Render lại UI
7
8
9
// 4. Gọi Cleanup nếu deps thay đổi
// 5. Gọi useEffect callback
10 // useLayoutEffect
11
// 1. Cập nhật lại state
12 // 2. Cập nhật DOM (mutated)
13
// 3. Gọi cleanup nếu deps thay đổi (sync) 14 // 4. Gọi useLayoutEffect callback (sync) 15 // 5. Render lại UI
16 -->

<!-- TODO: update later -->
