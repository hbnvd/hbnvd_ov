---
tags:
  - DSA/Sliding-window
  - DSA/two-pointers
  - DSA/Sub-array
cssclasses: "[[Two pointers]]"
---
- **Bản chất**: là 1 dạng mở rộng của [[Two pointers]] , có thêm 1 hoặc nhiều biến phụ để lưu đặc điểm như tổng, số lượng phần tử, ... của vùng bên trong 2 pointer. Thường chạy từ trái qua phải.

- **Tài liệu tham khảo**: 
	1. https://www.geeksforgeeks.org/dsa/window-sliding-technique/
	2. https://usaco.guide/gold/sliding-window?lang=cpp

---
# Mục lục
1. [[#Các dạng phổ biến]]
	1. [[#Fixed size - kích thước cố định]]
	2. [[#Dynamic size - kích thước động]]
2. [[#Bug từng gặp]]
# Các dạng phổ biến
## Fixed size - kích thước cố định
- 2 con trỏ luôn giữ cùng 1 `khoảng cách k`, k là hằng số.

**Easy:**
- https://www.geeksforgeeks.org/dsa/find-maximum-minimum-sum-subarray-size-k/
- 
## Dynamic size - kích thước động
- Cái này liên quan nhiều tới [[Two pointers]], phải hiểu được tư duy điều kiện của 2 con trỏ mới làm được mấy bài kiểu này

**Easy**:
- [[CP00008]]
# Bug từng gặp
- Tăng biên phải $r$ không đúng lúc.

# More bài
- https://www.geeksforgeeks.org/dsa/top-problems-on-sliding-window-technique-for-interviews/
- Leetcoode