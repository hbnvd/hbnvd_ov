#DSA/two-pointers #DSA/BigO/n

- **Tối ưu hóa độ phức tạp:** Chuyển đổi các bài toán duyệt mảng/chuỗi từ hai vòng lặp lồng nhau $O(N^2)$ về một vòng lặp đơn $O(N)$ bằng cách cho hai con trỏ di chuyển tịnh tiến theo một hướng hoặc ngược hướng nhau.
- **Tiết kiệm bộ nhớ:** Giải quyết cấu trúc đoạn, tìm kiếm cặp phần tử hoặc chuỗi con thỏa mãn điều kiện trực tiếp trên mảng hiện tại với độ phức tạp không gian lưu trữ tối ưu $O(1)$.

---
Nguồn:
- Khái niệm
	- https://viblo.asia/p/ky-thuat-two-pointers-trong-thuat-toan-PwlVmeZPV5Z
	- https://usaco.guide/silver/two-pointers?lang=cpp
- Bài tập
	- https://wiki.vnoi.info/algo/basic/two-pointers.md - Nên đọc cái này cùng với khái niệm.
	- https://leetcode.com/problem-list/two-pointers/

---
Chương này bao gồm:
1. Khái niệm
2. Ứng dụng

---
# I.Khái niệm
- 2 con trỏ là kĩ thuật sử dụng 2 biến chỉ số để duyệt qua 1 hoặc nhiều mảng nhằm tìm kiếm kết quả thỏa mãn điều kiện bài toán.
- Có thể sửa đổi hướng đi, điều kiện di chuyển của con trỏ để phù hợp với bài toán cụ thể.
# II. Ứng dụng
Các ứng dụng cơ bản của 2 con trỏ trong giải thuật
## 1. Gộp tập
- https://wiki.vnoi.info/algo/basic/two-pointers.md - bài 1
Cho 2 mảng số nguyên đã sắp xếp không giảm $A$ và $B$ có $n$ và $m$ phần tử. Nhiệm vụ của bạn là làm sao cho tạo ra mảng $C$ được gộp từ các phần tử của $A$ và $B$ và **cũng sắp xếp theo thứ tự không giảm**.
GIới hạn: $n,m\le 10^5$ và $0 \le A_i, B_i \le 10^9$
- Ta có thể cho 2 con trỏ lần lượt là $i$ và $j$ duyệt qua $A$ và $B$.
- Cách giải chi tiết ở [[CP00006]]
## 2. Hai con trỏ chạy ngược chiều
- https://wiki.vnoi.info/algo/basic/two-pointers.md bài 2
...
- Cách giải chi tiết ở [[CP00007]]
## 3. Hai con trỏ chạy cùng chiều
- 1 con thêm, 1 con bớt ;))
- Kiểu kiểu dynamic sliding window á

- https://wiki.vnoi.info/algo/basic/two-pointers.md bài 3
...
- Cách giải chi tiết ở [[CP00008]]
## 4. 
- https://wiki.vnoi.info/algo/basic/two-pointers.md bài 4
- Bài này thì toi đách hiểu gì hết á;)), nhưng mà nó có liên quan tới rùa và thỏ