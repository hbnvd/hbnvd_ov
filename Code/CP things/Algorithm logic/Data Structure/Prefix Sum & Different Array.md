---
tags:
  - DSA/DS/Prefix-sum
  - "#DSA/DS/Different-array"
---


- Mảng cộng dồn & mảng hiệu
- 1 cấu trúc dữ liệu chuyển tốc độ truy vấn tính tổng, hiệu 1 đoạn con lên O(1)

---
- Nguồn
	- https://wiki.vnoi.info/algo/data-structures/prefix-sum-and-difference-array.md
	- https://codeforces.com/blog/entry/78762
---
Chương này bao gồm:
1. Khái niệm
2. Tính chất
3. Ứng dụng
4. Bài

---
# I. Khái niệm
## Prefix Sum
- Gọi $S$ là `mảng cộng dồn` hay `mảng tiền tố` theo $c$ của mảng $A$
- Với số thực $c$ cho trước, `S[0] = c`
- Mảng cộng dồn $S$ dựa trên công thức $$S_i=S_{i-1}+A_{i}=c+\sum_{j=1}^{i}A_j$$
- Ta kí hiệu `S(c, A)` là mảng cộng dồn của mảng $A$ với hằng số $c$
![[Pasted image 20260529171339.png]]

## Difference Array
- Gọi $D$ là `mảng hiệu` của $A$
- Mảng hiệu $D$ dựa trên công thức: 
$$D_i=A_i-A_{i-1}$$
%%Trên vnoi là A_{i+1} - A_i cơ nhưng tôi đ thích:>%%
- Ta kí hiệu `D(A)` là mảng hiệu của mảng $A$
![[Pasted image 20260529203103.png]]
# II. Tính chất
## Tính riêng biệt
- Từ một mảng $A$ bất kỳ, ta sinh được vô hạn mảng cộng dồn $S(c ,A)$ từ $A$. Tuy nhiên, các mảng cộng dồn này chỉ khác nhau ở giá trị $c$ được chọn.
- Cũng với mảng $A$ đó, ta sinh được **một và chỉ một** mảng hiệu $D(A)$ từ $A$.
## Liên hệ giữa mảng cộng dồn và mảng hiệu
$$S(A_0,D(A))=A \space\space\space\space(1)$$
$$D(S(c, A)) = A\space\space\space\space(2)$$
- $(2)$ hiệu nghiệm với mọi $c$ thực
# III. Ứng dụng
## Prefix Sum
- Định nghĩa $A.sum(i, j)$ là tổng các giá trị của $A$ trong đoạn $[i, j]$
- Prf sum giúp ta truy vấn $A.sum(l,r)$ với độ phức tạp O(1) thay vì O(n)
- Với $S_i = A.sum(1, i)$ ,cho trước 2 số nguyên $l, r$ trong đoạn $1\leq l\leq r\leq n$ , ta có thể hiểu như sau:
![[Pasted image 20260529203905.png]]
- Như vậy có thể hiểu $S_r-S_l=A.sum(l+1, r)$ hay $S_r - S_{l-1} = A.sum(l,r)$

- %%xem như chữ a trên hình là A nhe;))%%

- Chứng minh toán học pro vip trên vnoi wiki
![[Pasted image 20260529204937.png]]

0. [[CP00004]]
1. [[CP00005]]
## Difference Array
- Cho $A$ là 1 mảng với $N$ số 0. Khi cần cập nhật $Q$ lần cho 1 phạm vi $[l,r]$ của mảng $A$ thêm một lượng $K$, thay vì cập nhật trực tiếp lên mảng $A$ với O(N), ta sẽ dựng 1 mảng hiệu D(A) và thao tác lên đó. Vì $D[i]$ `tượng trưng cho sự chênh lệch giá trị` giữa $A_i$ và $A_{i-1}$ nên:

	1. Nếu $A_i$ và $A_{i-1}$ cùng nằm ngoài $[l,r]$ -> giá trị của 2 phần tử không đổi -> $D_i$ không đổi
	2. Nếu $A_i$ và $A_{i-1}$ cùng nằm trong $[l,r]$ -> giá trị của 2 phần tử tăng đều 1 lượng $K$ -> $D_i$ không đổi
	3. Nếu chỉ 1 trong $A_i$ hoặc $A_{i-1}$ nằm trong $[l,r]$ -> giá trị của 2 phần tử tăng không đều -> $D_i$ đổi

- Nhận thấy chỉ trường hợp $3$ ta mới cần cập nhật $D$ và nó chỉ thỏa với $i=l$ hoặc $i-1=r <=>i=r+1$ , ta chỉ cần cập nhật lên $D_l$ và $D_{r+1}$ cho mỗi truy vấn.
- Sau khi hoàn tất truy vấn, ta chỉ cần áp dụng tính chất $A=S(0, D(A))$ để xây dựng mảng A.

0. [[CP00003]]
# IV. Mảng nhiều chiều
- Lười viết tiếp vl;))